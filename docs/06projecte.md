# Projecte Integrador Bloc 1.

??? abstract "Duració i criteris d'avaluació"

    Duració estimada: 16 hores

    <hr />

    | Resultat d'aprenentatge | Criteris d'avaluació |
    | --------                | --------             |
    | 3. Escriu blocs de sentències embeguts en llenguatges de marques, seleccionant i utilitzant les estructures de programació.| |
    | 4. Desenvolupa aplicacions web embegudes en llenguatges de marques analitzant i incorporant funcionalitats segons especificacions.| |
    | 5. Desenvolupa aplicacions web identificant i aplicant mecanismes per a separar el codi de presentació de la lògica de negoci.| |
    | 6. Desenvolupa aplicacions web d'accés a magatzems de dades, aplicant mesures per a mantindre la seguretat i la integritat de la informació| |



# Enunciat del Projecte: Backend de BatoiBooks

## Objectiu del Projecte

Desenvolupar el backend per a l’aplicació **BatoiBooks** en PHP, proporcionant:

- Autenticació per token JWT.
- Interfície d’administració amb funcionalitats avançades, com la generació de factures en PDF.

---

## Funcionalitats del Backend

### 1. BBDD

Crear la BBDD i les taules utilitzant el següent [sql](recursos/batoiBook/batoiBook-2.sql) 

### 2. Autenticació per al frontEnd

1. **Registre**: Endpoint per registrar nous usuaris. Rebrà dades com `email`, `nick` i `password`, i retornarà un token JWT per a la sessió de l’usuari.

2. **Login**: Endpoint per a l'inici de sessió, on es validarà `email` i `password`. En cas d'èxit, es generarà un token JWT amb la informació d'identificació de l'usuari.

3. **Validació de Token**: Cada controlador (excepte el de `login` i `register`) requerirà un token JWT vàlid per accedir a qualsevol dada, la qual cosa permetrà una gestió segura de la sessió.

---

### 3. API REST

Es crearà un fitxer PHP específic per a cada entitat, que atendrà les operacions CRUD bàsiques. Les taules que es gestionaran són:

- **Books**
- **Users**
- **Modules**
- **Courses**

Per a cada taula es permetran operacions:

- **GET**: Per obtenir dades (llistat o element per ID).
- **POST**: Per inserir nous elements.
- **PUT**: Per modificar elements existents.
- **DELETE**: Per eliminar elements.

Cada operació validarà les dades abans de ser processades i respondrà amb els estats corresponents.

---

#### Exemples de peticions

* Tornar un llibre

```http     
GET /api/books.php?id=2
``` 

* Tornar tots els llibres

```http 
GET /api/books.php
```

* Afegir un llibre

```http
POST /api/books.php
Contingut JSON: {
"userId": 2,
"moduleCode": "0011",
"publisher": "Apunts",
"price": 15.00,
"pages": 100,
"status": "new",
"photo": "ruta_foto.jpg",
"comments": "En bon estat"
}
```


### 4. Interfície d’Administrador

1. **Autenticació de l'usuari**: L'usuari s'autenticarà amb un usuari i es comprovarà que és l'administrador.
2. **Accés al CRUD de Mòduls i Cursos**: L’usuari administrador podrà gestionar completament les taules `modules` i `courses`.
3. **Generació de Factures en PDF**:
    - Permetre la selecció de dates i usuaris.
    - Calcular un 10% de l’import total de les vendes per generar la factura.
    - Incloure el logotip de l'aplicació, data de generació, import total i desglossament de vendes.

---

## Exigències Tècniques

- Utilitzar PHP com a llenguatge del servidor.
- Estructurar el projecte amb fitxers separats per a cada entitat dins de la carpeta `api/` i `backend`
- Utilitzar el format JSON per a la comunicació entre el client i el servidor.
- Garantir la seguretat en les peticions autenticades mitjançant el token JWT.
- Utilitzar en la mesura de lo possible el MVC en el backend i els control·ladors per a respondre a les peticions de l'API.
- Cal fer test de la lògica de la factura.
- Cal guardar en un fitxer de log les peticions que es fan a l'api en forma de: Usuari, IP client i Mètode utilitzat.   
- Utilitzar, en la mesura de lo possible, exempcions per al maneig d'errors de l'usuari.
 
