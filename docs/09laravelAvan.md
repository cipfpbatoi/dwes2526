# Laravel Avançat

## Autenticació i Autorització amb Laravel

### 1. Autenticació

#### 1.1 Configuració inicial
Laravel ofereix dos paquets principals per implementar l’autenticació:
1. **Laravel Breeze**: Simple i lleuger, ideal per a projectes educatius i senzills.
2. **Laravel Jetstream**: Robust i complet, inclou funcionalitats avançades com equips, autenticació de dos factors i gestió d'API.

**Instal·lació de Laravel Breeze**
```bash
composer require laravel/breeze --dev
php artisan breeze:install
npm install && npm run dev
php artisan migrate
```

Aquestes ordres configuren:
- Rutes per login, registre, restabliment de contrasenya, etc.
- Plantilles Blade predefinides amb Tailwind CSS.

#### 1.2 Recuperació de l'usuari autenticat
Un cop l'usuari ha fet login, podem accedir a les seues dades:
```php
use Illuminate\Support\Facades\Auth;

// Usuari autenticat
$user = Auth::user();

// ID de l'usuari autenticat
$id = Auth::id();
```

També podem obtenir l’usuari des d'una petició injectada al controlador:
```php
public function dashboard(Request $request)
{
    $user = $request->user(); // Equivalent a Auth::user()
}
```

#### 1.3 Protegir rutes amb middleware
El middleware `auth` assegura que només els usuaris autenticats poden accedir a una ruta:
```php
Route::get('/dashboard', function () {
    return view('dashboard');
})->middleware('auth');
```

#### 1.4 Logout
Laravel Breeze inclou logout preconfigurat:
```php
<form method="POST" action="{{ route('logout') }}">
    @csrf
    <button type="submit">Logout</button>
</form>
```

#### 1.5 Restabliment de contrasenya
Per habilitar el restabliment de contrasenya:

1. Configura el correu SMTP al fitxer `.env`.
2. Laravel Breeze genera automàticament els formularis i la lògica necessària.

 
### 2. Autorització

#### 2.1 Rols i permisos
**Afegir un camp `role` a la taula `users`**  
Per implementar rols:
1. Crear una migració:
   ```bash
   php artisan make:migration add_role_to_users_table --table=users
   ```
2. Afegir el camp `role`:
   ```php
   Schema::table('users', function (Blueprint $table) {
       $table->string('role')->default('user'); // Opcions: 'user', 'admin', etc.
   });
   ```
3. Actualitzar el model `User`:
   ```php
   class User extends Authenticatable
   {
       protected $fillable = ['name', 'email', 'password', 'role'];
   }
   ```

**Middleware per a rols**
1. Crear un middleware:
   ```bash
   php artisan make:middleware RoleMiddleware
   ```
2. Definir el rol al middleware:
   ```php
   public function handle($request, Closure $next, $role)
   {
       if (Auth::check() && Auth::user()->role === $role) {
           return $next($request);
       }
       return redirect('/');
   }
   ```
3. Registrar-lo a `Kernel.php`:
   ```php
   protected $routeMiddleware = [
       'role' => \App\Http\Middleware\RoleMiddleware::class,
   ];
   ```
4. Aplicar-lo a una ruta:
   ```php
   Route::get('/admin', function () {
       return view('admin.dashboard');
   })->middleware('role:admin');
   ```


#### Què és un Middleware?

Un **middleware** és una classe que actua com a intermediari entre una sol·licitud HTTP i la seua resposta. En Laravel, els middleware s'utilitzen per executar codi abans o després que una sol·licitud arribe al controlador, permetent així gestionar tasques com:
- Autenticació d'usuaris.
- Validació de permisos o rols.
- Filtratge de dades de la petició.
- Modificació de respostes.

Els middleware són ideals per encapsular lògica comuna que cal aplicar a diverses rutes, com per exemple assegurar que només usuaris autenticats poden accedir a certes àrees de l'aplicació.

Exemple d'ús:
```php
public function handle($request, Closure $next)
{
    if (Auth::check()) {
        return $next($request); // Continua amb la sol·licitud
    }
    return redirect('login'); // Redirigeix si no està autenticat
}
```

