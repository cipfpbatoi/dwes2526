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

Per **instal·lar-lo**, cal usar els comandos corresponents per a afegir el paquet, generar el frontend i aplicar les **migracions**.

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

Laravel utilitza el sistema `Hash` per a encriptar contrasenyes abans de guardar-les a la base de dades. Breeze ja ho implementa automàticament en el **registre**.

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
 
## SA 5.2 Seguretat en Formularis  i feedback

### ⚠️ Personalitzar Missatges d'Error

Podem personalitzar els missatges d'error sobreescrivint el mètode **messages()** dins del Form Request:
```php
public function messages()
{
    return [
        'title.required' => 'El camp títol és obligatori.',
        'title.min' => 'El camp títol ha de tindre almenys 3 caràcters.',
        'year.required' => 'El camp any és obligatori.',
    ];
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

###  🔄  Elements bàsics en vistes amb formularis

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

## 🌍 Ús d'idiomes en Laravel (Internalització)

Laravel proporciona eines senzilles i potents per a la **localització d'aplicacions**, permetent suportar múltiples idiomes. Aquesta funcionalitat és ideal per a desenvolupar aplicacions accessibles a usuaris de diferents regions i llengües.

### 1️⃣ Configuració Inicial
 
L'idioma predeterminat s'estableix al fitxer `config/app.php` mitjançant el paràmetre `locale`:
```php
'locale' => 'ca', // o 'es', 'en', etc.
'fallback_locale' => 'en', //altenNATIU
```
 
### 2️⃣  Fitxers de Traducció
 
Els fitxers de traducció es guarden al directori `lang`. Cada idioma té la seua pròpia carpeta, amb fitxers `.php` que contenen arrays clau-valor per a les traduccions:

**Exemple d'estructura:**
```
/lang
    /en
        messages.php
    /es
        messages.php
```

**Exemples de ftixer**
```php
// lang/en/messages.php
return [
    'welcome' => 'Welcome to our application!',
];
```

Per a altres idiomes:
```php
// lang/es/messages.php
return [
    'welcome' => '¡Bienvenido a nuestra aplicación!',
];
```

---

### 3️⃣ Ús de Traduccions en el Codi
 
Utilitza la funció auxiliar `__()` per obtenir les traduccions:
```php
echo __('messages.welcome'); // Welcome to our application!
```
Amb paràmetres:
 
```php
// lang/en/messages.php
return [
    'greeting' => 'Hello, :name!',
];
```
```php
echo __('messages.greeting', ['name' => 'John']); // Hello, John!
```

 

#### 4️⃣ Canviar l'Idioma Dinàmicament

Per canviar l'idioma de l'aplicació en temps d'execució, utilitza el mètode `App::setLocale()`:

```php
use Illuminate\Support\Facades\App;

App::setLocale('es'); // Canvia a espanyol
```

Aquesta configuració només afecta la petició actual.


### 5️⃣ Traduccions amb Fitxers JSON

Laravel permet utilitzar fitxers JSON per a traduccions simples. Aquest enfocament és útil per a aplicacions amb cadenes de traducció úniques i desordenades.

**Exemple de Fitxer JSON:**

// lang/es.json

```json

{
    "I love programming.": "Me encanta programar."
}
```

Per accedir a aquestes cadenes:
```php
echo __('I love programming.');
```

# 📬 Enviament de Correus en Laravel 12

Laravel proporciona una API elegant per a l’enviament de correus electrònics a través de múltiples serveis (SMTP, Mailgun, Postmark, Amazon SES...).

---

## 1️⃣ Configuració del Servei de Correu

Edita el fitxer `.env`:

```env
MAIL_MAILER=smtp
MAIL_HOST=smtp.gmail.com
MAIL_PORT=587
MAIL_USERNAME=el_teu_email@gmail.com
MAIL_PASSWORD=la_teua_contrasenya
MAIL_ENCRYPTION=tls
MAIL_FROM_ADDRESS=el_teu_email@gmail.com
MAIL_FROM_NAME="Nom del Projecte"

```
El fitxer config/mail.php carregarà automàticament aquests valors.

### 2️⃣ Crear una Classe de Correu

 
```bash
php artisan make:mail WelcomeMail
```

Aquest comandament crea una classe al directori `App\Mail`. Aquesta classe és on es defineix el contingut i el disseny del correu.

**Exemple**

```php
namespace App\Mail;

use Illuminate\Bus\Queueable;
use Illuminate\Mail\Mailable;
use Illuminate\Queue\SerializesModels;

class WelcomeMail extends Mailable
{
    use Queueable, SerializesModels;

    public $user;

    public function __construct($user)
    {
        $this->user = $user;
    }

    public function build()
    {
        return $this->view('emails.welcome')
                    ->subject('Benvingut a la nostra aplicació');
    }
}
```

### 3️⃣ Crear la Vista del Correu
resources/views/emails/benvinguda.blade.php

```bladehtml
<h1>Hola, {{ $usuari->name }}!</h1>
<p>Gràcies per unir-te a la nostra aplicació.</p>
```

### Enviar el Correu

Des d’un controlador:

```php
use App\Mail\WelcomeMail;
use Illuminate\Support\Facades\Mail;

Mail::to('usuari@example.com')->send(new WelcomeMail($user));
```

**Enviar correus a múltiples destinataris**

```php
Mail::to(['user1@example.com', 'user2@example.com'])->send(new WelcomeMail($user));
```

### 5️⃣ Correus amb Markdown

Laravel permet crear correus amb components de Markdown. Generem un correu amb components:
```bash
php artisan make:mail WelcomeMail --markdown=emails.welcome
```

Aquest comandament crea una plantilla Markdown a `resources/views/emails`.

Exemple de plantilla Markdown:

```bladehtml
@component('mail::message')
    # Hola, {{ $usuari->name }}
    
    Benvingut/da a la nostra aplicació!
    
    @component('mail::button', ['url' => 'https://example.com'])
    Visita'ns
    @endcomponent
    
    Gràcies,<br>
    {{ config('app.name') }}
@endcomponent

```

### 6️⃣ Correus en cua (asíncrons)

Per millorar el rendiment:
```php
Mail::to('usuari@example.com')->queue(new WelcomeMail($user));
```

Assegura't que el sistema de cues estiga configurat al fitxer `.env`:
```env
QUEUE_CONNECTION=database
```

## 🗂️ Gestió de Fitxers en Laravel 12

Laravel proporciona una API senzilla per treballar amb fitxers i directoris a través del component `Storage`.

 
### 1️⃣ Configuració del Sistema de Fitxers

Els “discs” es configuren al fitxer `config/filesystems.php`.

#### Tipus comuns:
- `local`: emmagatzematge intern (no accessible públicament)
- `public`: fitxers accessibles via navegador
- `s3`: Amazon S3 o altres serveis compatibles

#### `.env`:

```env
FILESYSTEM_DISK=local
AWS_ACCESS_KEY_ID=el_teu_access_key
AWS_SECRET_ACCESS_KEY=el_teu_secret_key
AWS_DEFAULT_REGION=us-east-1
AWS_BUCKET=el_teu_bucket
```

### 2️⃣ Operacions Bàsiques

**Guardar fitxers**
 
```php
use Illuminate\Support\Facades\Storage;

