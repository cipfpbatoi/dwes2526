# SA5. Aplicacions segures i reactives en Laravel

??? abstract "Duració i criteris d'avaluació"

    Duració estimada: 16 hores

    <hr />

    | Resultat d'aprenentatge  | Criteris d'avaluació  |
    | ------                   | -----                 |
    | RA6.-Genera pàgines web dinàmiques analitzant i utilitzant tecnologies i frameworks del servidor web que afigen codi al llenguatge de marques. | a) S'han identificat les diferències entre l'execució de codi en el servidor i en el client web. <br/>   b) S'han reconegut els avantatges d'unir totes dues tecnologies en el procés de desenvolupament de programes. <br/>   c) S'han identificat les tecnologies i frameworks relacionades amb la generació per part del servidor de pàgines web amb guions embeguts. <br/>d) S'han utilitzat aquestes tecnologies i frameworks per a generar pàgines web que incloguen interacció amb l'usuari.<br/> e) S'han utilitzat aquestes tecnologies i frameworks, per a generar pàgines web que incloguen verificació de formularis. <br/> f) S'han utilitzat aquestes tecnologies i frameworks per a generar pàgines web que incloguen modificació dinàmica del seu contingut i la seua estructura.<br/> g) S'han aplicat aquestes tecnologies i frameworks en la programació d'aplicacions web. |

## SA 5.1 Autenticació, hashing i autorització

### 🌬️🍃 Laravel Breeze: registre, login, logout

Laravel Breeze és el starter kit oficial més simple per implementar autenticació en Laravel. Inclou rutes, controladors i vistes per a registre, login i logout.

Per **instal·lar-lo**, cal usar els comandos corresponents per a afegir el paquet, generar el frontend i aplicar les migracions.

```bash
./vendor/bin/sail shell
composer require laravel/breeze --dev
php artisan breeze:install blade
npm install && npm run dev
php artisan migrate
``` 
**Recuperació de l'usuari autenticat**
Un cop l'usuari ha fet login, podem accedir a les seues dades:
```php
use Illuminate\Support\Facades\Auth;

// Usuari autenticat
$user = Auth::user();

// ID de l'usuari autenticat
$id = Auth::id();
```

També podem obtenir l’usuari des d'una **petició injectada al controlador**:
```php
public function dashboard(Request $request)
{
    $user = $request->user(); // Equivalent a Auth::user()
}
```

**Logout**
Laravel Breeze inclou logout preconfigurat:
```php
<form method="POST" action="{{ route('logout') }}">
    @csrf
    <button type="submit">Logout</button>
</form>
```

**Restabliment de contrasenya**
Laravel Breeze genera automàticament els formularis i la lògica necessària, soles has de
configurar el correu SMTP al **fitxer `.env`**.
- 

**Hashing automàtic de contrasenyes**

Laravel utilitza el sistema `Hash` per a encriptar contrasenyes abans de guardar-les a la base de dades. Breeze ja ho implementa automàticament en el registre.

```php
use Illuminate\Support\Facades\Hash;

$user = User::create([
    'name' => $request->name,
    'email' => $request->email,
    'password' => Hash::make($request->password),
]);
```

### 🔒 Protecció

#### 🛣️ Protecció de rutes amb `auth`

Per a protegir rutes perquè només siguen accessibles per usuaris autenticats, es fa ús del middleware `auth`. Aquest es pot aplicar tant a **grups de rutes**:

```php
Route::middleware(['auth'])->group(function () {
    Route::resource('equips', EquipController::class);
});
```

com a **rutes individuals**:

```php
Route::get('/dashboard', function () {
    return view('dashboard');
})->middleware('auth');
``` 
 
#### 🚦Protecció amb middlewares
 
##### 🔍 1.Què és un middleware?

Un middleware és una classe que actua com a intermediari entre una sol·licitud HTTP i la seua resposta. Permet executar lògica abans o després d’arribar al controlador.

S’usa per a:
 
- 🔐 Autenticació d’usuaris
- 🛡️ Validació de rols i permisos
- 🧼 Neteja o modificació de peticions/respostes

⚙️ Exemple senzill de **middleware**

```php
public function handle($request, Closure $next)
{
    if (Auth::check()) {
        return $next($request); // Continua amb la sol·licitud
    }
    return redirect('login'); // Redirigeix si no està autenticat
}
```

