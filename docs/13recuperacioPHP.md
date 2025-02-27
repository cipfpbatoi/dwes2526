# **Projecte: Control d'Accés a un Pàrquing amb Porta Automàtica**

## **1. Descripció del Projecte**
Aquest projecte implementa un sistema per gestionar l’accés d’un pàrquing mitjançant una porta automàtica. Els usuaris poden registrar-se i afegir vehicles, però un administrador ha d’autoritzar-los perquè puguin accedir. Quan la porta llegeix una matrícula, el sistema ha de validar si està autoritzada i respondre amb un **OK** o **FALSE**.

## **2. Funcionalitats**
### **Funcionalitats per als usuaris**
- Registre d’usuari.
- Inici de sessió i gestió de sessió.
- Afegir un vehicle al sistema.
- Veure l’estat d’aprovació dels seus vehicles.

### **Funcionalitats per a l'administrador**
- Llistar vehicles pendents d’aprovació.
- Aprovar o rebutjar vehicles.

### **Funcionalitats per a la porta automàtica**
- Enviar una matrícula al sistema per validar si està registrada i autoritzada.
- Rebre una resposta (`OK` o `FALSE`).

---

## **3. Requeriments Tècnics**
- **PHP** (versió 7 o superior).
- **MySQL/MariaDB** com a base de dades.
- **HTML + CSS + JavaScript** per a la interfície d’usuari.
- **AJAX** per a les peticions de la porta automàtica.
- **Sessions en PHP** per a l’autenticació.
- **Estructura MVC** per separar la lògica.

---

## **4. Model de Dades (Base de Dades)**
### **Taula `users` (Usuaris)**
```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    is_active BOOLEAN DEFAULT TRUE,
    role ENUM('admin', 'user') DEFAULT 'user'
);
```

### **Taula `vehicles` (Vehicles)**
```sql
CREATE TABLE vehicles (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    license_plate VARCHAR(20) UNIQUE NOT NULL,
    model VARCHAR(100) NOT NULL,
    is_approved BOOLEAN DEFAULT FALSE,
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

---

## **5. Estructura de Carpetes (MVC)**
```plaintext
/parking-access
│── /public
│   ├── index.php           # Entrada principal
│   ├── assets/             # CSS, JS, imatges
│── /app
│   ├── controllers/        # Controladors
│   │   ├── UserController.php
│   │   ├── VehicleController.php
│   │   ├── AdminController.php
│   │   ├── AccessController.php
│   ├── models/             # Models
│   │   ├── User.php
│   │   ├── Vehicle.php
│   ├── views/              # Vistes
│   │   ├── users/
│   │   │   ├── register.php
│   │   │   ├── login.php
│   │   │   ├── dashboard.php
│   │   ├── admin/
│   │   │   ├── vehicle_list.php
│   │   ├── access/
│   │   │   ├── check_access.php
│── /config
│   ├── config.php          # Configuració BD
│── /core
│   ├── Router.php          # Gestió de rutes
│   ├── Controller.php      # Classe base per controladors
│   ├── Model.php           # Classe base per models
│── .htaccess               # Reescriptura d’URL
│── composer.json           # Dependències (opcional)
│── README.md
```

---

## **6. Configuració del Projecte**

### **1. Configurar Connexió a la Base de Dades**
Fitxer `/config/config.php`:
```php
<?php
define('DB_HOST', 'localhost');
define('DB_NAME', 'parking');
define('DB_USER', 'root');
define('DB_PASS', '');

try {
    $pdo = new PDO("mysql:host=" . DB_HOST . ";dbname=" . DB_NAME, DB_USER, DB_PASS);
    $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
} catch (PDOException $e) {
    die("Error en la connexió: " . $e->getMessage());
}
?>
```

### **2. Implementar el Model d'Usuari**
Fitxer: `/app/models/User.php`
```php
<?php
class User {
    private $db;

    public function __construct($db) {
        $this->db = $db;
    }

    public function register($name, $email, $password) {
        $hashedPassword = password_hash($password, PASSWORD_DEFAULT);
        $stmt = $this->db->prepare("INSERT INTO users (name, email, password) VALUES (?, ?, ?)");
        return $stmt->execute([$name, $email, $hashedPassword]);
    }

    public function login($email, $password) {
        $stmt = $this->db->prepare("SELECT * FROM users WHERE email = ?");
        $stmt->execute([$email]);
        $user = $stmt->fetch(PDO::FETCH_ASSOC);
        return $user && password_verify($password, $user['password']) ? $user : false;
    }
}
?>
```

### **3. Implementar el Controlador d’Usuari**
Fitxer: `/app/controllers/UserController.php`
```php
<?php
require_once 'app/models/User.php';

class UserController {
    private $userModel;

    public function __construct($db) {
        $this->userModel = new User($db);
    }

    public function register() {
        if ($_SERVER["REQUEST_METHOD"] == "POST") {
            $name = $_POST['name'];
            $email = $_POST['email'];
            $password = $_POST['password'];

            if ($this->userModel->register($name, $email, $password)) {
                header("Location: /login");
                exit();
            } else {
                echo "Error en el registre.";
            }
        }
        include 'app/views/users/register.php';
    }
}
?>
```

---

Aquest seria el començament del projecte. Pots continuar amb els controladors de vehicles, administradors i la resposta de la porta automàtica!

