º<html>
<head>
  <title>@yield('title', config('app.name'))</title>
  @vite(['resources/css/app.css','resources/js/app.js'])
</head>
<body>
  @include('partials.nav')
  <main>@yield('content')</main>
</body>
</html>
Vista que hereta:
@extends('layouts.app')
@section('title','Inici')
@section('content')
  <h1>Benvingut/da!</h1>
@endsection
5.5 Components Blade
php artisan make:component Alert
Ús:
<x-alert type="success">Missatge enviat!</x-alert>
6) Controladors (organitzar la lògica)
6.1 Crea# Arquitectura MVC amb Laravel

??? abstract "Duració i criteris d'evaluació"

    Duració estimada: 16 hores

    <hr />

    | Resultat d'aprenentatge  | Criteris d'avaluació  |
    | ------                    | -----                |
    | 5. Desenvolupa aplicacions Web identificant i aplicant mecanismes per a separar el codi de presentació de la lògica de negoci. | a) S'han identificat els avantatges de separar la lògica de negoci dels aspectes de presentació de l'aplicació. b) S'han analitzat i utilitzat mecanismes i frameworks que permeten realitzar aquesta separació i les seues característiques principals. c) S'han utilitzat objectes i controls en el servidor per a generar l'aspecte visual de l'aplicació web en el client. d) S'han utilitzat formularis generats de manera dinàmica per a respondre als esdeveniments de l'aplicació web. e) S'han identificat i aplicat els paràmetres relatius a la configuració de l'aplicació web. f) S'han escrit aplicacions web amb manteniment d'estat i separació de la lògica de negoci. g) S'han aplicat els principis i patrons de disseny de la programació orientada a objectes. h) S'ha provat i documentat el codi. |

## SA 3.1 MVC i instal·lació de Laravel

###  🧩 Avantatges de la separació de capes

#### 🔍 Què és la separació de responsabilitats?
En el desenvolupament d’aplicacions web, separar la **lògica de negoci** (com es processen les dades) de la **presentació** (com es mostren) és essencial per crear projectes escalables i fàcils de mantindre.

#### Problemes quan no hi ha separació
- Codi desordenat i difícil de llegir.
- Modificar la interfície pot trencar la lògica i viceversa.
- Dificultat per treballar en equip.

#### Beneficis

| Avantatge        | Descripció                                                                 |
|------------------|-----------------------------------------------------------------------------|
| Mantenibilitat   | És més fàcil modificar el codi, ja que cada part està separada.             |
| Reutilització    | El codi es pot reutilitzar en diferents parts del projecte.                 |
| Escalabilitat    | És més senzill afegir noves funcionalitats sense trencar les existents.     |
| Treball en equip | Permet dividir tasques entre programadors backend i frontend.              |
| Testabilitat     | Podem fer proves unitàries de la lògica sense necessitat de la interfície.  |
| Seguretat        | Mantindre la lògica separada ajuda a controlar millor les entrades i sortides. |


#### Comparació
- **Aplicació monolítica**: tot el codi barrejat (HTML, SQL, lògica PHP).
- **MVC**: cada capa té la seua responsabilitat i només interactua amb les necessàries.

#### 💡 Exemple senzill

Sense separació:

```php
<?php
// Exemple dolent: lògica i presentació mesclades
$conn = new PDO('mysql:host=localhost;dbname=test', 'root', '');
$sql = "SELECT * FROM usuaris";
$result = $conn->query($sql);
echo "<ul>";
foreach ($result as $usuari) {
    echo "<li>" . $usuari['nom'] . "</li>";
}
echo "</ul>";
 ```
Amb separació:

```php
// Controlador (lògica)
$usuaris = Usuari::tots();

// Vista (presentació - Blade)
<ul>
    @foreach ($usuaris as $usuari)
        <li>{{ $usuari->nom }}</li>
    @endforeach
</ul>
```
#### Avantatges de la separació

| Avantatge        | Descripció                                                                 |
|------------------|-----------------------------------------------------------------------------|
| Mantenibilitat   | És més fàcil modificar el codi, ja que cada part està separada.             |
| Reutilització    | El codi es pot reutilitzar en diferents parts del projecte.                 |
| Escalabilitat    | És més senzill afegir noves funcionalitats sense trencar les existents.     |
| Treball en equip | Permet dividir tasques entre programadors backend i frontend.              |
| Testabilitat     | Podem fer proves unitàries de la lògica sense necessitat de la interfície.  |
| Seguretat        | Mantindre la lògica separada ajuda a controlar millor les entrades i sortides. |