##### 🧩 2. Rols i permisos

Primer, hem d'afegir camp role a la taula users

1. Crear una **migració**:
   ```bash
   php artisan make:migration add_role_to_users_table --table=users
   ```
2. Afegir el **camp `role`**:
   ```php
   Schema::table('users', function (Blueprint $table) {
       $table->string('role')->default('user'); // Opcions: 'user', 'admin', etc.
   });
   ```
3. Actualitzar el **model `User`**:
   ```php
   class User extends Authenticatable
   {
       protected $fillable = ['name', 'email', 'password', 'role'];
   }
   ```

##### 🛡️ 3. Middleware personalitzat per a rols

1. Crear el **middleware**:
   ```bash
   php artisan make:middleware RoleMiddleware
   ```
2. Definir la **lògica**:
   ```php
   namespace App\Http\Middleware;

    use Closure;
    use Illuminate\Support\Facades\Auth;
    
    class RoleMiddleware
    {
        public function handle($request, Closure $next, $role)
        {
            if (Auth::check() && Auth::user()->role === $role) {
                return $next($request);
              }
            abort(403, 'Accés no autoritzat');
        }
    }
   ```
3. Registrar-lo a **`Kernel.php`**:
   ```php
   protected $routeMiddleware = [
       'role' => \App\Http\Middleware\RoleMiddleware::class,
   ];
   ```
4. Aplicar-lo a una **ruta**:
 
   ```php
   Route::get('/admin', function () {
       return view('admin.dashboard');
   })->middleware('role:admin');
   ```
   o en **laravel 12**, directament al **controlador**:
   
```php
  use Illuminate\Routing\Attributes\Middleware;
  
  #[Middleware('role:admin')]
  class AdminController extends Controller
  {
    public function dashboard()
    {
      return view('admin.dashboard');
    }
  }
```
#### 🛡️  Polítiques (`Policy`) per  autoritzacions
 
Les **policies** en Laravel permeten controlar l’accés a recursos de manera precisa i reutilitzable. Es poden aplicar automàticament als models o explícitament mitjançant mètodes com `authorize()`.

##### 🛠️ 1. Crear una Policy

Es genera una **política associada a un model** per controlar qui pot realitzar accions sobre aquest recurs.

```bash
./vendor/bin/sail artisan make:policy PostPolicy --model=Post
``` 

Es crea a **app/Policies/PostPolicy.php**.

##### 🧠 2. Definir les regles d’autorització

Dins la policy es **defineixen mètodes** com `view`, `create`, `update` o `delete` que retornen si un usuari pot realitzar o no eixa acció.

```php
public function update(User $user, Post $post)
{
  return $user->id === $post->user_id;
}
``` 

Cada mètode pot retornar:
- true (permés)
- false (denegat)
- O fins i tot llançar excepcions o missatges personalitzats

##### 🧾 3. Registrar la Policy

Cal **registrar la política** al proveïdor d’autenticació **(`AuthServiceProvider`)** per vincular el model amb la seua policy corresponent.

```php
use App\Models\Post;
use App\Policies\PostPolicy;

protected $policies = [
Post::class => PostPolicy::class,
];
``` 

##### 🧪 4. Utilitzar-la en controladors

Dins dels controladors, s’utilitza la **funció `authorize()`** per verificar si l’usuari pot executar una acció determinada sobre un recurs.

```php
public function edit(Post $post)
{
  $this->authorize('update', $post);
  return view('posts.edit', compact('post'));
}
```

##### ✅ 5. Ús en vistes Blade

Amb la **directiva `@can`**, podem controlar l’accés a botons o seccions visuals segons la política definida.

```bladehtml
@can('update', $post)
<a href="{{ route('posts.edit', $post) }}">Editar</a>
@endcan
```

##### 🔁 6. Regles globals

És possible definir regles generals dins la policy (com per exemple donar accés total als usuaris administradors) mitjançant el **mètode `before()`**.

```php
public function before(User $user, $ability)
{
  if ($user->role === 'admin') {
    return true; // accés total
  }
}
```
 
## SA 5.2 Formularis amb seguretat i feedback

### 📋✅ Validació amb `FormRequest`

La validació de dades pot separar-se del controlador utilitzant **classes de tipus `FormRequest`**. Aquestes classes permeten definir regles de validació clares i reutilitzables, millorant la neteja del codi.

