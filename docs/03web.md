# Programació Web

??? abstract "Duració i criteris d'evaluació"

    Duració estimada: 10 hores

    <hr />

    | Resultat d'aprenentatge  | Criteris d'avaluació  |
    | ------                    | -----                |
    | 4. Desenvolupa aplicacions Web embegudes en llenguatges de marques analitzant i incorporant funcionalitats segons especificacions | a) S'han identificat els mecanismes disponibles per al manteniment de la informació que concerneix un client web concret i s'han assenyalat els seus avantatges.<br /> b) S'han utilitzat mecanismes per a mantindre l'estat de les aplicacions web.<br /> c) S'han utilitzat mecanismes per a emmagatzemar informació en el client web i per a recuperar el seu contingut.<br /> d) S'han identificat i caracteritzat els mecanismes disponibles per a l'autenticació d'usuaris.<br /> e) S'han escrit aplicacions que integren mecanismes d'autenticació d'usuaris.<br /> f) S'han utilitzat eines i entorns per a facilitar la programació, prova i depuració del codi. |



## Gestió de l'estat

HTTP és un protocol **stateless**, sense estat. Per això, se simula l'estat mitjançant l'ús de cookies, tokens o la sessió. L'estat és necessari per a processos com ara el carret de la compra, operacions associades a un usuari, etc...
El mecanisme de PHP per a gestionar la sessió empra cookies de manera interna.
Les cookies s'emmagatzemen en el navegador, i la sessió en el servidor web.

### Cookies

Les cookies s'emmagatzemen en el array global `$_COOKIE`. El que col·loquem dins del array, es guardarà en el client. Cal tindre present que el client pot no voler emmagatzemar-les.

Existeix una limitació de 20 cookies per domini i 300 en total en el navegador.

En PHP, per a crear una cookie s'utilitza la funció `setcookie`:

``` php
<?php
setcookie(nombre [, valor [, expira [, ruta [, dominio [, seguro [, httponly ]]]]]]);
setcookie(nombre [, valor = "" [, opciones = [] ]] )
?>
```
Destacar que el nom no pot contindre espais ni el caràcter `;`. Respecte al contingut de la cookie, no pot superar els 4 KB.

Per exemple, mitjançant *cookies* podem comprovar la quantitat de visites diferents que realitza un usuari:

``` php
<?php
$accesosPagina = 0;
if (isset($_COOKIE['accesos'])) { 
    $accesosPagina = $_COOKIE['accesos']; // recuperamos una cookie
    setcookie('accesos', ++$accesosPagina); // le asignamos un valor
}
?>
```

!!! tip "Inspeccionant les cookies"
    Si volem veure que contenen les cookies que tenim emmagatzemades en el navegador, es pot comprovar el seu valor en Dev Tools --> Application --> Storage

El temps de vida de les cookies pot ser tan llarg com el lloc web en el qual resideixen. Elles seguiran ací, fins i tot si el navegador està tancat o obert.

Per a esborrar una cookie es pot posar que expiren en el passat:

``` php
<?php
setcookie(nombre, "", 1) // pasado
```

O que caduquen dins d'un període de temps deteminado:

``` php
<?php
setcookie(nombre, valor, time() + 3600) // Caducan dentro de una hora
```

<figure style="align: center;">
    <img src="imagenes/04/04cookies.png" width="700">
    <figcaption>Comunicació amb cookies</figcaption>
</figure>

S'utilitzen per a:

* Recordar els inicis de sessió
* Emmagatzemar valors temporals d'usuari
* Si un usuari està navegant per una llista paginada d'articles, ordenats d'una certa manera, podem emmagatzemar l'ajust de la classificació.