En resum, separar la lògica de negoci dels aspectes de presentació és una bona pràctica fonamental per desenvolupar aplicacions web robustes, escalables i fàcils de mantindre. Aquesta separació s’aplica de forma natural amb frameworks com **Laravel**, que segueixen el patró **MVC (Model-Vista-Controlador)**.


### 🔧 Frameworks i mecanismes de separació

Un **framework** és un conjunt d'eines i biblioteques que facilita el desenvolupament d'aplicacions seguint una estructura predefinida i bones pràctiques.

#### Característiques generals:
- Facilita la separació de responsabilitats (MVC).
- Redueix el temps de desenvolupament.
- Estableix un patró coherent i mantenible.
- Incorpora sistemes de seguretat, validació, rutes i molt més.


### 🧱 Patró MVC (Model – Vista – Controlador)

El patró MVC és un **patró de disseny** que separa clarament tres responsabilitats:

| Component  | Funció principal |
|------------|------------------|
| **Model**  | Gestiona les dades i la lògica de negoci. |
| **Vista**  | Mostra la informació a l’usuari. |
| **Controlador** | Gestiona les peticions i coordina el Model i la Vista. |

![Modelo Vista Controlador](imagenes/07/mvc.png)

### 🚀 Laravel com a framework MVC

Laravel és un framework PHP modern que aplica de manera nativa el patró MVC.



    app/
    ├── Http/
    │ └── Controllers/ → Controladors (C)
    ├── Models/ → Models (M)
    resources/
    └── views/ → Vistes Blade (V)
    └── routes/ → Rutes (R)



#### 🧪 Exemple bàsic

Ruta:

```php
Route::get('/usuaris', [UsuariController::class, 'index']);
``` 

Controlador:
```php
class UsuariController extends Controller {
    public function index() {
        $usuaris = Usuari::all();
        return view('usuaris.index', compact('usuaris'));
    }
}

``` 
Models:

```php
class Usuari extends Model {
    protected $table = 'usuaris';
}

``` 
Vista (Blade):
```php
<ul>
@foreach($usuaris as $usuari)
    <li>{{ $usuari->nom }}</li>
@endforeach
</ul>

``` 

###  📦 Instal·lació de Laravel

#### 🔧 Crear una aplicació Laravel amb Docker (Sail)

Si estàs desenvolupant en Linux i ja tens Docker Compose instal·lat, pots crear una aplicació Laravel nova amb una simple comanda de term

1️⃣ Preparació (només si utilitzes Docker Desktop per a Linux)

Si estàs utilitzant Docker Desktop per a Linux, executa aquesta comanda:

```bash
docker context use default
```
Si no utilitzes Docker Desktop per a Linux, pots saltar aquest pas.

2️⃣ Crear el projecte

Executa aquesta comanda per crear una nova aplicació Laravel en una carpeta anomenada example-app


```bash
curl -s https://laravel.build/example-app | bash
``` 

Per descomptat, podeu canviar "exemple-app" en aquest URL a qualsevol cosa que vulgueu - només assegureu-vos que el nom de l'aplicació només conté caràcters alfanumèrics, guions i guions baixos. El directori de l'aplicació Laravel es crearà dins del directori des del qual executeu l'ordre.


3️⃣ Iniciar Laravel Sail

Ara podeu navegar al directori de l'aplicació i iniciar Laravel Sail. Laravel Sail proporciona una interfície senzilla de línia d'ordres per a interactuar amb la configuració predeterminada de l'acoblador Laravel:

```bash
cd exemple-app && ./vendor/bin/sail up &
```
La instal·lació del **Sail** pot trigar diversos minuts mentre els contenidors de l'aplicació del **sail** es construeixen a la vostra màquina local.


4️⃣ Executar les migracions

Una vegada arrancats els contenidors, pots aplicar les migracions:

```bash
./vendor/bin/sail artisan migrate
```
🌐 Accedir a l’aplicació

Ara pots obrir l’aplicació en el navegador en http://localhost.


📎 Annex: Instal·lació de phpMyAdmin amb Docker (opcional)

Si volem que funcione el phpmyadmin haurien d'afegir un altre contenidor docker, o farem incluint el següent codi en el docker-compose.yml

```php
myadmin:
 image: 'phpmyadmin:latest'
 ports:
 - 8080:80
 environment:
 MYSQL_ROOT_PASSWORD: '${DB_PASSWORD}'
 links:
 - "mysql:db"
 depends_on:
 - mysql
 networks:
 - sail
```