// Text
Storage::put('documents/info.txt', 'Contingut');

// Arxiu pujat
Storage::putFile('uploads', $request->file('document'));

// Amb nom personalitzat
Storage::putFileAs('uploads', $request->file('document'), 'factura.pdf');

```
 
***Llegir i verificar fitxers**

```php
// Obtenir el contingut d'un fitxer
$content = Storage::get('documents/file.txt');

// Verificar si un fitxer existeix
if (Storage::exists('documents/file.txt')) {
    // Fitxer existeix
}
```

**Eliminar Fitxers**
```php
// Eliminar un fitxer
Storage::delete('documents/file.txt');

// Eliminar múltiples fitxers
Storage::delete(['file1.txt', 'file2.txt']);
```

**Llistar Fitxers i carpetes**

```php
// Llistar tots els fitxers d'un directori
$files = Storage::files('documents');

// Llistar fitxers recursivament
$allFiles = Storage::allFiles('documents');

// Llistar carpetes
$directories = Storage::directories('documents');

// Llistar carpetes recursivament
$allDirectories = Storage::allDirectories('documents');
```

### 3️⃣ Fitxers Públics

Per servir fitxers públicament, utilitza el disc public i crea un enllaç simbòlic:
```bash
php artisan storage:link
```

**Obtenir una URL Pública**

```php
$url = Storage::url('documents/file.txt'); // Genera una URL pública
```

4️⃣ Amazon S3

Inclou les credencials d'Amazon S3 al fitxer `.env`:
```env
AWS_ACCESS_KEY_ID=el_teu_access_key
AWS_SECRET_ACCESS_KEY=el_teu_secret_key
AWS_DEFAULT_REGION=us-east-1
AWS_BUCKET=el_teu_bucket
```

**Exemple**
```php
use Illuminate\Support\Facades\Storage;

// Guardar un fitxer a S3
Storage::disk('s3')->put('documents/file.txt', 'Contingut');

// Obtenir una URL
$url = Storage::disk('s3')->url('documents/file.txt');
```
##   ✅ Testing en Laravel 12

Laravel inclou una infraestructura de proves robusta basada en PHPUnit, que permet realitzar proves unitàries, d'integració i de funcionalitat HTTP.
 

### 🧪 Tipus de proves

- Proves Unitàries : Validen la lògica d’un component aïllat (model, servei, etc.).

- Proves de Funcionalitat (Feature Tests) : Simulen sol·licituds HTTP completes i proven controladors, middleware, i rutes.

- Proves de Base de Dades: Verifiquen la persistència i integritat de les dades (amb `RefreshDatabase` o `DatabaseTransactions`).

- Proves de Navegació amb Dusk: Permeten interactuar amb l’aplicació mitjançant un navegador real o virtual.

---

### ⚙️ Configuració

### `.env.testing`
Defineix la configuració per a l’entorn de proves:

```env
APP_ENV=testing
DB_CONNECTION=sqlite
DB_DATABASE=:memory:
```
S’utilitza automàticament en executar **php artisan test**.
 
### ✏️ Crear proves

Per generar una prova:
```bash
php artisan make:test EquipServiceTest         # Prova unitària
php artisan make:test EquipCrudTest --unit      # Prova unitària (opció explícita)
php artisan make:test UserFeatureTest           # Prova de feature

```

**Exemple de Prova feature amb Validació i Autenticació** 

```php
namespace Tests\Feature;

use Tests\TestCase;
use App\Models\User;
use Illuminate\Foundation\Testing\RefreshDatabase;

class EquipFeatureTest extends TestCase
{
    use RefreshDatabase;

    public function test_creacio_equip_requereix_autenticacio_i_valida()
    {
        $user = User::factory()->create();

        // Prova redirecció sense login
        $this->get(route('equips.create'))
             ->assertRedirect(route('login'));

        // Prova validació invàlida
        $this->actingAs($user)
             ->post(route('equips.store'), [])
             ->assertSessionHasErrors(['nom', 'categoria']);

        // Prova validació vàlida
        $data = ['nom' => 'Nou Equip', 'categoria' => 'Base'];
        $this->actingAs($user)
             ->post(route('equips.store'), $data)
             ->assertRedirect(route('equips.index'))
             ->assertSessionHas('success'); // si s’usa missatge flash
    }
}

```

### Proves de Base de Dades

####   Migracions 

Utilitza el trait `RefreshDatabase` per executar les migracions abans de cada prova:

**Exemple de CRUD complet amb Base de Dades**
```php
namespace Tests\Feature;

use Tests\TestCase;
use App\Models\User;
use App\Models\Equip;
use Illuminate\Foundation\Testing\RefreshDatabase;

class EquipCrudTest extends TestCase
{
    use RefreshDatabase;

    public function test_crud_complet_d_equip()
    {
        $user = User::factory()->create();
        $this->actingAs($user);

        // CREATE
        $equip = Equip::factory()->create(['nom' => 'Equip A']);
        $this->assertDatabaseHas('equips', ['nom' => 'Equip A']);

        // UPDATE
        $equip->update(['nom' => 'Equip B']);
        $this->assertDatabaseHas('equips', ['nom' => 'Equip B']);

        // DELETE
        $equip->delete();
        $this->assertDatabaseMissing('equips', ['nom' => 'Equip B']);
    }
}

```

**Exemple de prova unitària amb Service o Repository**
```php
namespace Tests\Unit;

use Tests\TestCase;
use App\Models\Estadi;
use App\Services\EquipService;
use Illuminate\Foundation\Testing\RefreshDatabase;

class EquipServiceTest extends TestCase
{
    use RefreshDatabase;

    public function test_service_crea_equip_correctament()
    {
        $estadi = Estadi::factory()->create();
        $service = new EquipService();
        $equip = $service->create([
            'nom' => 'València CF',
            'categoria' => 'Pro',
            'estadi_id' => $estadi->id,
        ]);

        $this->assertDatabaseHas('equips', ['nom' => 'València CF']);
        $this->assertEquals('València CF', $equip->nom);
    }
}

```

 
### Bones pràctiques

-  Refactoritzar el codi amb Service, Repository, etc.
-  Usar factories per crear dades de prova.
-  Fer proves independents i narratives (test-first sempre que siga possible).
-  Provar estats de sessió, permisos i policies.
-  Executar proves en paral·lel si ho permet la màquina (php artisan test --parallel).

##  🌀 Laravel Livewire 3 – Desenvolupament d’interfícies reactives amb PHP

**Livewire 3** és una llibreria per Laravel que permet desenvolupar components interactius i reactius directament amb PHP, sense necessitat d'escriure JavaScript.

---

### ✅ 1. Instal·lació i configuració bàsica

```bash
composer require livewire/livewire

