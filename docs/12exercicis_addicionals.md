# Exercicis per treballar els resultats d'aprenentatge (RA3 - RA8)

## 📌 RA3 - Escriu blocs de sentències embeguts en llenguatges de marques

### 1️⃣ Formulari de registre amb validació bàsica
- Crea un formulari en HTML que demane: nom, email, contrasenya i data de naixement.
- Usa PHP per validar que tots els camps estan plens i que l'email té el format correcte.
- Mostra missatges d'error si la validació falla.

### 2️⃣ Calculadora bàsica amb PHP
- Crea un formulari HTML amb dos camps numèrics i quatre botons (sumar, restar, multiplicar i dividir).
- Quan l'usuari prem un botó, mostra el resultat en la mateixa pàgina.
- Usa `$_POST` per processar les operacions.

### 3️⃣ Simulació d’una botiga amb carret de compra
- Mostra una llista de productes amb un botó "Afegir al carret".
- Quan es polsa el botó, el producte s’afegeix a una sessió.
- Mostra el total de la compra i permet eliminar productes.

---

## 📌 RA4 - Desenvolupa aplicacions web embegudes en llenguatges de marques

### 4️⃣ Sistema de sessió d’usuari
- Crea un sistema d’inici de sessió amb PHP on els usuaris puguen entrar amb un nom d'usuari i una contrasenya.
- Mostra un missatge de benvinguda si la sessió està activa.
- Afig un botó de tancament de sessió que esborre la sessió.

### 5️⃣ Control d'accés a una pàgina web
- Crea dues pàgines: una pública i una privada.
- Els usuaris només poden accedir a la privada si estan autenticats.
- Redirigeix els usuaris no autenticats a la pàgina de login.

### 6️⃣ Sistema de comentaris amb sessions
- Permet als usuaris afegir comentaris a una pàgina sense base de dades.
- Guarda els comentaris en `$_SESSION` i mostra’ls ordenats per ordre d'inserció.
- Afig la possibilitat d’eliminar comentaris.

---

## 📌 RA5 - Desenvolupa aplicacions web separant el codi de presentació de la lògica de negoci

### 7️⃣ Refactorització d’una aplicació en PHP amb MVC
- Crea una aplicació PHP que gestione una llista de tasques (CRUD bàsic).
- Implementa la separació del codi en:
    - Model (`Task.php`): Gestiona les dades.
    - Vista (`tasks.view.php`): Mostra les tasques.
    - Controlador (`TaskController.php`): Gestiona les operacions (crear, eliminar, modificar).

### 8️⃣ Plantilles amb Twig
- Instal·la Twig i refés una aplicació existent per a utilitzar plantilles.
- Separa les dades del codi HTML usant `{{ variable }}` dins de les plantilles.

### 9️⃣ Autenticació avançada amb Laravel
- Implementa un sistema d’autenticació amb Laravel `Auth`.
- Personalitza la vista de login i registre.
- Crea diferents rols d’usuari (administrador, usuari).

---

## 📌 RA6 - Aplicacions web amb accés a bases de dades

### 🔟 CRUD de gestió d'usuaris en PHP
- Crea una aplicació que permeta afegir, modificar i eliminar usuaris en una base de dades MySQL.
- Utilitza `PDO` per fer consultes segures.
- Mostra un llistat d'usuaris en una taula HTML.

### 1️⃣1️⃣ Sistema de gestió de publicacions en Laravel
- Crea un projecte Laravel amb autenticació.
- Genera un model `Post` amb camps `title`, `content`, `user_id`.
- Implementa el CRUD amb Eloquent i Blade.

### 1️⃣2️⃣ Autenticació d'usuaris amb base de dades
- Adapta el sistema d’autenticació PHP per utilitzar una base de dades.
- Desa les credencials en MySQL i verifica els accessos fent consultes a la BD.

---

## 📌 RA7 - Desenvolupament de serveis web reutilitzables

### 1️⃣3️⃣ Creació d'una API REST amb Laravel
- Implementa un controlador d'API per gestionar tasques (`TaskController`).
- Implementa endpoints:
    - `GET /tasks` (llistat de tasques)
    - `POST /tasks` (crear una nova tasca)
    - `PUT /tasks/{id}` (actualitzar tasca)
    - `DELETE /tasks/{id}` (esborrar tasca)