Els middleware es registren al fitxer `Kernel.php`, i poden aplicar-se a rutes específiques o a tot l'aplicatiu.

#### 2.2 Policies per a accés granular

**Creació d'una Policy**  

Les policies permeten definir regles d'autorització específiques:

```bash
php artisan make:policy PostPolicy --model=Post
```

Exemple per permetre que un usuari només puga editar els seus posts:
```php
public function update(User $user, Post $post)
{
    return $user->id === $post->user_id;
}
```
Registrar la política a `AuthServiceProvider`:
```php
protected $policies = [
    Post::class => PostPolicy::class,
];
```

Ús de la política en un controlador:
```php
public function edit(Post $post)
{
    $this->authorize('update', $post);
    return view('posts.edit', compact('post'));
}
```

### 3.Utilitzar Form Requests per a Validacions més Complexes

Els **Form Requests** són classes dedicades que encapsulen la lògica de validació d'una sol·licitud HTTP. Aquestes classes permeten organitzar millor el codi, especialment en formularis amb moltes regles de validació.

#### 1. Crear un Form Request
Per crear un **Form Request**, utilitzem l'eina Artisan:
```bash
php artisan make:request MoviePost
```
Això genera una nova classe a la carpeta `app/Http/Requests`. Aquesta classe conté dos mètodes principals:

1. **authorize()**  
   Retorna `true` o `false` segons si l'usuari està autoritzat a fer la sol·licitud. Per defecte, podem retornar `true` per permetre totes les sol·licituds:
    ```php
    public function authorize()
    {
        return true;
    }
    ```

2. **rules()**  
   Retorna un array amb les regles de validació:
    ```php
    public function rules()
    {
        return [
            'title' => 'required|min:3',
            'director' => 'required',
            'year' => 'required|numeric|min:1900',
        ];
    }
    ```

#### 2. Utilitzar el Form Request en un Controlador
En lloc d'especificar les regles de validació directament al controlador, podem injectar el **Form Request** al mètode del controlador:
```php
public function store(MoviePost $request)
{
    // Si arribem aquí, les dades són vàlides.
    // Accedim a les dades validades:
    $validated = $request->validated();

    // Crear una nova pel·lícula
    $movie = new Movie($validated);
    $movie->save();

    return redirect()->route('movies.index');
}
```
El mètode `validated()` retorna només les dades que han passat les regles de validació.

#### 3. Personalitzar Missatges d'Error
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

#### 4. Mostrar Errors de Validació a la Vista
Quan es produeixen errors de validació, Laravel redirigeix automàticament a la vista anterior amb la variable global `$errors`, que conté els errors de validació.

Exemple de com mostrar un llistat d'errors al començament del formulari:
```php
@if ($errors->any())
    <ul>
        @foreach($errors->all() as $error)
            <li>{{ $error }}</li>
        @endforeach
    </ul>
@endif
```

Per mostrar errors específics sota un camp:
```php
<div class="form-group">
    <label for="title">Títol:</label>
    <input type="text" name="title" id="title" class="form-control" value="{{ old('title') }}">
    @if ($errors->has('title'))
        <div class="text-danger">{{ $errors->first('title') }}</div>
    @endif
</div>
```


## Ús d'idiomes en Laravel

Laravel proporciona eines senzilles i potents per a la **localització d'aplicacions**, permetent suportar múltiples idiomes. Aquesta funcionalitat és ideal per a desenvolupar aplicacions accessibles a usuaris de diferents regions i llengües.
 
### 1. Configuració Inicial

#### 1.1 Idioma Predeterminat
L'idioma predeterminat s'estableix al fitxer `config/app.php` mitjançant el paràmetre `locale`:
```php
'locale' => 'en', // Idioma predeterminat
```

#### 1.2 Idioma Alternatiu
Es pot definir un idioma "alternatiu" que s'utilitzarà quan no es troben traduccions en l'idioma actiu:
```php
'fallback_locale' => 'en', // Idioma alternatiu
```
 
### 2. Treballant amb Fitxers de Traducció

#### 2.1 Organització dels Fitxers
Els fitxers de traducció es guarden al directori `lang`. Cada idioma té la seua pròpia carpeta, amb fitxers `.php` que contenen arrays clau-valor per a les traduccions:

**Exemple d'estructura:**
```
/lang
    /en
        messages.php
    /es
        messages.php
```

#### 2.2 Crear un Fitxer de Traducció
Un fitxer de traducció típic conté un array de cadenes:
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

### 3. Ús de Traduccions en el Codi

#### 3.1 Recuperar Traduccions
Utilitza la funció auxiliar `__()` per obtenir les traduccions:
```php
echo __('messages.welcome'); // Welcome to our application!
```

Si la traducció no existeix, es retorna la clau proporcionada:
```php
echo __('messages.unknown'); // messages.unknown
```

#### 3.2 Traduccions amb Paràmetres
És possible definir paràmetres dins de les traduccions utilitzant el símbol `:`, que es substitueix quan es crida a la funció:
```php
// lang/en/messages.php
return [
    'greeting' => 'Hello, :name!',
];
```
```php
echo __('messages.greeting', ['name' => 'John']); // Hello, John!
```

---

### 4. Localització en Temps d'Execució

#### 4.1 Canviar l'Idioma Actiu
Per canviar l'idioma de l'aplicació en temps d'execució, utilitza el mètode `App::setLocale()`:
```php
use Illuminate\Support\Facades\App;

App::setLocale('es'); // Canvia a espanyol
```

Aquesta configuració només afecta la petició actual.
 

### 5. Traduccions amb Fitxers JSON

Laravel permet utilitzar fitxers JSON per a traduccions simples. Aquest enfocament és útil per a aplicacions amb cadenes de traducció úniques i desordenades.

**Exemple de Fitxer JSON:**
```json
// lang/es.json
{
    "I love programming.": "Me encanta programar."
}
```

Per accedir a aquestes cadenes:
```php
echo __('I love programming.');
```

## Enviament de Correus en Laravel

Laravel ofereix una API senzilla i flexible per gestionar l'enviament de correus electrònics. Aquesta funcionalitat és útil per a notificacions, restabliment de contrasenyes i altres comunicacions amb els usuaris.

---

### 1. Configuració Inicial

#### 1.1 Configurar el Servei de Correu
Laravel suporta múltiples serveis d'enviament de correu com SMTP, Mailgun, Postmark, Amazon SES, entre altres. La configuració es defineix al fitxer `.env`:

**Exemple de configuració SMTP per Gmail:**
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

#### 1.2 Configurar el Fitxer `config/mail.php`
Aquest fitxer conté la configuració global per al sistema de correu. Normalment, no és necessari modificar-lo si es configura correctament el `.env`.

---

### 2. Crear Correus
 
#### 2.1 Crear una Classe de Correu
Les classes de correu es generen amb Artisan:
```bash
php artisan make:mail WelcomeMail
```

Aquest comandament crea una classe al directori `App\Mail`. Aquesta classe és on es defineix el contingut i el disseny del correu.

#### 2.2 Exemple d'una Classe de Correu
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
 
### 3. Enviar Correus

#### 3.1 Enviar un Correu des d'un Controlador
Utilitza la façana `Mail` per enviar correus:
```php
use App\Mail\WelcomeMail;
use Illuminate\Support\Facades\Mail;

Mail::to('usuari@example.com')->send(new WelcomeMail($user));
```

#### 3.2 Enviar a Múltiples Receptors
Laravel permet enviar correus a múltiples destinataris:
```php
Mail::to(['user1@example.com', 'user2@example.com'])->send(new WelcomeMail($user));
```
 
### 4. Plantilles de Correus

#### 4.1 Crear una Vista per al Correu
Les vistes per a correus es guarden al directori `resources/views/emails`. Exemple de plantilla Blade:
```html
<!DOCTYPE html>
<html>
<head>
    <title>Benvingut</title>
</head>
<body>
    <h1>Hola, {{ $user->name }}</h1>
    <p>Gràcies per registrar-te a la nostra aplicació!</p>
</body>
</html>
```

#### 4.2 Utilitzar Components i Markdown
Laravel permet crear correus amb components de Markdown. Generem un correu amb components:
```bash
php artisan make:mail WelcomeMail --markdown=emails.welcome
```

Aquest comandament crea una plantilla Markdown a `resources/views/emails`.