---

## Exemples de resposta

Estos exemples es poden agafar com a referència per a la implementació de l'API. Però només són la base sobre la que construir una solució pròpia que puga incorporar l'harència de classes per fer
mes eficient i reutilitzable el codi.

### Estructura de directoris

```
App
├── Controllers
│   ├── Api
│   │   ├── ApiController.php 
│   │   ├── BookController.php
│   │   ├── CourseController.php
│   │   ├── ModuleController.php
│   │   └── AuthController.php
│   ├── ModuleController.php
│   ├── CourseController.php
│   └── AuthController.php
├── Helpers      
├── Exceptions       
├── Models
│   ├── Book.php
│   ├── Course.php
│   ├── Module.php
│   └── User.php
├── Services
│   ├── DBService.php
│   └── AuthService.php
├── Views
├── logs 
├── tests
├── config
│   └── connection.php
├── src
│   ├── api
│   │   ├── books.php
│   │   ├── courses.php
│   │   ├── modules.php
│   │   ├── register.php
│   │   └── login.php
│   ├── backend
│   │   ├── login.php
│   │   ├── generateInvoice.php
│   │   ├── modules.php
│   │   └── courses.php  
└── └── index.php
      
```   

### API

#### POSTMAN

Ací tens una [col.lecció del POSTMAN](./recursos/batoiBook/BatoiBooksApi.postman_collection.json) per realitzar les peticions i provar-les.

#### DBService.php

```php
namespace BatoiBook\Services;

class DBService
{
    public static function connect(): \PDO
    {
        $dbConfig =  require  $_SERVER['DOCUMENT_ROOT'] . '/../config/connection.php';

        try {
            $dsn = "mysql:host=" . $dbConfig['host'] . ";dbname=" . $dbConfig['dbname'];
            $db = new \PDO($dsn, $dbConfig['username'], $dbConfig['password']);
            $db->setAttribute(\PDO::ATTR_ERRMODE, \PDO::ERRMODE_EXCEPTION);
        } catch (\PDOException $e) {
            die("Error de connexió: " . $e->getMessage());
        }

        return $db;

    }
}
```

#### Model 

```php
namespace BatoiBook\Models;

class Course
{
   public function __construct(
   public int $id = 0,
   public string $course = '',
   public int $familyId = 0,
   public string $vliteral = '',
   public string $cliteral = '' ) 
   {}
}
```

#### Controlador

En el ApiController.php es troben les funcions comunes a tots els controladors, com el jsonResponse i errorResponse.  

```php
namespace BatoiBook\Controllers\Api;
use \PDO;
use \PDOException;

class CourseController extends ApiController
{
    protected PDO $db;
    public function __construct()
    {
        $this->db = DBService::connect();
    }

    public function getAll(): void
    {
        $stmt = $this->db->prepare("SELECT * FROM courses");
        $stmt->execute();
        $stmt->setFetchMode(PDO::FETCH_CLASS | PDO::FETCH_PROPS_LATE, Course::class);

        $this->jsonResponse($stmt->fetchAll());
    }

    public function getOne(int $id): void
    {
        //TODO: Implementar consulta 
        $record = $stmt->fetch();

        if ($record) {
            $this->jsonResponse($record);
        } else {
            $this->errorResponse("Record not found", 404);
        }
    }

    public function create(array $data): int
    {
        try {
            //TODO: Implementar inserció
            return $this->db->lastInsertId();
         } catch (PDOException $e) {
            $this->errorResponse("Failed to create record: " . $e->getMessage());
        }
    }

    public function update(int $id, array $data): void
    {
        try {
            //TODO: Implementar actualització

            $stmt->execute();
            if ($stmt->rowCount() > 0) {
                $this->jsonResponse(["message" => "Record updated successfully"]);
            } else {
                $this->errorResponse("Record not found", 404);
            }
        } catch (PDOException $e) {
            $this->errorResponse("Failed to update record: " . $e->getMessage());
        }
    }

    public function delete(int $id): void
    {
        //TODO: Implementar eliminació
        if ($stmt->rowCount() > 0) {
            $this->jsonResponse(["message" => "Record deleted successfully"]);
        } else {
            $this->errorResponse("Record not found", 404);
        }
    }
}
```