#### Estructura de carpetes simplificada

![Estructura directoris](./imagenes/03/carpetes_laravel.png){ width=400 }


### ⚙️ Configuració bàsica en Laravel

Laravel gestiona la configuració en el fitxer `.env` i en fitxers del directori `config/`.

**.env** → Conté les variables de configuració de l’entorn (nom de l’app, base de dades, correu…).  
**config/** → Conté fitxers PHP amb configuracions globals (`app.php`, `database.php`, etc.).

📌 Exemple `.env` mínim:

```env
APP_NAME="LaravelApp"
APP_ENV=local
APP_DEBUG=true
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_DATABASE=laravel
DB_USERNAME=root
DB_PASSWORD=
```
Per comprovar configuracions o generar codi, utilitza Artisan:

```bash
php artisan list        # Llista de comandes disponibles
php artisan route:list  # Llista totes les rutes de l’aplicació
``` 

## SA 3.2 CRUD bàsic en Laravel

![Funcionament Bàsic Laravel](imagenes/07/l101.png)

### 🛣️ Rutes
Les rutes web viuen a routes/web.php. Importa les classes amb use.

**Simple**

```php
    use Illuminate\Support\Facades\Route;
    Route::get('/salut', fn() => 'Hola món!');
 ```

**Amb Paràmetres (i opcionals)**

```php
    Route::get('/salut/{nom}', fn(string $nom) => "Bon dia, $nom");
    Route::get('/salut/{nom?}', fn(?string $nom = 'Convidat') => "Bon dia, $nom");
``` 

**Amb Validació bàsica (regex helpers)**

```php
Route::get('/producte/{id}', fn(int $id) => "Producte ID: $id")->whereNumber('id');
``` 

**Amb Route Model Binding (recomanat)**

```php
use App\Models\Producte;
Route::get('/productes/{producte}', fn(Producte $producte) => $producte->nom);
``` 

**Amb nom**

```php
Route::get('/contacte', fn() => 'Pàgina de contacte')->name('contacte');
// Blade: <a href="{{ route('contacte') }}">Contacte</a>
```

**Grups (prefix + middleware)**

```php
Route::prefix('admin')->middleware('auth')->group(function () {
Route::get('/dashboard', fn() => 'Admin Dashboard');
Route::get('/usuaris', fn() => 'Admin Usuaris');
});
``` 

**Controladors i recursos**

```php
use App\Http\Controllers\UsuariController;
use App\Http\Controllers\ArticleController;

Route::get('/usuari/{id}', [UsuariController::class, 'mostrar']);

Route::resource('articles', ArticleController::class);
// variants:
Route::resource('articles', ArticleController::class)->only(['index','show']);
``` 

### 🪟 Vistes i Blade (essencial)

Vistes en resources/views. No hi posem lògica de negoci.

**Mostrar vista i passar dades**

```php
Route::get('/', fn() => view('welcome'));
Route::get('/inici', function () {
    $nom = 'Nacho';
    return view('inici', compact('nom')); // o ['nom'=>$nom] o ->with('nom',$nom)
});
``` 

resources/views/inici.blade.php
```bladehtml
Benvingut/da, {{ $nom }}
``` 

#### 🗡️ Sintaxi Blade bàsica

```bladehtml
{{-- Comentari Blade --}}

Hola, {{ $nom }}     {{-- escapada (segura) --}}
{!! $html !!}        {{-- sense escapar (atenció XSS) --}}

@if($condicio) ... @elseif($altra) ... @else ... @endif

@foreach($items as $it) {{ $it }} @endforeach

@forelse($items as $it) {{ $it }} @empty Sense items @endforelse

``` 
####  📰 Layouts (herència)

resources/views/layouts/app.blade.php

```bladehtml 
<!doctype html>
<html>
<head>
  <title>@yield('title', config('app.name'))</title>
  @vite(['resources/css/app.css','resources/js/app.js'])
</head>
<body>
  @include('partials.nav')
  <main>@yield('content')</main>
</body>
</html>
``` 
Vista que hereta:

```bladehtml 
@extends('layouts.app')
@section('title','Inici')
@section('content')
  <h1>Benvingut/da!</h1>
@endsection
``` 

5.5 Components Blade
php artisan make:component Alert
Ús:
<x-alert type="success">Missatge enviat!</x-alert>