Exemple de plantilla Markdown:
```markdown
# Benvingut, {{ $user->name }}

Gràcies per unir-te a la nostra aplicació.

@component('mail::button', ['url' => 'https://example.com'])
Visita el nostre lloc web
@endcomponent

Gràcies,<br>
{{ config('app.name') }}
```
 
### 5. Correu en Cua

Per enviar correus de manera asíncrona i millorar el rendiment de l'aplicació, podem utilitzar cues:
```php
Mail::to('usuari@example.com')->queue(new WelcomeMail($user));
```

Assegura't que el sistema de cues estiga configurat al fitxer `.env`:
```env
QUEUE_CONNECTION=database
```

## Sistema de Fitxers en Laravel

Laravel proporciona una API unificada per treballar amb diferents sistemes de fitxers com el sistema local, Amazon S3, FTP, i altres. Aquesta funcionalitat permet gestionar l'emmagatzematge de fitxers d'una manera senzilla i flexible.
 
### 1. Configuració Inicial

#### 1.1 Configurar els Discs d'Emmagatzematge
Els discos d'emmagatzematge es defineixen al fitxer `config/filesystems.php`. Per defecte, Laravel inclou els següents discos:
- **local**: Emmagatzematge en el sistema local.
- **public**: Per fitxers públics accessibles des d'un navegador.
- **s3**: Per emmagatzematge a Amazon S3.

#### 1.2 Configuració del `.env`
Exemple de configuració:
```env
FILESYSTEM_DISK=local
AWS_ACCESS_KEY_ID=el_teu_access_key
AWS_SECRET_ACCESS_KEY=el_teu_secret_key
AWS_DEFAULT_REGION=us-east-1
AWS_BUCKET=el_teu_bucket
```
 
### 2. Treballar amb el Sistema de Fitxers

#### 2.1 Accedir a un Disc
Utilitza la façana `Storage` per accedir al sistema de fitxers:
```php
use Illuminate\Support\Facades\Storage;

$disk = Storage::disk('local'); // Accedir al disc local
```

Si no especifiques cap disc, Laravel utilitza el disc predeterminat (`FILESYSTEM_DISK` al `.env`).

 
### 3. Operacions Bàsiques amb Fitxers

#### 3.1 Guardar Fitxers
```php
use Illuminate\Support\Facades\Storage;

// Guardar un fitxer amb contingut
Storage::put('documents/file.txt', 'Contingut del fitxer');

// Guardar un fitxer pujat
$file = $request->file('document');
Storage::putFile('uploads', $file);

// Guardar amb un nom personalitzat
Storage::putFileAs('uploads', $file, 'custom_name.txt');
```

#### 3.2 Obtenir Fitxers
```php
// Obtenir el contingut d'un fitxer
$content = Storage::get('documents/file.txt');

// Verificar si un fitxer existeix
if (Storage::exists('documents/file.txt')) {
    // Fitxer existeix
}
```

#### 3.3 Eliminar Fitxers
```php
// Eliminar un fitxer
Storage::delete('documents/file.txt');

// Eliminar múltiples fitxers
Storage::delete(['file1.txt', 'file2.txt']);
```

#### 3.4 Llistar Fitxers
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
 
### 4. Fitxers Públics

#### 4.1 Publicar Fitxers
Per fer fitxers accessibles públicament, utilitza el disc `public`. Assegura't de crear un enllaç simbòlic per al directori `storage/app/public` al directori `public/storage`:
```bash
php artisan storage:link
```

#### 4.2 Obtenir una URL Pública
```php
$url = Storage::url('documents/file.txt'); // Genera una URL pública
```
 

### 5. Treballar amb Amazon S3

#### 5.1 Configuració
Inclou les credencials d'Amazon S3 al fitxer `.env`:
```env
AWS_ACCESS_KEY_ID=el_teu_access_key
AWS_SECRET_ACCESS_KEY=el_teu_secret_key
AWS_DEFAULT_REGION=us-east-1
AWS_BUCKET=el_teu_bucket
```

#### 5.2 Exemple
```php
use Illuminate\Support\Facades\Storage;

// Guardar un fitxer a S3
Storage::disk('s3')->put('documents/file.txt', 'Contingut');

// Obtenir una URL
$url = Storage::disk('s3')->url('documents/file.txt');
```
 