```
 
Inclou els scripts de Livewire en les teues vistes Blade:
```bladehtml
@livewireStyles
@livewireScripts
```

Opcional per usar vite (Laravel 12):

```bash
php artisan livewire:configure-vite

```

### 🧱 2. Crear components

**Generar un Component**
 
```bash
php artisan make:livewire HelloWorld
```

Això genera:
- Un fitxer de classe PHP: `app/Livewire/HelloWorld.php`
- Una plantilla Blade: `resources/views/livewire/hello-world.blade.php`

**Exemple de Component**

app/Livewire/HelloWorld.php
```php
namespace App\Livewire;

use Livewire\Component;

class HelloWorld extends Component
{
    public $message = "Hola, món!";

    public function render()
    {
        return view('livewire.hello-world');
    }
}
```

resources/views/livewire/hello-world.blade.php
```bladehtml
<div>
    <h1>{{ $message }}</h1>
</div>
```

**Inserir component en una vista**
```html
<livewire:hello-world />
```

### 🔁 3. Propietats reactives i accions

#### Propietats i bindings
Les propietats de la classe PHP es poden vincular directament als camps d'un formulari HTML:

```php
class Counter extends Component
{
    //propietat
    public $count = 0;

    //mètode del component
    public function increment()
    {
        $this->count++;
    }

    public function render()
    {
        return view('livewire.counter');
    }
}
```

 
```bladehtml
<div>
    <button wire:click="increment">+</button>
    <h1>{{ $count }}</h1>
</div>
```


### 💬 4. Validació

Livewire permet validar dades a mesura que l'usuari interactua amb el formulari:

**Tradicional**

```php
protected $rules = [
'nom' => 'required|string|min:3',
];

public function guardar() {
$this->validate();
}
```php

**En temps real**

```php
protected $rules = ['nom' => 'required|min:3'];

public function updated($propertyName)
{
    $this->validateOnly($propertyName);
}

```

### 📦 5. Components amb formularis

 
```php
public $nom, $email;

public function enviar()
{
$this->validate([
'nom' => 'required',
'email' => 'required|email',
]);

// Guardar o enviar dades...
}
 
```
```bladehtml
<form wire:submit.prevent="enviar">
    <input type="text" wire:model="nom">
    @error('nom') <span>{{ $message }}</span> @enderror

    <input type="email" wire:model="email">
    @error('email') <span>{{ $message }}</span> @enderror

    <button>Enviar</button>
</form>
```

### 🧠 6. Exemple complet

contador.php
```php
namespace App\Livewire;

use Livewire\Component;

class Contador extends Component
{
    public $valor = 0;

    public function incrementar() { $this->valor++; }

    public function render() {
        return view('livewire.contador');
    }
}
```
contador.blade.php
```bladehtml
<div>
    <button wire:click="incrementar">+</button>
    <span>{{ $valor }}</span>
</div>

```
### 7. Altres funcionalitats útils

**Hooks**

- mount(): s’executa en inicialitzar el component.
- hydrate(): després de cada request.
- dehydrate(): abans d’enviar al client.

**Flash messages**

```php
session()->flash('missatge', 'Guardat!');
```

```bladehtml
@if (session()->has('missatge'))
<div>{{ session('missatge') }}</div>
@endif
```

### 🔐 8. Amb autenticació i autorització

```php
public function mount()
{
    if (!auth()->check()) {
        abort(403);
    }
}

```

### 🧪 9. Proves de components Livewire

```php
namespace Tests\Feature\Livewire;

use Tests\TestCase;
use Livewire\Livewire;
use App\Livewire\HistorialPartits;
use App\Models\Partit;
use Illuminate\Foundation\Testing\RefreshDatabase;

class HistorialPartitsTest extends TestCase
{
    use RefreshDatabase;

    public function test_filtre_livewire_mostra_correctament()
    {
        Partit::factory()->create(['equip_local' => 'A']);
        Partit::factory()->create(['equip_local' => 'B']);

        Livewire::test(HistorialPartits::class)
            ->set('equip', 'A')
            ->call('filtrar')
            ->assertSee('A')
            ->assertDontSee('B');
    }
}

```

### 🧩 10. Avantatges de Livewire

- Sense JavaScript
- Integració directa amb Laravel
- Ideal per a CRUD i components de UI dinàmics
- Compatible amb Alpine.js

##  Exercicis

###  🏟️ Exercici guiat: Reestructurar projecte Futbol Femení amb BD + Repository + Service

#### 🎯 Objectiu
Reestructurar l’aplicació de futbol femení (feta sense persistència) cap a una arquitectura escalable amb:
 
- Validació amb FormRequest
- Autenticació

---
c
#### 1.  🛡️ Afegir un escut a l'equip  (Branca escut)

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


#### 🔑 2. Configurar l'autenticació amb Laravel Breeze

1. Canviar el nom del fitxer app.blade.php de la carpeta resources/views/layouts a equip.blade.php.
2. Guarda les rutes de la Guia d'Equips de Futbol Femení en algun fitxer per utilitzar després.
3. Instal·la Laravel Breeze:

```bash
composer require laravel/breeze --dev
php artisan breeze:install
npm install && npm run build
php artisan migrate
```
Triarem **blade amb alpine** i **PHPUNIT**

4. Canviar totes les vistes per a que extenguen de layouts.equip

#### 👥 3.  Afegir els rols al sistema
  
**Crea una nova migració per afegir el camp `role` a usuaris**
 
   ```bash
   php artisan make:migration add_role_to_users_table --table=users
   ```
   Afegeix el [camp](https://github.com/Curs-2025-26/futbol-femeni/blob/escut/database/migrations/2025_09_03_171410_add_role_to_users_table.php) i aplica-la:
   ```php
   Schema::table('users', function (Blueprint $table) {
       $table->string('role')->default('arbitre');
   });
   ```
   Aplica la migració:
   ```bash
   php artisan migrate
   ```

**Crea el seeders d'usuaris i crea un usuari administrador**

```bash
 php artisan make:seeder UserSeeder
``` 

**Executa el [seeder](https://github.com/Curs-2025-26/futbol-femeni/blob/escut/database/seeders/UserSeeder.php) havent canviat [DatabaseSeeder](https://github.com/Curs-2025-26/futbol-femeni/blob/escut/database/seeders/DatabaseSeeder.php )**

#### 🚪3. Middleware per a permisos de rol i manager
 
- **Genera el middleware**
   ```bash
   php artisan make:middleware RoleMiddleware
   ```
- **Defineix el control dels rols en el metode [handle](https://github.com/Curs-2025-26/futbol-femeni/blob/escut/app/Http/Middleware/RoleMiddleware.php)**
 
- **Aplica  Middleware a [rutes](https://github.com/Curs-2025-26/futbol-femeni/blob/escut/routes/web.php)** fent que  les rutes per tal que els equips,estadis soles puguen modificar-los els administradors. 
 
 
#### 🧑‍💼👥 4. Associar managers a equips

 
**Crea una migració nova**
```bash
   php artisan make:migration add_team_id_to_users_table --table=users
