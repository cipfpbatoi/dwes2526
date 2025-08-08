# Arquitectura MVC amb Laravel

??? abstract "Duració i criteris d'evaluació"

    Duració estimada: 16 hores

    <hr />

    | Resultat d'aprenentatge  | Criteris d'avaluació  |
    | ------                    | -----                |
    | 5. Desenvolupa aplicacions Web identificant i aplicant mecanismes per a separar el codi de presentació de la lògica de negoci. | a) S'han identificat els avantatges de separar la lògica de negoci dels aspectes de presentació de l'aplicació. b) S'han analitzat i utilitzat mecanismes i frameworks que permeten realitzar aquesta separació i les seues característiques principals. c) S'han utilitzat objectes i controls en el servidor per a generar l'aspecte visual de l'aplicació web en el client. d) S'han utilitzat formularis generats de manera dinàmica per a respondre als esdeveniments de l'aplicació web. e) S'han identificat i aplicat els paràmetres relatius a la configuració de l'aplicació web. f) S'han escrit aplicacions web amb manteniment d'estat i separació de la lògica de negoci. g) S'han aplicat els principis i patrons de disseny de la programació orientada a objectes. h) S'ha provat i documentat el codi. |

## SA3.1  Introducció al patró MVC i la separació de capes. Instal·lació de Laravel.   

###  Avantatges de separar la lògica de negoci dels aspectes de presentació
 
#### 🔍 Què és la separació de capes?

La **separació de capes** consisteix a dividir una aplicació en mòduls independents segons la seua responsabilitat. En aplicacions web, les dues capes principals són:

- **Capa de presentació:** S’encarrega de mostrar la informació a l’usuari (interfície web).
- **Capa de lògica de negoci:** Processa la informació, aplica regles, realitza càlculs i gestiona dades.

---

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

### 🔧 Què és un Framework?

Un **framework** és un conjunt d'eines i biblioteques que facilita el desenvolupament d'aplicacions seguint una estructura predefinida i bones pràctiques.

#### Característiques generals:
- Facilita la separació de responsabilitats (MVC).
- Redueix el temps de desenvolupament.
- Estableix un patró coherent i mantenible.
- Incorpora sistemes de seguretat, validació, rutes i molt més.

---

### 🧱 Patró MVC (Model – Vista – Controlador)

El patró MVC és un **patró de disseny** que separa clarament tres responsabilitats:

| Component  | Funció principal |
|------------|------------------|
| **Model**  | Gestiona les dades i la lògica de negoci. |
| **Vista**  | Mostra la informació a l’usuari. |
| **Controlador** | Gestiona les peticions i coordina el Model i la Vista. |

---

### 🚀 Laravel com a framework MVC

Laravel és un framework PHP modern que aplica de manera nativa el patró MVC.

#### 📂 Estructura bàsica d’una aplicació Laravel

    app/
    ├── Http/
    │ └── Controllers/ → Controladors (C)
    ├── Models/ → Models (M)
    resources/
    └── views/ → Vistes Blade (V)


---

### ⚙️ Mecanismes de separació en Laravel

| Mecanisme                     | Descripció |
|------------------------------|------------|
| **Controladors**             | Gestionen la lògica d’interacció amb l’usuari. |
| **Models Eloquent**          | Accés a dades mitjançant ORM (Object-Relational Mapping). |
| **Blade Templates**          | Sistema de plantilles per a la presentació de dades. |
| **Rutes (`routes/web.php`)** | Enllacen URLs amb controladors. |
| **Request/Response Cycle**   | Permet captar i retornar dades estructurades. |

---

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

En resum, els frameworks com Laravel implementen el patró MVC, afavorint la separació de la lògica de negoci i la capa de presentació. Aquesta divisió millora la claredat del projecte, la col·laboració en equip i la mantenibilitat del codi a llarg termini.

###  Instal·lació de Laravel

#### I🔧 Crear una aplicació Laravel amb Docker (Sail)

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