L'alternativa en el client per a emmagatzemar informació en el navegador és l'objecte [LocalStorage](https://developer.mozilla.org/es/docs/web/api/window/localstorage).

### Sessió

La sessió afig la gestió de l'estat a HTTP, emmagatzemant en aquest cas la informació en el servidor.
Cada visitant té un ID de sessió únic, el qual per defecte s'emmagatzema en una cookie denominada `PHPSESSID`.
Si el client no té les cookies actives, l'ID es propaga en cada URL dins del mateix domini.
Cada sessió té associat un magatzem de dades mitjançant el array global `$_SESSION`, en el qual podem emmagatzemar i recuperar informació.

La sessió comença en executar un script PHP. Es genera un nou ID i es carreguen les dades del magatzem:

<figure style="align: center;">
    <img src="imagenes/04/04sesion.png" width="700">
    <figcaption>Comunicació amb sessions</figcaption>
</figure>

Les operacions que podem realitzar amb la sessió són:

``` php
<?php
session_start(); // carga la sesión
session_id() // devuelve el id
$_SESSION[clave] = valor; // inserción
session_destroy(); // destruye la sesión
unset($_SESSION[clave]; // borrado
```

Veurem mitjançant un exemple com podem inserir en un pàgina dades en la sessió per a posteriorment en una altra pàgina accedir a aqueixes dades. Per exemple, en `sesion1.php` tindríem

``` php
<?php
session_start(); // inicializamos
$_SESSION["ies"] = "IES Severo Ochoa"; // asignación
$instituto = $_SESSION["ies"]; // recuperación
echo "Estamos en el $instituto ";
?>
<br />
<a href="sesion2.php">Y luego</a>
```

I posteriorment podem accedir a la sessió en `sesion2.php`:

``` php
<?php
session_start();
$instituto = $_SESSION["ies"]; // recuperación
echo "Otra vez, en el $instituto ";
?>
```

!!! note "Configurant la sessió en `php.ini`"
    Les següent propietats de `php.ini` permeten configurar alguns aspectes de la sessió:

      * `session.save_handler`: controlador que gestiona com s'emmagatzema (`files`)
      * `session.save_path`: ruta on s'emmagatzemen els arxius amb les dades (si tenim un clúster, podríem usar `/mnt/sessions` en tots els servidor de manera que apunten a una carpeta compartida)
      * `session.name`: nom de la sessió (`PHSESSID`)
      * `session.acte_start`: Es pot fer que s'autocarregue amb cada script. Per defecte està deshabilitat
      * `session.cookie_lifetime`: temps de vida per defecte

Més informació en la [documentació oficial](https://www.php.net/manual/es/session.configuration.php).

### Serialització en PHP

La serialització és el procés de convertir una estructura de dades o un objecte en una seqüència de caràcters que pot ser fàcilment emmagatzemada o transmesa i després reconstruïda. PHP proporciona dos funcions principals per a això: serialize() i unserialize().

1. serialize()
   La funció serialize() en PHP s'utilitza per a convertir una estructura de dades o un objecte en una representació de cadena.

``` php
$data = array("a", "b", "c");
$serialized_data = serialize($data);
echo $serialized_data;
```
Eixida 

``` php
a:3:{i:0;s:1:"a";i:1;s:1:"b";i:2;s:1:"c";}
```

2. unserialize()
   La funció unserialize() en PHP s'utilitza per a convertir la representació de cadena serialitzada de nou en una estructura de dades o un objecte.

``` php
$original_data = unserialize($serialized_data);
print_r($original_data);
```

Eixida

``` php
Array
(
    [0] => a
    [1] => b
    [2] => c
)
```

#### Utilitzant amb Sessions
Les sessions en PHP permeten emmagatzemar informació d'usuari per ser utilitzada en diverses pàgines. Pot ser útil serialitzar dades per a emmagatzemar-les en una sessió:

Iniciant una sessió i emmagatzemant dades serialitzades:

``` php
session_start();

$data = array("a", "b", "c");
$_SESSION['data_serialitzada'] = serialize($data);
``` 

``` php
session_start();

if (isset($_SESSION['data_serialitzada'])) {
$data = unserialize($_SESSION['data_serialitzada']);
print_r($data);
}
```

Consideracions de Seguretat:
És crucial entendre que la funció unserialize() pot ser perillosa si s'usa amb dades que no són de confiança, ja que podria portar a l'execució de codi arbitrari. Per això, mai has de deserialitzar dades que vinguen d'una font desconeguda o no fiable sense validar-les prèviament.

## Autenticació d'usuaris

### Mecanismes d'Autenticació d'Usuaris

| Mecanisme d'Autenticació | Característiques | Avantatges |
| ------------------------- | ---------------- | ---------- |
| **Bàsica (usuari/contrasenya)** | Es requereix un nom d'usuari i una contrasenya per accedir. | Fàcil d'implementar, àmpliament utilitzada. |
| **Cookies** | Emmagatzema informació d'autenticació en el navegador de l'usuari. | Persistència d'inici de sessió, personalització d'experiència. |
| **Sessions** | Manté l'estat d'autenticació en el servidor amb una identificació de sessió única. | Major seguretat, evita la necessitat d'emmagatzemar informació sensible al client. |
| **OAuth** | Permet als usuaris accedir a recursos sense compartir les seves credencials. | Seguretat millorada, experiència d'usuari simplificada. |
| **JWT (JSON Web Token)** | Utilitza tokens basats en JSON per a l'autenticació. | Lliure d'estat, fàcil de compartir entre diferents serveis. |
| **SAML (Security Assertion Markup Language)** | Utilitza XML per a intercanviar dades d'autenticació entre l'usuari i el servei. | Integració amb sistemes d'autenticació empresarial, alt nivell de seguretat. |
| **Autenticació multifactor (MFA)** | Requereix múltiples formes de verificació (per exemple, contrasenya + codi SMS). | Seguretat augmentada, redueix el risc de compromís de comptes. |

#### Exemple amb sessions

Una sessió estableix una relació anònima amb un usuari particular, de manera que podem saber si és el mateix usuari entre dues peticions diferents. Si preparem un sistema de login, podrem saber qui utilitza la nostra aplicació.

``` php
<?php
// Llista d'usuaris predefinits amb contrasenyes en text pla
$users = [
    'user1@example.com' => 'password1',
    'user2@example.com' => 'password2',
];

// Convertir les contrasenyes a un format encriptat
foreach ($users as $email => $password) {
    $users[$email] = password_hash($password, PASSWORD_BCRYPT);
}

// Formulari d'autenticació
if (isset($_POST['login'])) {
    $email = $_POST['email'];
    $password = $_POST['password'];

    if (isset($users[$email]) && password_verify($password, $users[$email])) {
        // L'usuari està autenticat
        session_start();
        $_SESSION['user'] = $email;
        echo "Login successful. Welcome, " . $email;
    } else {
        // Credencials incorrectes
        echo "Invalid email or password.";
    }
}
?>
<form method="post">
    Email: <input type="email" name="email" required>
    Password: <input type="password" name="password" required>
    <button type="submit" name="login">Login</button>
</form>
```
Aquest exemple mostra com mantenir l'estat de la sessió d'un usuari una vegada autenticat.
    
``` php
<?php
session_start();

if (!isset($_SESSION['user'])) {
    header("Location: login.php");
    exit();
}

// Mostra la pàgina només si l'usuari està autenticat
echo "Welcome, " . $_SESSION['user'];
?>
```

Finalment, necessitem l'opció de tancar la sessió que col·loquem en `logout.php`:

``` php
<?php
// Recuperamos la información de la sesión
session_start();

// Y la destruimos
session_destroy();
header("Location: index.php");
?>
```

!!! warning "Autenticació en producció"
    En l'actualitat l'autenticació d'usuari no es realitza gestionant la sessió direcamente, sinó que es realitza mitjançant algun framekwork que abstrau tot el procés o la integració de mecanismes d'autenticació tipus *OAuth*, com estudiarem en l'última unitat mitjançant *Laravel*.

#### Exemple amb cookies

``` php
<?php
// Llista d'usuaris predefinits amb contrasenyes en text pla
$users = [
    'user1@example.com' => 'password1',
    'user2@example.com' => 'password2',
];

// Convertir les contrasenyes a un format encriptat
foreach ($users as $email => $password) {
    $users[$email] = password_hash($password, PASSWORD_BCRYPT);
}

if (isset($_POST['login'])) {
    $email = $_POST['email'];
    $password = $_POST['password'];

    if (isset($users[$email]) && password_verify($password, $users[$email])) {
        // Establir una cookie d'autenticació
        setcookie("user", $email, time() + (86400 * 30), "/"); // 86400 = 1 dia
        echo "Login successful. Welcome, " . $email;
    } else {
        // Credencials incorrectes
        echo "Invalid email or password.";
    }
}

// Llegir la cookie
if (isset($_COOKIE['user'])) {
    echo "Welcome back, " . $_COOKIE['user'];
}
?>
<form method="post">
    Email: <input type="email" name="email" required>
    Password: <input type="password" name="password" required>
    <button type="submit" name="login">Login</button>
</form>
```

!!! warning "Seguretat en cookies"
    Les cookies són vulnerables a atacs com *Cross-Site Scripting (XSS)* i *Cross-Site Request Forgery (CSRF)*. Per a protegir-les, s'ha de configurar la cookie com a segura i només accessible a través de la web.

#### Exemple amb JWT

Aquest exemple mostra com generar i verificar un JWT per a l'autenticació.

``` php
<?php
function base64UrlEncode($data) {
    return rtrim(strtr(base64_encode($data), '+/', '-_'), '=');
}

function base64UrlDecode($data) {
    return base64_decode(strtr($data, '-_', '+/'));
}

function createJWT($header, $payload, $secret) {
    $headerEncoded = base64UrlEncode(json_encode($header));
    $payloadEncoded = base64UrlEncode(json_encode($payload));

    $signature = hash_hmac('sha256', "$headerEncoded.$payloadEncoded", $secret, true);
    $signatureEncoded = base64UrlEncode($signature);

    return "$headerEncoded.$payloadEncoded.$signatureEncoded";
}

function verifyJWT($jwt, $secret) {
    list($headerEncoded, $payloadEncoded, $signatureEncoded) = explode('.', $jwt);

    $signature = base64UrlDecode($signatureEncoded);
    $expectedSignature = hash_hmac('sha256', "$headerEncoded.$payloadEncoded", $secret, true);

    if ($signature === $expectedSignature) {
        return json_decode(base64UrlDecode($payloadEncoded));
    }

    return false;
}

// Exemples d'ús
$header = ['alg' => 'HS256', 'typ' => 'JWT'];
$payload = ['email' => 'user1@example.com', 'exp' => time() + 3600];
$secret = 'your_secret_key';

$jwt = createJWT($header, $payload, $secret);
echo "JWT: " . $jwt . "\n";

$decoded = verifyJWT($jwt, $secret);
if ($decoded) {
    echo "JWT valid: " . json_encode($decoded) . "\n";
} else {
    echo "Invalid JWT.\n";
}
?>

```
#### Exemple amb MFA

Aquest exemple mostra com afegir una capa addicional d'autenticació amb un codi MFA.

``` php
<?php
session_start();

function sendMFACode() {
    $code = rand(100000, 999999);
    $_SESSION['mfa_code'] = $code;

    // Simular enviament de codi via email o SMS
    echo "Verification code: $code"; // En un entorn real, envia el codi per email o SMS.
}

function verifyMFACode($inputCode) {
    return isset($_SESSION['mfa_code']) && $inputCode == $_SESSION['mfa_code'];
}

if (isset($_POST['send_code'])) {
    sendMFACode();
}

if (isset($_POST['verify_code'])) {
    if (verifyMFACode($_POST['mfa_code'])) {
        echo "MFA successful.";
    } else {
        echo "Invalid verification code.";
    }
}
?>
<form method="post">
    <button type="submit" name="send_code">Send MFA Code</button>
</form>
<form method="post">
    MFA Code: <input type="text" name="mfa_code" required>
    <button type="submit" name="verify_code">Verify MFA Code</button>
</form>

```

#### Exemple amb OAuth

Per a OAuth, es pot utilitzar un proveïdor extern com Google per autenticar els usuaris. Ho vorem més avant.

``` php
<?php
require_once 'vendor/autoload.php';

$provider = new League\OAuth2\Client\Provider\Google([
    'clientId'     => 'your-client-id',
    'clientSecret' => 'your-client-secret',
    'redirectUri'  => 'your-redirect-url',
]);

if (!isset($_GET['code'])) {
    $authUrl = $provider->getAuthorizationUrl();
    $_SESSION['oauth2state'] = $provider->getState();
    header('Location: ' . $authUrl);
    exit;
} elseif (empty($_GET['state']) || ($_GET['state'] !== $_SESSION['oauth2state'])) {
    unset($_SESSION['oauth2state']);
    exit('Invalid state');
} else {
    $token = $provider->getAccessToken('authorization_code', [
        'code' => $_GET['code']
    ]);

    $user = $provider->getResourceOwner($token);
    $userData = $user->toArray();

    // Mostra la informació de l'usuari
    echo 'Hello, ' . $userData['name'];
}
?>
```



## Referències

* [Cookies en PHP](https://www.php.net/manual/es/features.cookies.php)
* [Manejo de sesiones en PHP](https://www.php.net/manual/es/book.session.php)

## Exercicis

400. [402.html](recursos/402.html) Treballa sobre este formulari.

### Activitat
421. [newBook.php](recursos/newBook.php) Utilitzant este formulari completa-lo per a que ixca la llista amb els mòduls i el select amb l'estat del llibre. Mostra els valors carregats en un resumen.

422. `newBook.php`: A partir del formulari anterior, introdueix validacions en php per tal que:
     * el camps editorial, preu, pàgines siguen requerits i del tipus adient.
     * el camp mòdul i status siguen vàlids.

!!! tip "Utilitza exempcions"
    Pots utilitzar exempcions per a tractar els errors.

423. `newBook.php`: Separa la part html de la de php. Crea una vista /views/books/new.php que carregue el formulari. Crida'l amb un include des de `newBook.php`.
424. `/views/books/new.php`: Modifica el formulari per a que mostre els errors i els valors introduïtsen el mateix formulari. Haurà de crear un funció `printError($errors,$field)` en una llibreria `/myHelpers/utils.php` que mostre el error d'un camp.
425. `newBook.php`: Si tot va bé, crea un objecte de la classe Book, introdueix el llibre creat pel formulari i mostra'l. 
426. `load.php` : Anem a crear un fitxer load.php que importaran tots els fitxers (no les classes) de la web. El fitxer contindrà:
     * El autoload 
     * La creació de la sessió
     * La inicialitació de les variables $users, $books, $modules, $courses, $statuses de la següent forma:
       * Es carregara des de la variable de sessio corresponent si existeix.
       * En cas contrari es crearà, s'inicialitzarà i s'emmagatzemarà en la variable de sessió corresponent.
       * Utilitza serialize i unserialize per a emmagatzemar els objectes en la sessió.
427. [register.php](recursos/register.php) A partir d'aquest fitxer crear la vista `/views/user/register.php`
428. `register.php`: Tracta el formulari per a 
     * Valida el formulari de forma que els camps sigue obligatoris i les contrasenyes coincidisquen. Crea si calen noves exempcions.
     * Opcional: Validar que ni el nick d'usuari ni el email estiga repetit en users.
     * Crea un nou usuari i guardar-lo en la variable de sessió $users.
     * Ves a index.php i mostra el nom de l'usuari registrat.
429. [login.php](recursos/login.php): A partir d'aquest fitxer crear la vista `/views/user/login.php`
430. `login.php`: Tracta el formulari per a
     * Comprovar que l'usuari i la contrasenya siguen correctes. En cas contrari recuperar el formulari amb l'email introduït i amb un missatge d'error
     * Ves a index.php i mostra el nom de l'usuari loguejat.
431. `logout.php`: Crea un fitxer logout.php que tanque la sessió i redirigeix a index.php.
432. `header.php` : Crea una capçalera on aparega:
     * L'usuari loguejat i l'enllaç a newBook i a logout si hi ha usuari.
     * L'enllaç a login o register en cas contrari.
     * Fes que la capçalera es carregue en totes les pàgines.
433. `newBook.php` : Fes que ningú no loguejat puga accedir a la pàgina i quan es guarde un llibre o faça amb l'id de l'usuari loguejat.