### 1️⃣4️⃣ Autenticació JWT en una API
- Instal·la `laravel/passport` o `sanctum` per gestionar autenticació per tokens.
- Crea un endpoint `/login` que retorne un token JWT.
- Protegeix altres endpoints perquè només funcionen amb autenticació.

### 1️⃣5️⃣ Consumir una API externa amb Laravel
- Utilitza `GuzzleHTTP` per consumir una API externa, per exemple, obtenir dades meteorològiques des d’una API com OpenWeather.
- Mostra la informació en una vista Laravel.

---

## 📌 RA8 - Generació de pàgines web dinàmiques amb frameworks

### 1️⃣6️⃣ Generació de documents PDF amb Laravel
- Instal·la `barryvdh/laravel-dompdf`.
- Implementa una funcionalitat per generar un informe en PDF amb dades d’una base de dades.
- Exemple: Generar una factura en PDF amb la informació del client i els productes comprats.

### 1️⃣7️⃣ Gestió de permisos amb Middleware
- Crea un middleware per restringir accés a certes rutes segons el rol de l’usuari.
- Exemple: `/admin` només pot ser accedit per administradors.

### 1️⃣8️⃣ Aplicació en temps real amb Laravel i Pusher
- Implementa un xat en temps real amb Laravel, Pusher i WebSockets.
- Mostra missatges instantanis entre dos usuaris sense necessitat de recarregar la pàgina.

# Exercicis per treballar els resultats d'aprenentatge (RA3 - RA8)

## 📌 RA3 - Escriu blocs de sentències embeguts en llenguatges de marques

### 1️⃣ Formulari de registre amb validació bàsica
- **Solució:**
```php
<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $nom = trim($_POST['nom']);
    $email = trim($_POST['email']);
    $errors = [];
    if (empty($nom)) $errors[] = "El nom és obligatori.";
    if (!filter_var($email, FILTER_VALIDATE_EMAIL)) $errors[] = "Email no vàlid.";
}
?>
<form method="post">
    <input type="text" name="nom" placeholder="Nom">
    <input type="email" name="email" placeholder="Email">
    <button type="submit">Enviar</button>
</form>
```

### 2️⃣ Calculadora bàsica amb PHP
- **Solució:**
```php
<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $num1 = $_POST['num1'];
    $num2 = $_POST['num2'];
    $op = $_POST['operacio'];
    switch ($op) {
        case 'sumar': $resultat = $num1 + $num2; break;
        case 'restar': $resultat = $num1 - $num2; break;
    }
}
?>
<form method="post">
    <input type="number" name="num1">
    <input type="number" name="num2">
    <select name="operacio">
        <option value="sumar">Sumar</option>
        <option value="restar">Restar</option>
    </select>
    <button type="submit">Calcular</button>
</form>
<?php if (isset($resultat)) echo "Resultat: $resultat"; ?>
```

### 3️⃣ Simulació d’una botiga amb carret de compra
- **Solució:**
```php
<?php
session_start();
if (!isset($_SESSION['carret'])) $_SESSION['carret'] = [];
if (isset($_POST['producte'])) {
    $_SESSION['carret'][] = $_POST['producte'];
}
?>
<form method="post">
    <input type="text" name="producte" placeholder="Nom del producte">
    <button type="submit">Afegir</button>
</form>
<h2>Carret:</h2>
<ul>
    <?php foreach ($_SESSION['carret'] as $p) echo "<li>$p</li>"; ?>
</ul>
```

## 📌 RA4 - Desenvolupa aplicacions web embegudes en llenguatges de marques

### 4️⃣ Sistema de sessió d’usuari
- **Solució:**
```php
<?php
session_start();
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $_SESSION['usuari'] = $_POST['nom'];
}
if (isset($_SESSION['usuari'])) {
    echo "Benvingut, ".$_SESSION['usuari'];
    echo "<a href='logout.php'>Tanca sessió</a>";
} else {
?>
<form method="post">
    <input type="text" name="nom" placeholder="Nom d'usuari">
    <button type="submit">Iniciar sessió</button>
</form>
<?php } ?>
```

### 5️⃣ Control d'accés a una pàgina web
- **Solució:**
```php
<?php
session_start();
if (!isset($_SESSION['usuari'])) {
    header("Location: login.php");
    exit;
}
echo "Benvingut a la pàgina privada.";
```