#### courses.php

```php
  
require_once $_SERVER['DOCUMENT_ROOT'] . '/../vendor/autoload.php';
require_once $_SERVER['DOCUMENT_ROOT'] . '/../Helpers/functions.php';

use BatoiBook\Controllers\Api\CourseController;
 
header("Content-Type: application/json");

$controller = new CourseController();
$method = $_SERVER['REQUEST_METHOD'];
$id = isset($_GET['id']) ? (int)$_GET['id'] : null;

switch ($method) {
    case 'GET':
        if (isset($id)) {
            $controller->getOne($id);
        } else {
            $controller->getAll ();
       }
        break;
    case 'POST':
        $data = json_decode(file_get_contents('php://input'), true);

        if ($data) {
            $controller->create($data);
        } else {
            echo json_encode(["error" => "Invalid data"]);
        }
        break;
    case 'PUT':
        $data = json_decode(file_get_contents('php://input'), true);

        if (isset($_GET['id']) && $data) {
            $success = $controller->update ($id, $data);
            echo json_encode(["message" => $success ? "Field updated successfully" : "Book not found"]);
        } else {
            echo json_encode(["error" => "Invalid data or ID"]);
        }
        break;
    case 'DELETE':
        if (isset($_GET['id'])) {
            $controller->delete ($id);
        } else {
            echo json_encode(["error" => "ID not provided"]);
        }
        break;
    default:
        echo json_encode(["error" => "Invalid request method"]);
        break;
}
```

### Autentificació

#### Requeriments previs

Cal instal·lar la llibreria `firebase/php-jwt` per a poder generar i validar els tokens JWT.

```bash
composer require firebase/php-jwt
```

#### login.php

```php
 
   require_once $_SERVER['DOCUMENT_ROOT'] . '/../vendor/autoload.php';
   
   use Firebase\JWT\JWT;
   use Firebase\JWT\Key;
   use BatoiBook\Services\DBService;
   
   // Clau secreta per generar el token (és important mantenir-la segura)
   $secretKey = 'clau_secreta';
   header('Content-Type: application/json');
   // Llegeix les dades de la petició
   $data = json_decode(file_get_contents("php://input"));
    
   if (!empty($data->email) && !empty($data->password)) {
       
        $db = DBService::connect();  
        //TODO: Implementar consulta per recuperar l'usuari
        $user = $stmt->fetch();
        if ($user) {
            if (password_verify($data->password,$user->password)) {
                $payload = [
                     "iss" => "http://localhost", // Issuer
                     "aud" => "http://localhost", // Audience
                     "iat" => time(),             // Issued at
                     "exp" => time() + 3600,      // Expira en una hora
                     "userId" => $userId
                 ];
                $jwt = JWT::encode($payload, $secretKey, 'HS256');    
                echo json_encode(["success" => true, "token" => $jwt]);
            } else {
                echo json_encode(["success" => false, "message" => "Contrasenya incorrecta"]);
            }
        } else {
            echo json_encode(["success" => false, "message" => "Usuari no trobat"]);
        }
   
   } else {
       echo json_encode(["success" => false, "message" => "Falten dades"]);
   }
``` 

#### register.php

```php
//TODO: Implementar registre d'usuari
```

#### validate.php

per a validar que qualsevol petició a l'API siga autenticada.
```php
if (!isset($_SERVER['HTTP_AUTHORIZATION'])) {
      throw new UnAuthoritzedException("Token no proporcionat");
}
$authHeader = $_SERVER['HTTP_AUTHORIZATION'];
[$type, $token] = explode(" ", $authHeader);
if ($type !== 'Bearer') {
    throw new UnAuthoritzedException("Tipus de token no vàlid");
}
try {
    $jwt = JWT::decode($token, new Key(SELF::SECRET_KEY, 'HS256'));
    $userId = $jwt->userId;
} catch (Exception $e) {
    throw new UnAuthoritzedException("Token no vàlid o expirat");
}
 
```

 