```

**Afegeix el camp [`team_id`](https://github.com/Curs-2025-26/futbol-femeni/blob/escut/database/migrations/2025_09_03_174708_add_team_id_to_users_table.php)**  i **aplica la migració**
   ```bash
   php artisan migrate
   ```

**Assigna equips als managers, creant u manager per equip i assigna-li** 

[EquipsSeeder](https://github.com/Curs-2025-26/futbol-femeni/blob/escut/database/seeders/EquipsSeeder.php)   

 
**Defineix la relació al model [`User`](https://github.com/Curs-2025-26/futbol-femeni/blob/escut/app/Models/User.php)**
 
**Defineix la relació inversa al model [`Equip`](https://github.com/Curs-2025-26/futbol-femeni/blob/escut/app/Models/Equip.php)**
  


### 🧩🖼️ 5. Adaptar les vistes al component layout de Breeze

1. Modificar equips.blade.php per a utilitzar el layout de Breeze.

```php
<x-app-layout>
    <x-slot name="header">
        <h2 class="font-semibold text-xl text-gray-800 dark:text-gray-200 leading-tight">
            @yield('title','Guia de futbol femení')
        </h2>
    </x-slot>

    <div class="py-12">
        <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
            <div class="bg-white dark:bg-gray-800 overflow-hidden shadow-sm sm:rounded-lg">
                <div class="p-6 text-gray-900 dark:text-gray-100">
                    @yield('content')
                </div>
            </div>
        </div>
    </div>
    <footer>
        <p>&copy; 2024 Guia de Futbol Femení</p>
    </footer>
</x-app-layout>
```

2. Modificar la vista de l'equip per a utilitzar el layout de Breeze.

```php
@extends('layouts.equips')
```

3. Modificar el layout de Breeze per a incloure el menú de navegació .

En navigation.blade.php:
```php
    ...
    <!-- Navigation Links -->
    <div class="hidden space-x-8 sm:-my-px sm:ms-10 sm:flex">
        <x-nav-link :href="route('dashboard')" :active="request()->routeIs('dashboard')">
            {{ __('Dashboard') }}
        </x-nav-link>
    </div>
    @include('partials.menu')
    ...
```

4. En partials/menu.blade.php:
```php
    ...
    <div class="hidden space-x-8 sm:-my-px sm:ms-10 sm:flex">
        <x-nav-link :href="route('equips.index')" :active="request()->routeIs('dashboard')">
            {{ __('Guia Equips') }}
        </x-nav-link>
    </div>
    <div class="hidden space-x-8 sm:-my-px sm:ms-10 sm:flex">
        <x-nav-link :href="route('estadis.index')" :active="request()->routeIs('dashboard')">
            {{ __('Estadis') }}
        </x-nav-link>
    </div>
    ...
```

### Pas 6: El manager soles puga editar el seu equip

#### 1. Crear la Política
Executa el següent comandament per generar la política associada al model `Equip`:
```bash
php artisan make:policy EquipPolicy --model=Equip
```

#### 2. Definir la Lògica a la Política
Edita el fitxer generat `app/Policies/EquipPolicy.php` i afegeix les regles de permisos.


```php
namespace App\Policies;

use App\Models\User;
use App\Models\Equip;

class EquipPolicy
{
    /**
     * Determine whether the user can create models.
     */
    public function create(User $user): bool
    {
        // Només els administradors poden crear equips
        return $user->role === 'administrador';
    }

    /**
     * Determine whether the user can update the model.
     */
    public function update(User $user, Equip $equip)
    {
        // Permetre si l'usuari és un administrador o un manager i està assignat a aquest equip
        return $user->role === 'administrador' || ($user->role === 'manager' && $user->equip_id === $equip->id);
    }

    /**
     * Determina si l'usuari pot eliminar l'equip.
     *
     * @param  \App\Models\User  $user
     * @param  \App\Models\Equip $equip
     * @return bool
     */
    public function delete(User $user, Equip $equip)
    {
        // Només els administradors poden eliminar equips
        return $user->role === 'administrador';
    }
}
```


#### 3. Utilitzar la Política al Controlador
Al controlador `EquipController`, utilitza el mètode `authorize` per aplicar la política abans de permetre accions.

```php
class EquipController extends Controller
{

    use AuthorizesRequests;

    public function index() {
        $equips = Equip::all();
        return view('equips.index', compact('equips'));
    }

    public function show(Equip $equip) {
        return view('equips.show', compact('equip'));
    }

    public function create() {
        $this->authorize('create');
        $estadis = Estadi::all();
        return view('equips.create',compact('estadis'));
    }

    public function edit(Equip $equip) {
        $this->authorize('update', $equip);
        $estadis = Estadi::all();
        return view('equips.edit', compact('equip','estadis'));
    }


    public function store(Request $request)
    {
        $this->authorize('create');
        $validated = $request->validate([
            'nom' => 'required|unique:equips',
            'titols' => 'integer|min:0',
            'estadi_id' => 'required|exists:estadis,id',
            'escut' => 'nullable|image|mimes:jpeg,png,jpg|max:2048', // Validació del fitxer
        ]);

        if ($request->hasFile('escut')) {
            $path = $request->file('escut')->store('escuts', 'public');
            $validated['escut'] = $path;
        }

        Equip::create($validated);

        return redirect()->route('equips.index')->with('success', 'Equip creat correctament!');
    }


    public function update(Request $request, Equip $equip)
    {
        $this->authorize('update', $equip);
        $validated = $request->validate([
            'nom' => 'required|unique:equips,nom,' . $equip->id,
            'titols' => 'integer|min:0',
            'estadi_id' => 'required|exists:estadis,id',
            'escut' => 'nullable|image|mimes:jpeg,png,jpg|max:2048',
        ]);


        if ($request->hasFile('escut')) {
            if ($equip->escut) {
                Storage::disk('public')->delete($equip->escut); // Esborra l'escut antic
            }
            $path = $request->file('escut')->store('escuts', 'public');
            $validated['escut'] = $path;
        }

        $equip->update($validated);

        return redirect()->route('equips.index')->with('success', 'Equip actualitzat correctament!');
    }

    public function destroy(Equip $equip)
    {
        $this->authorize('delete', $equip);
        if ($equip->escut) {
            Storage::disk('public')->delete($equip->escut);
        }
        $equip->delete();
        return redirect()->route('equips.index')->with('success', 'Equip esborrat correctament!');
    }


}
```


#### 4. Utilitzar la Política a les Vistes
A les vistes Blade, pots utilitzar les directives `@can` per verificar els permisos.


```blade
@can('update', $equip)
    <a href="{{ route('equips.edit', $equip->id) }}" class="text-yellow-600 hover:underline">Editar</a>
