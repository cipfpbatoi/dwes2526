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
1. Configura el correu SMTP al fitxer `.env`:
   ```env
   MAIL_MAILER=smtp
   MAIL_HOST=smtp.gmail.com
   MAIL_PORT=587
   MAIL_USERNAME=el_teu_email@gmail.com
   MAIL_PASSWORD=la_teua_contrasenya
   MAIL_ENCRYPTION=tls
   MAIL_FROM_ADDRESS=el_teu_email@gmail.com
   MAIL_FROM_NAME="Nom del projecte"
   ```
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
 