```bash
php artisan make:request StoreEquipRequest
``` 

A la classe generada, **defineixes**:

```php
public function rules()
{
    return [
    'nom' => 'required|string|max:255',
    'categoria' => 'required|string|max:100',
    ];
}
```

I al **controlador**:

```php
public function store(StoreEquipRequest $request)
{
  Equip::create($request->validated());  // validated() retorna només les dades validades, evitant riscos de mass assignment.
  return redirect()->route('equips.index');
}
``` 
### 🛡️ Autorització dins de FormRequest amb Policies

Cada FormRequest inclou un **mètode  authorize()** per controlar si l’usuari té permís per a executar l’acció abans de validar les dades. És el lloc idoni per invocar una policy.

**Exemple amb policy:**
Si tenim una policy EquipPolicy@update, dins el FormRequest:
 
```php
public function authorize(): bool
{
    $equip = $this->route('equip'); // Obtenim el model Equip des de la ruta
                                    // Només funcionarà si en la definició de rutes has fet binding del model com Route::put('/equips/{equip}', ...).
    return $this->user()->can('update', $equip); // Crida a la policy
}
``` 

- Si no pot, Laravel llança automàticament un error **403 Forbidden**.
- Si pot, executa la validació.


**Alternativa amb Gate::allows()**

També pots usar:

```php
use Illuminate\Support\Facades\Gate;

public function authorize(): bool
{
    return Gate::allows('update', $this->route('equip'));
}
``` 

### 🛡️🔄⏮️⚠️ Elements bàsics en vistes amb formularis

- `@csrf`: Protecció contra atacs de tipus cross-site request forgery
- `@method(´PUT´)`: Permet enviar formularis amb verbs PUT o DELETE
- `old('camp')`: Manté les dades introduïdes en cas d’error de validació, després d'un error de validació.
- `@error('camp')`: Mostra els errors de validació associats a cada camp després d'un error de validació.

### Missatges flash amb `session()->flash()`

Permeten mostrar **missatges temporals** (èxit, error, etc.) després d’una acció, com una redirecció després de crear o modificar un recurs.

```php
return redirect()->route('equips.index')->with('ok', 'Equip creat correctament!');
```

A la vista **Blade**:

```bladehtml
@if (session('ok'))
    <div class="alert alert-success">
        {{ session('ok') }}
    </div>
@endif
```

#### ✨ UX i manteniment d'estat

L'ús combinat de `old()`, `@error`, missatges flash i bones pràctiques de disseny millora significativament l’experiència d’usuari (UX) en formularis.
 
#### ❗ Mostrar Errors de Validació a la Vista
   
Quan es produeixen errors de validació, Laravel redirigeix automàticament a la vista anterior amb la variable global `$errors`, que conté els errors de validació.

Exemple de com mostrar un **llistat d'errors** al començament del formulari:
```php
@if ($errors->any())
    <ul>
        @foreach($errors->all() as $error)
            <li>{{ $error }}</li>
        @endforeach
    </ul>
@endif
```

A **sota de cada camp**:
  
```php
<div class="form-group">
    <label for="title">Títol:</label>
    <input type="text" name="title" id="title" class="form-control" value="{{ old('title') }}">
    @if ($errors->has('title'))
        <div class="text-danger">{{ $errors->first('title') }}</div>
    @endif
</div>
```
 
### 4.7 Extensió opcional: CRUD dinàmic amb Livewire
- Introducció a Livewire
- Creació de component CRUD
- Connexió amb Service i Repository
- Millora UX sense JS explícit

##  Exercicis

###  🏟️ Exercici guiat: Reestructurar projecte Futbol Femení amb BD + Repository + Service

#### 🎯 Objectiu
Reestructurar l’aplicació de futbol femení (feta sense persistència) cap a una arquitectura escalable amb:
 
- Validació amb FormRequest
- Autenticació

---

 
#### 1. 🧪 Validació amb FormRequest

**Crear Validació**

```bash
./vendor/bin/sail artisan make:request StoreEquipRequest
./vendor/bin/sail artisan make:request UpdateEquipRequest
``` 

**Modificar els fitxers**