@endcan
```

### Pas 7. Afegir FormRequest per a la validació

####  1. Generar el Form Request

Executa el següent comandament per crear un Form Request:

```bash
php artisan make:request StoreEquipRequest
php artisan make:request UpdateEquipRequest
```

Aquest comandament crearà una classe `StoreEquipRequest` i altra `UpdateEquipRequest  al directori `app/Http/Requests`.

---

####  2. Definir les regles de validació

Obre el fitxer `StoreEquipRequest.php` i defineix les regles de validació al mètode `rules`.

##### Exemple de validació:
```php
namespace App\Http\Requests;

use Illuminate\Foundation\Http\FormRequest;

class StoreEquipRequest extends FormRequest
{
    /**
     * Determina si l'usuari està autoritzat a fer aquesta petició.
     *
     * @return bool
     */
    public function authorize(): bool
    {
         return $this->user()->can('create', Equip::class);
    }

    /**
     * Get the validation rules that apply to the request.
     *
     * @return array<string, \Illuminate\Contracts\Validation\ValidationRule|array<mixed>|string>
     */
    public function rules(): array
    {
        return [
            'nom' => 'required|unique:equips',
            'titols' => 'integer|min:0',
            'estadi_id' => 'required|exists:estadis,id',
            'escut' => 'nullable|image|mimes:jpeg,png,jpg|max:2048', // Validació del fitxer
        ];
    }
    
    public function messages()
    {
        return [
            'nom.required' => 'El camp "Nom" és obligatori.',
            'nom.unique' => 'Aquest nom ja està en ús. Si us plau, tria un altre.',
            'titols.integer' => 'El camp "Títols" ha de ser un número enter.',
            'titols.min' => 'El nombre de títols no pot ser inferior a zero.',
            'estadi_id.required' => 'El camp "Estadi" és obligatori.',
            'estadi_id.exists' => 'L\'estadi seleccionat no és vàlid.',
            'escut.image' => 'El camp "Escut" ha de ser una imatge.',
            'escut.mimes' => 'El camp "Escut" només accepta formats: jpeg, png, jpg.',
            'escut.max' => 'La mida de l\'escut no pot superar els 2 MB.',
        ];
    }
}
```

#### 3. Modificar el Controlador per Utilitzar el Form Request

Substitueix la injecció de `Request` pel nou `StoreEquipRequest` al mètode `store` del controlador `EquipController`.

##### Exemple:
```php
use App\Http\Requests\StoreEquipRequest;

public function store(StoreEquipRequest $request)
{
     
    $validated = $request->validated(); // Obté les dades validades

    if ($request->hasFile('escut')) {
        $path = $request->file('escut')->store('escuts', 'public');
        $validated['escut'] = $path;
    }

    Equip::create($validated);

    return redirect()->route('equips.index')->with('success', 'Equip creat correctament!');
}
```

#### 4. Fes el mateix per al Mètode `update`


Defineix les regles al mètode `rules`, incloent l'excepció per al camp únic (en aquest cas, el `nom`):


```php
use App\Http\Requests\StoreEquipRequest;

public function authorize()
{
    $equip = $this->route('equip'); // Obté l'equip de la ruta
    return $this->user()->can('update', $equip);
}

public function rules()
{
    $equipId = $this->route('equip')->id; // Obté l'ID de l'equip actual

    return [
        'nom' => 'required|unique:equips,nom,' . $equipId,
        'titols' => 'integer|min:0',
        'estadi_id' => 'required|exists:estadis,id',
        'escut' => 'nullable|image|mimes:jpeg,png,jpg|max:2048',
    ];
} 
```
## Pas 8. Idiomes al projecte

#### 1. Publicar els Fitxers de Llenguatge

Per defecte, Laravel no inclou el directori `lang`. Per personalitzar els fitxers de llenguatge o crear-ne de nous, executa:

```bash
php artisan lang:publish
```

Aquesta comanda crearà el directori `lang` i publicarà els fitxers de llenguatge predeterminats de Laravel.



#### 2. Configurar l'Idioma Predeterminat

Al fitxer `.env`, ajusta l'opcions `locale` per establir l'idioma predeterminat:

```php
APP_LOCALE=ca
APP_FALLBACK_LOCALE=en
```



#### 3. Definir les Traduccions

Les cadenes de traducció es poden emmagatzemar en fitxers PHP o JSON dins del directori `lang`.

##### Utilitzant Fitxers PHP

Crea subdirectoris per a cada idioma dins de `lang` i afegeix els fitxers de traducció corresponents. Per exemple:

```
/lang
     ca.json
     es.json 
     en.json
```

Cada fitxer ha de retornar un array de cadenes traduïdes:

```json
 {
  "Creació d'Equip": "Creació d'Equip",
  "Guia d'Equips": "Guia d'Equips",
  "Modificació d'Equip": "Modificació d'Equip",
  "Escut actual": "Escut actual",
  "Escut": "Escut",
  "Estadi": "Estadi",
  "Nom": "Nom",
  "Títols": "Títols",
  "Guardar": "Guardar",
  "Actualitzar": "Actualitzar",
  "Esborrar": "Esborrar",
  "Crear Equip": "Crear Equip"  
}
```
```json
{
  "Creació d'Equip": "Creación de Equipo",
  "Guia d'Equips": "Guía de Equipos",
  "Modificació d'Equip": "Modificación de Equipo",
  "Escut actual": "Escudo actual",
  "Escut": "Escudo",
  "Estadi": "Estadio",
  "Nom": "Nombre",
  "Títols": "Títulos",
  "Guardar": "Guardar",
  "Actualitzar": "Actualizar",
  "Esborrar": "Borrar",
  "Crear Equip": "Crear Equipo"
} 
```
```json
{
  "Creació d'Equip": "Team Creation",
  "Guia d'Equips": "Team Guide",
  "Modificació d'Equip": "Team Modification",
  "Escut actual": "Current Shield",
  "Escut": "Shield",
  "Estadi": "Stadium",
  "Nom": "Name",
  "Títols": "Titles",
  "Guardar": "Save",
  "Actualitzar": "Update",
  "Esborrar": "Delete",
  "Crear Equip": "Create Team"
}
```


#### 4. Recuperar Cadenes de Traducció

Utilitza la funció `__` per obtenir les cadenes traduïdes:

```php
 
 @extends('layouts.equips')

@section('title', __("Creació d'Equips"))

@section('content')
    <form action="{{ route('equips.store') }}" method="POST" enctype="multipart/form-data" class="bg-white p-6 rounded-lg shadow-md max-w-md mx-auto">
        @csrf
        <div class="mb-4">
            <label for="nom" class="block text-sm font-medium text-gray-700 mb-1">{{ __('Nom')}}:</label>
            <input type="text" name="nom" id="nom" required
                   class="w-full border-gray-300 rounded-lg shadow-sm focus:ring-blue-500 focus:border-blue-500">
        </div>

        <div class="mb-4">
            <label for="titols" class="block text-sm font-medium text-gray-700 mb-1">{{__('Títols')}}:</label>
            <input type="number" name="titols" id="titols" required
                   class="w-full border-gray-300 rounded-lg shadow-sm focus:ring-blue-500 focus:border-blue-500">
        </div>

        <div class="mb-4">
            <label for="estadi_id" class="block text-sm font-medium text-gray-700 mb-1">{{__('Estadi')}}:</label>
            <select name="estadi_id" id="estadi_id" required
                    class="w-full border-gray-300 rounded-lg shadow-sm focus:ring-blue-500 focus:border-blue-500">
                @foreach ($estadis as $estadi)
                    <option value="{{ $estadi->id }}">{{ $estadi->nom }}</option>
                @endforeach
            </select>
        </div>

        <div class="mb-4">
            <label for="escut" class="block text-sm font-medium text-gray-700 mb-1">{{__('Escut')}}:</label>
            <input type="file" name="escut" id="escut"
                   class="w-full border-gray-300 rounded-lg shadow-sm focus:ring-blue-500 focus:border-blue-500">
        </div>

        <button type="submit"
                class="w-full bg-blue-500 text-white font-medium py-2 px-4 rounded-lg shadow hover:bg-blue-600 focus:ring focus:ring-blue-300">
            {{__('Crear Equip')}}
        </button>
    </form>
@endsection

```

#### 5. Canviar l'Idioma Dinàmicament

Per canviar l'idioma durant l'execució, utilitza el mètode `setLocale`:

```php
App::setLocale('es');
```

Per facilitar als usuaris la selecció de l'idioma, pots crear rutes o enllaços que estableixin l'idioma desitjat.

---

#### 7. Traduir Missatges de Validació

Els missatges de validació es poden personalitzar als fitxers de llenguatge corresponents. Per exemple, al fitxer `resources/lang/ca/validation.php`:

```php
<?php

return [
    /*
    |--------------------------------------------------------------------------
    | Missatges de validació
    |--------------------------------------------------------------------------
    |
    | Les següents línies contenen els missatges d'error per a les diferents
    | regles de validació. Pots ajustar aquests missatges segons les
    | necessitats de la teva aplicació.
    |
    */

    'accepted' => 'El camp :attribute ha de ser acceptat.',
    'active_url' => 'El camp :attribute no és una URL vàlida.',
    'after' => 'El camp :attribute ha de ser una data posterior a :date.',
    'after_or_equal' => 'El camp :attribute ha de ser una data igual o posterior a :date.',
    'alpha' => 'El camp :attribute només pot contenir lletres.',
    'alpha_dash' => 'El camp :attribute només pot contenir lletres, números, guions i guions baixos.',
    'alpha_num' => 'El camp :attribute només pot contenir lletres i números.',
    'array' => 'El camp :attribute ha de ser un array.',
    'before' => 'El camp :attribute ha de ser una data anterior a :date.',
    'before_or_equal' => 'El camp :attribute ha de ser una data igual o anterior a :date.',
    'between' => [
        'numeric' => 'El camp :attribute ha d\'estar entre :min i :max.',
        'file' => 'El camp :attribute ha de tenir entre :min i :max kilobytes.',
        'string' => 'El camp :attribute ha de tenir entre :min i :max caràcters.',
        'array' => 'El camp :attribute ha de tenir entre :min i :max elements.',
    ],
    'boolean' => 'El camp :attribute ha de ser verdader o fals.',
    'confirmed' => 'La confirmació del camp :attribute no coincideix.',
    'date' => 'El camp :attribute no és una data vàlida.',
    'date_format' => 'El camp :attribute no coincideix amb el format :format.',
    'different' => 'Els camps :attribute i :other han de ser diferents.',
    'digits' => 'El camp :attribute ha de tenir :digits dígits.',
    'digits_between' => 'El camp :attribute ha de tenir entre :min i :max dígits.',
    'dimensions' => 'El camp :attribute té dimensions d\'imatge no vàlides.',
    'distinct' => 'El camp :attribute té un valor duplicat.',
    'email' => 'El camp :attribute ha de ser una adreça de correu electrònic vàlida.',
    'exists' => 'El camp :attribute seleccionat no és vàlid.',
    'file' => 'El camp :attribute ha de ser un fitxer.',
    'filled' => 'El camp :attribute ha de tenir un valor.',
    'gt' => [
        'numeric' => 'El camp :attribute ha de ser més gran que :value.',
        'file' => 'El camp :attribute ha de tenir més de :value kilobytes.',
        'string' => 'El camp :attribute ha de tenir més de :value caràcters.',
        'array' => 'El camp :attribute ha de tenir més de :value elements.',
    ],
    'gte' => [
        'numeric' => 'El camp :attribute ha de ser més gran o igual a :value.',
        'file' => 'El camp :attribute ha de tenir com a mínim :value kilobytes.',
        'string' => 'El camp :attribute ha de tenir com a mínim :value caràcters.',
        'array' => 'El camp :attribute ha de tenir com a mínim :value elements.',
    ],
    'image' => 'El camp :attribute ha de ser una imatge.',
    'in' => 'El camp :attribute seleccionat no és vàlid.',
    'in_array' => 'El camp :attribute no existeix a :other.',
    'integer' => 'El camp :attribute ha de ser un nombre enter.',
    'ip' => 'El camp :attribute ha de ser una adreça IP vàlida.',
    'ipv4' => 'El camp :attribute ha de ser una adreça IPv4 vàlida.',
    'ipv6' => 'El camp :attribute ha de ser una adreça IPv6 vàlida.',
    'json' => 'El camp :attribute ha de ser una cadena JSON vàlida.',
    'lt' => [
        'numeric' => 'El camp :attribute ha de ser més petit que :value.',
        'file' => 'El camp :attribute ha de tenir menys de :value kilobytes.',
        'string' => 'El camp :attribute ha de tenir menys de :value caràcters.',
        'array' => 'El camp :attribute ha de tenir menys de :value elements.',
    ],
    'lte' => [
        'numeric' => 'El camp :attribute ha de ser més petit o igual a :value.',
        'file' => 'El camp :attribute ha de tenir com a màxim :value kilobytes.',
        'string' => 'El camp :attribute ha de tenir com a màxim :value caràcters.',
        'array' => 'El camp :attribute no ha de tenir més de :value elements.',
    ],
    'max' => [
        'numeric' => 'El camp :attribute no pot ser més gran que :max.',
        'file' => 'El camp :attribute no pot tenir més de :max kilobytes.',
        'string' => 'El camp :attribute no pot tenir més de :max caràcters.',
        'array' => 'El camp :attribute no pot tenir més de :max elements.',
    ],
    'mimes' => 'El camp :attribute ha de ser un fitxer de tipus: :values.',
    'mimetypes' => 'El camp :attribute ha de ser un fitxer de tipus: :values.',
    'min' => [
        'numeric' => 'El camp :attribute ha de ser com a mínim :min.',
        'file' => 'El camp :attribute ha de tenir com a mínim :min kilobytes.',
        'string' => 'El camp :attribute ha de tenir com a mínim :min caràcters.',
        'array' => 'El camp :attribute ha de tenir com a mínim :min elements.',
    ],
    'not_in' => 'El camp :attribute seleccionat no és vàlid.',
    'not_regex' => 'El format del camp :attribute no és vàlid.',
    'numeric' => 'El camp :attribute ha de ser un nombre.',
    'present' => 'El camp :attribute ha de ser present.',
    'regex' => 'El format del camp :attribute no és vàlid.',
    'required' => 'El camp :attribute és obligatori.',
    'required_if' => 'El camp :attribute és obligatori quan :other és :value.',
    'required_unless' => 'El camp :attribute és obligatori excepte si :other és a :values.',
    'required_with' => 'El camp :attribute és obligatori quan :values és present.',
    'required_with_all' => 'El camp :attribute és obligatori quan :values són presents.',
    'required_without' => 'El camp :attribute és obligatori quan :values no és present.',
    'required_without_all' => 'El camp :attribute és obligatori quan cap de :values són presents.',
    'same' => 'Els camps :attribute i :other han de coincidir.',
    'size' => [
        'numeric' => 'El camp :attribute ha de tenir la mida :size.',
        'file' => 'El camp :attribute ha de tenir :size kilobytes.',
        'string' => 'El camp :attribute ha de tenir :size caràcters.',
        'array' => 'El camp :attribute ha de contenir :size elements.',
    ],
    'starts_with' => 'El camp :attribute ha de començar amb un dels valors següents: :values.',
    'string' => 'El camp :attribute ha de ser una cadena de text.',
    'timezone' => 'El camp :attribute ha de ser una zona horària vàlida.',
    'unique' => 'El camp :attribute ja està en ús.',
    'uploaded' => 'El camp :attribute ha fallat en pujar.',
    'url' => 'El format del camp :attribute no és vàlid.',
    'uuid' => 'El camp :attribute ha de ser un identificador UUID vàlid.',

    /*
    |--------------------------------------------------------------------------
    | Missatges personalitzats per a atributs
    |--------------------------------------------------------------------------
    |
    | Pots utilitzar aquesta secció per personalitzar els noms dels atributs.
    |
    */

    'attributes' => [],
];

```