### 6️⃣ Sistema de comentaris amb sessions
- **Solució:**
```php
<?php
session_start();
if (!isset($_SESSION['comentaris'])) $_SESSION['comentaris'] = [];
if ($_SERVER["REQUEST_METHOD"] == "POST" && !empty($_POST['comentari'])) {
    $_SESSION['comentaris'][] = $_POST['comentari'];
}
?>
<form method="post">
    <textarea name="comentari"></textarea>
    <button type="submit">Enviar</button>
</form>
<ul>
    <?php foreach ($_SESSION['comentaris'] as $c) echo "<li>$c</li>"; ?>
</ul>
```

## 📌 RA5 - Desenvolupa aplicacions web separant el codi de presentació de la lògica de negoci

### 7️⃣ Refactorització d’una aplicació en PHP amb MVC
- **Solució:**

- **Model:** `Task.php`
```php
class Task {
    public $id, $nom;
    public function __construct($id, $nom) {
        $this->id = $id;
        $this->nom = $nom;
    }
}
```

- **Vista:** `tasks.view.php`
```php
<?php foreach ($tasks as $task) echo "<li>$task->nom</li>"; ?>
```

- **Controlador:** `TaskController.php`
```php
require 'Task.php';
$tasks = [new Task(1, "Estudiar"), new Task(2, "Treballar")];
require 'tasks.view.php';
```

---
 

## 📌 RA6 - Aplicacions web amb accés a bases de dades

### 🔟 CRUD de gestió d'usuaris en PHP
- **Solució:**
```php
<?php
$pdo = new PDO("mysql:host=localhost;dbname=test", "root", "");
if ($_SERVER["REQUEST_METHOD"] == "POST" && isset($_POST['nom'])) {
    $stmt = $pdo->prepare("INSERT INTO usuaris (nom) VALUES (:nom)");
    $stmt->execute(['nom' => $_POST['nom']]);
}
$usuaris = $pdo->query("SELECT * FROM usuaris")->fetchAll();
?>
<form method="post">
    <input type="text" name="nom" placeholder="Nom">
    <button type="submit">Afegir Usuari</button>
</form>
<ul>
    <?php foreach ($usuaris as $usuari) echo "<li>{$usuari['nom']}</li>"; ?>
</ul>
```

### 1️⃣1️⃣ Sistema de gestió de publicacions en Laravel
- **Solució:**
```php
// Model
class Post extends Model {
    protected $fillable = ['title', 'content'];
}
// Controlador
class PostController extends Controller {
    public function store(Request $request) {
        Post::create($request->only(['title', 'content']));
        return redirect()->route('posts.index');
    }
}
// Rutes
Route::post('/posts', [PostController::class, 'store']);
```

## 📌 RA7 - Desenvolupament de serveis web reutilitzables

### 1️⃣3️⃣ Creació d'una API REST amb Laravel
- **Solució:**
```php
Route::middleware('auth:sanctum')->group(function () {
    Route::get('/tasks', [TaskController::class, 'index']);
    Route::post('/tasks', [TaskController::class, 'store']);
});
```

## 📌 RA8 - Generació de pàgines web dinàmiques amb frameworks

### 1️⃣6️⃣ Generació de documents PDF amb Laravel
- **Solució:**
```php
use Barryvdh\DomPDF\Facade as PDF;
class ReportController extends Controller {
    public function generate() {
        $data = ['title' => 'Informe PDF'];
        $pdf = PDF::loadView('pdf_view', $data);
        return $pdf->download('document.pdf');
    }
}
```

### 1️⃣7️⃣ Gestió de permisos amb Middleware
- **Solució:**
```php
class AdminMiddleware {
    public function handle($request, Closure $next) {
        if (!auth()->user()->isAdmin()) {
            return redirect('/home');
        }
        return $next($request);
    }
}
```

### 1️⃣8️⃣ Aplicació en temps real amb Laravel i Pusher
- **Solució:**
```php
use Pusher\Pusher;
$pusher = new Pusher('APP_KEY', 'APP_SECRET', 'APP_ID', ['cluster' => 'eu']);
$pusher->trigger('chat', 'message', ['message' => 'Hola món!']);
```

 