[StoreEquipRequest](https://github.com/Curs-2025-26/futbol-femeni/blob/bdd/app/Http/Requests/StoreEquipRequest.php)
[UpdateEquipRequest](https://github.com/Curs-2025-26/futbol-femeni/blob/bdd/app/Http/Requests/UpdateEquipRequest.php)

#### 2. 💡 Controlador final

[EquipController](https://github.com/Curs-2025-26/futbol-femeni/blob/bdd/app/Http/Controllers/EquipController.php)

**Adaptar les [vistes](https://github.com/Curs-2025-26/futbol-femeni/bdd/escut/resources/views/equips)**

#### 3.  🛡️ Afegir un escut a l'equip  (Branca escut)

**Crear una migració per afegir un camp `escut` a la taula `equips`**

```bash
./vendor/bin/sail artisan make:migration add_escut_to_equips_table
```

Modificar la migració [`add_escut_to_equips_table`](https://github.com/Curs-2025-26/futbol-femeni/blob/bdd/database/migrations/2025_08_31_044414_add_escut_to_equips_table.php)

**Aplicar la migració**

```bash
./vendor/bin/sail artisan migrate
```   

**Modificar el model `Equip` per incloure el camp `escut`**

```php 
protected $fillable = ['nom', 'estadi_id', 'titols', 'escut'];
``` 

**Modificar la vista `equips.create` per incloure un camp d'arxiu per pujar l'escut de l'equip i incloure enctype="multipart/form-data" al  formulari**

```bladehtml
<form action="{{ route('equips.store') }}" method="POST" enctype="multipart/form-data">

<div class="mb-4">
    <label for="escut" class="block text-sm font-medium text-gray-700 mb-1">Escut:</label>
    <input type="file" name="escut" id="escut"
        class="w-full border-gray-300 rounded-lg shadow-sm focus:ring-blue-500 focus:border-blue-500">
</div>
```


**Crear la  vista [`equips.edit`](https://github.com/Curs-2025-26/futbol-femeni/blob/escut/resources/views/equips/edit.blade.php) **

**Crear un enllaç simbòlic a la carpeta storage**

```bash
./vendor/bin/sail artisan storage:link
```
**Modificar el [controlador](https://github.com/Curs-2025-26/futbol-femeni/blob/escut/app/Http/Controllers/EquipController.php) per passar el fitxer al servei**

**Actualitzar les [validacions](https://github.com/Curs-2025-26/futbol-femeni/tree/escut/app/Http/Requests) per incorporar el camp escut**
**Actualitzar el mètode store,update i destroy del [servei](https://github.com/Curs-2025-26/futbol-femeni/blob/escut/app/Services/EquipService.php)**

**Modificat el [component](https://github.com/Curs-2025-26/futbol-femeni/blob/escut/resources/views/components/equip.blade.php) de la vista [`equips.show`](https://github.com/Curs-2025-26/futbol-femeni/blob/escut/resources/views/equips/show.blade.php) per mostrar l'escut de l'equip**



###  🏁 Exercici Final: Guia de Futbol Femení II

#### 🎯 Objectiu
Transformar i ampliar l’aplicació del projecte anterior per a incorporar:
 
- Validació robusta amb FormRequest
- Autenticació i autorització amb Laravel Breeze i Policies
- Components visuals, relacions entre models i funcionalitats avançades

---
#### 1. Autenticació i restriccions
- Laravel Breeze per login, logout
- Protegeix rutes amb `auth` i `@auth` en vistes
- Policies per controlar:
   - Jugadores: només el manager del seu equip
   - Partits: només l’àrbitre assignat
- No es permet crear partits manualment

---

#### 2. Formularis amb FormRequest
- Crea `EstadiRequest`, `JugadoraRequest`, `PartitRequest`
- Valida:
   - `data_naixement` mínima de 16 anys
   - `foto` (tipus .png i mida màxima)
   - `dorsal`, `capacitat`, `gols` (numèrics positius)
- Usa `authorize()` per controlar accés a modificació segons rol

---

 
#### 3. Classificació en temps real amb Livewire
- Taula amb:
   - Nom de l’equip, punts, gols a favor/en contra, diferència, etc.
- Component Livewire que es refresca automàticament
- Ordenació per punts i diferència de gols

---

#### 4. Proves
- Crea proves per:
   - EstadiController
   - JugadoraController
   - PartitController
   - FormRequest i Policies

---

#### 5. Correu a àrbitres
- Enviar correu personalitzat a cada àrbitre amb:
   - Llistat de partits en què arbitrarà
   - Format HTML amigable