Això assegura que els missatges de validació es mostren en l'idioma seleccionat.

### Pas 9. Crear proves

1. Crea un fitxer de proves per al CRUD d'equips:
```bash
php artisan make:test EquipCRUDTest
```

2. Modifica el fitxer de proves `tests/Feature/EquipCRUDTest.php`:
```php
namespace Tests\Feature;

use App\Models\Estadi;
use Illuminate\Foundation\Testing\RefreshDatabase;
use Tests\TestCase;
use App\Models\Equip;

class EquipCrudTest extends TestCase
{
    use RefreshDatabase;

    /** @test */
    public function es_pot_crear_un_equip_correctament()
    {
        // Actuar: Crear un equip
        $estadi = Estadi::create([
            'nom' => 'Camp Nou',
            'ciutat' => 'Barcelona',
            'capacitat' => 99354,
        ]);
        $equip = Equip::create([
            'nom' => 'FC Barcelona',
             'titols' =>30,
             'estadi_id' => 1,
        ]);

        // Comprovar que l’equip es guarda a la base de dades
        $this->assertDatabaseHas('equips', [
            'nom' => 'FC Barcelona',
            'titols' => 30,
            'estadi_id' => 1,
        ]);
    }

    public function es_poden_llistar_els_equips()
    {
        // Arrange: Crear equips
        Equip::factory()->create(['nom' => 'FC Barcelona']);
        Equip::factory()->create(['nom' => 'Real Madrid']);

        // Actuar: Obtenir la llista d’equips
        $equips = Equip::all();

        // Comprovar que la llista conté els equips creats
        $this->assertCount(2, $equips);
        $this->assertEquals('FC Barcelona', $equips[0]->nom);
        $this->assertEquals('Real Madrid', $equips[1]->nom);
    }

    public function es_pot_actualitzar_un_equip()
    {
        // Arrange: Crear un equip
        $equip = Equip::create([
            'nom' => 'FC Barcelona',
            'ciutat' => 'Barcelona',
        ]);

        // Actuar: Actualitzar l’equip
        $equip->update([
            'nom' => 'Barça',
            'ciutat' => 'Catalunya',
        ]);

        // Comprovar que els canvis es reflecteixen a la base de dades
        $this->assertDatabaseHas('equips', [
            'nom' => 'Barça',
            'ciutat' => 'Catalunya',
        ]);
    }

    public function es_pot_esborrar_un_equip()
    {
        // Arrange: Crear un equip
        $equip = Equip::create([
            'nom' => 'FC Barcelona',
            'ciutat' => 'Barcelona',
        ]);

        // Actuar: Esborrar l’equip
        $equip->delete();

        // Comprovar que l’equip ja no existeix a la base de dades
        $this->assertDatabaseMissing('equips', [
            'nom' => 'FC Barcelona',
            'ciutat' => 'Barcelona',
        ]);
    }

    public function no_es_pot_crear_un_equip_sense_nom()
    {
        $this->expectException(\Illuminate\Database\QueryException::class);

        // Intentar crear un equip sense nom
        Equip::create([
            'ciutat' => 'Barcelona',
        ]);
    }
}
```
3. Copia el .env en .env.testing i modifica'l per a executar les proves en una BBDD de testing

```bash
DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=testing
DB_USERNAME=sail
DB_PASSWORD=password
```

4. Executa les proves:
```bash
php artisan test
```

### Pas 10. Generar un correu electrònic amb la jornada actual (partits programats) i enviar-lo als managers dels equips.

#### **1. Crear una Comanda Artisan**
```bash
php artisan make:command EnviarJornadaManagers
```

Al fitxer `app/Console/Commands/EnviarJornadaManagers.php`:

```php
namespace App\Console\Commands;

use App\Models\User;
use Carbon\Carbon;
use Illuminate\Console\Command;
use Illuminate\Support\Facades\Mail;
use App\Models\Partit;
use App\Mail\JornadaMail;

class EnviarJornadaManagers extends Command
{
    protected $signature = 'jornada:enviar';
    protected $description = 'Envia la jornada actual als managers';

    public function handle()
    {
        $partit = Partit::whereDate('data', '>', Carbon::now()) // Filtra partits posteriors a avui
            ->orderBy('data', 'asc') // Ordena per la data més propera
            ->first();
        $partits = Partit::with(['equipLocal', 'equipVisitant'])->where('jornada',$partit->jornada)->get();

        // Lògica per obtenir els correus dels managers
        $managers = User::where('role','manager')->get();


        foreach ($managers as $manager) {
            Mail::to($manager->email)->send(new JornadaMail($partits));
            $this->info($manager->name . ' ha rebut la jornada.');

        }

        $this->info('La jornada s\'ha enviat correctament als managers.');
    }
}
 
#### **2. Crear el Mail**
```bash
php artisan make:mail JornadaMail --markdown=emails.jornada
```

Al fitxer `app/Mail/JornadaMail.php`:

```php
namespace App\Mail;

use Illuminate\Bus\Queueable;
use Illuminate\Contracts\Queue\ShouldQueue;
use Illuminate\Mail\Mailable;
use Illuminate\Mail\Mailables\Content;
use Illuminate\Queue\SerializesModels;

class JornadaMail extends Mailable
{
    use Queueable, SerializesModels;

    public $partits;

    public function __construct($partits)
    {
        $this->partits = $partits;
    }



    public function content(): Content
    {
        return new Content(
            markdown: 'emails.jornada',
            with: [
                'partits' => $this->partits,
            ],
        );
    }
}

```


#### **3. Crear la Vista del Correu**
Al fitxer `resources/views/emails/jornada.blade.php`:

```markdown
<x-mail::message>
    # Jornada {{ $partits->first()->jornada }}

    ## Partits Programats:
    @foreach($partits as $partit)
        - **{{ $partit->equipLocal->nom }}** vs **{{ $partit->equipVisitant->nom }}** ({{ $partit->data }})
    @endforeach

    Gràcies,
    **{{ config('app.name') }}**
</x-mail::message>
```

#### **4. Efectuar l'Enviament**
Pots enviar els correus manualment executant la comanda:

```bash
php artisan jornada:enviar
``` 

Pots programar la comanda al `Kernel.php`:

```php
protected function schedule(Schedule $schedule)
{
    $schedule->command('jornada:enviar')->weeklyOn(1, '8:00');
}
```


### Pas 11. Crear un component livewire per a mostrar un històric de partits

1. Instal·la Livewire:
```bash
composer require livewire/livewire
php artisan livewire:publish
```

2. Afegeix els scripts de Livewire a la plantilla Blade:

```html
<!DOCTYPE html>
<html lang="{{ str_replace('_', '-', app()->getLocale()) }}">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta name="csrf-token" content="{{ csrf_token() }}">

    <title>{{ config('app.name', 'Laravel') }}</title>

    <!-- Fonts -->
    <link rel="preconnect" href="https://fonts.bunny.net">
    <link href="https://fonts.bunny.net/css?family=figtree:400,500,600&display=swap" rel="stylesheet" />

    <!-- Scripts -->
    @vite(['resources/css/app.css', 'resources/js/app.js'])
    @livewireStyles
</head>
<body class="font-sans antialiased">
<div class="min-h-screen bg-gray-100 dark:bg-gray-900">
    @include('layouts.navigation')

    <!-- Page Heading -->
    @isset($header)
    <header class="bg-white dark:bg-gray-800 shadow">
        <div class="max-w-7xl mx-auto py-6 px-4 sm:px-6 lg:px-8">
            {{ $header }}
        </div>
    </header>
    @endisset

    <!-- Page Content -->
    <main>
        {{ $slot }}
    </main>
</div>
@livewireScripts
</body>
</html>
```
3. Genera el component Livewire:
```bash
 php artisan make:livewire HistorialPartits
```

4. Modifica el component Livewire `app/Livewire/HistorialPartits.php`:
```php
namespace App\Livewire;

use App\Models\Partit;
use Livewire\Component;

class HistorialPartits extends Component
{
    public $partits;
    public $equip = '';
    public $data = '';

    public function mount()
    {
        $this->partits = Partit::with(['equipLocal', 'equipVisitant', 'estadi', 'arbitre'])->get();
    }


    public function filtrar()
    {
        $this->partits = Partit::with(['equipLocal', 'equipVisitant', 'estadi', 'arbitre'])
            ->when($this->equip, function ($query) {
                $query->whereHas('equipLocal', fn($q) => $q->where('nom', 'like', "%{$this->equip}%"))
                    ->orWhereHas('equipVisitant', fn($q) => $q->where('nom', 'like', "%{$this->equip}%"));
            })
            ->when($this->data, function ($query) {
                $query->whereDate('data', $this->data);
            })
            ->get();
    }

    public function render()
    {
        return view('livewire.historial-partits', ['partits' => $this->partits]);
    }
}
```
5. Modifica la vista del component Livewire `resources/views/livewire/historial-partits.blade.php`:
```php
<div>
    <div class="flex space-x-4">
        <input wire:model="equip" type="text" placeholder="Cerca equip" class="border px-4 py-2">
        <input wire:model="data" type="date" class="border px-4 py-2">
        <button wire:click="filtrar" class="bg-blue-500 text-white px-4 py-2">Filtrar</button>
    </div>

    <table class="table-auto w-full mt-4">
        <thead>
        <tr>
            <th>Data</th>
            <th>Equip Local</th>
            <th>Equip Visitant</th>
            <th>Resultat</th>
            <th>Estadi</th>
            <th>Àrbitre</th>
        </tr>
        </thead>
        <tbody>
        @foreach($partits as $partit)
            <tr>
                <td>{{ $partit->data }}</td>
                <td>{{ $partit->equipLocal->nom }}</td>
                <td>{{ $partit->equipVisitant->nom }}</td>
                <td>{{ $partit->resultat }}</td>
                <td>{{ $partit->estadi->nom }}</td>
                <td>{{ $partit->arbitre->name }}</td>
            </tr>
        @endforeach
        </tbody>
    </table>
</div>
```
6. Crea la vista `resources/views/partits/historic.blade.php`:
```php
@extends('layouts.futbolFemeni')

@section('title', __('Històric de partits' ))

@section('content')

    <!-- Afegim el component Livewire aquí -->
    <div class="mt-8">
        @livewire('historial-partits')
    </div>
@endsection
```
7. Modifica la ruta `routes/web.php`:
```php
Route::get('/historic', [PartitController::class, 'historic'])->name('partits.historic');

```
8. Modifica el controlador `app/Http/Controllers/PartitController.php`:
```php
public function historic()
{
    return view('partits.historic');
}
```
9. Afegix entrada en el menú `resources/views/layouts/navigation.blade.php`:
```php
<div class="hidden space-x-8 sm:-my-px sm:ms-10 sm:flex">
    <x-nav-link :href="route('partits.historic')" :active="request()->routeIs('partits.historic')">
        {{ __('Històric Partits') }}
    </x-nav-link>
</div>
```



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

