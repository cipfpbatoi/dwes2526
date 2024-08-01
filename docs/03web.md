# Programació Web

??? abstract "Duració i criteris d'evaluació"

    Duració estimada: 10 hores

    <hr />

    | Resultat d'aprenentatge  | Criteris d'avaluació  |
    | ------                    | -----                |
    | 4. Desenvolupa aplicacions Web embegudes en llenguatges de marques analitzant i incorporant funcionalitats segons especificacions | a) S'han identificat els mecanismes disponibles per al manteniment de la informació que concerneix un client web concret i s'han assenyalat els seus avantatges.<br /> b) S'han utilitzat mecanismes per a mantindre l'estat de les aplicacions web.<br /> c) S'han utilitzat mecanismes per a emmagatzemar informació en el client web i per a recuperar el seu contingut.<br /> d) S'han identificat i caracteritzat els mecanismes disponibles per a l'autenticació d'usuaris.<br /> e) S'han escrit aplicacions que integren mecanismes d'autenticació d'usuaris.<br /> f) S'han utilitzat eines i entorns per a facilitar la programació, prova i depuració del codi. |



## Mecanismes per al Manteniment de la Informació en Aplicacions Web

HTTP és un protocol **stateless**, sense estat. En les aplicacions web modernes, és essencial gestionar l'estat del client per proporcionar una experiència d'usuari fluida i personalitzada.
Per això, se simula l'estat mitjançant l'ús de cookies, tokens o la sessió. L'estat és necessari per a processos com ara el carret de la compra, operacions associades a un usuari, etc... 
A continuació es detallen diversos mecanismes per mantenir aquesta informació, així com els seus avantatges i desavantatges.

### Cookies

Les **cookies** són petits fitxers de text emmagatzemats al navegador de l'usuari. Són àmpliament utilitzades per mantenir l'estat del client entre sol·licituds HTTP, ja que HTTP és un protocol sense estat.

#### Avantatges de les Cookies

- **Persistència**: Les cookies poden mantenir-se durant períodes llargs definits per l'atribut `expires` o `max-age`.
- **Accessibilitat**: Es poden accedir des de qualsevol pàgina del mateix domini.
- **Simplicitat**: Fàcils d'implementar i gestionar.

#### Desavantatges de les Cookies

- **Seguretat**: Poden ser objectiu d'atacs com **XSS (Cross-Site Scripting)** si no es gestionen correctament.
- **Limitacions de mida**: Les cookies estan limitades a 4KB de dades.
- **Privadesa**: Les dades de l'usuari poden ser vulnerables si no es protegeixen adequadament.

#### Millors Pràctiques

- Utilitzar l'atribut `HttpOnly` per evitar l'accés a les cookies des de JavaScript.
- Configurar `SameSite` per prevenir atacs CSRF.
- Emmagatzemar únicament informació essencial i no sensible.

### Sessions

Les **sessions** són un mecanisme que permet associar dades a un usuari durant una sessió específica. Aquestes dades s'emmagatzemen al servidor, mentre que el client només guarda un identificador de sessió.

#### Avantatges de les Sessions

- **Seguretat**: Les dades sensibles es mantenen al servidor.
- **Capacitat d'emmagatzematge**: No limitades per la mida de les cookies.
- **Compartició de dades**: Facilita la compartició d'estat entre diferents components d'una aplicació web.

#### Desavantatges de les Sessions

- **Escalabilitat**: Requereix memòria addicional al servidor, la qual cosa pot ser problemàtica amb molts usuaris.
- **Persistència limitada**: Normalment només duren mentre el navegador està obert, tret que es configuri d'una altra manera.

#### Millors Pràctiques

- Emmagatzemar únicament referències o identificadors a la sessió.
- Utilitzar eines com Redis per a una gestió eficient de sessions en entorns escalables.

### Web Storage

El **Web Storage** proporciona dos mecanismes per emmagatzemar dades al navegador del client: `localStorage` i `sessionStorage`.

#### Avantatges del Web Storage

- **Capacitat**: `localStorage` pot emmagatzemar fins a 5-10MB de dades.
- **Persistència**: `localStorage` persisteix fins que s'elimina explícitament, mentre que `sessionStorage` persisteix durant la sessió de la pestanya.
- **Facilitat d'ús**: API simple per emmagatzemar i recuperar dades.

#### Desavantatges del Web Storage

- **Seguretat**: Les dades emmagatzemades són accessibles per JavaScript, la qual cosa les fa vulnerables a atacs XSS.
- **Compatibilitat**: No totes les característiques poden ser suportades per navegadors més antics.

#### Millors Pràctiques

- Utilitzar el `sessionStorage` per dades que no necessiten persistir entre pestanyes o sessions.
- Minimitzar l'emmagatzematge de dades sensibles i xifrar-les si cal.

### Tokens d'Autenticació

Els **JSON Web Tokens (JWT)** són un estàndard obert que defineix una manera compacta i autònoma d'enviar informació entre dues parts de manera segura com a objecte JSON. S'utilitzen habitualment per a l'autenticació en aplicacions web.

#### Avantatges dels JWT

- **Estatut autònom**: Porten tota la informació necessària, eliminant la necessitat de mantenir sessions al servidor.
- **Escalabilitat**: Milloren l'escalabilitat en aplicacions distribuïdes.
- **Seguretat**: Es poden signar digitalment per assegurar la seva autenticitat.

#### Desavantatges dels JWT

- **Revocació complexa**: Una vegada emesos, és difícil revocar-los sense mantenir una llista negra.
- **Sobrecarrega de dades**: Si els tokens són grans, poden afectar el rendiment, especialment en xarxes de baixa latència.

#### Millors Pràctiques

- Utilitzar signatura HS256 o RS256 per garantir la integritat del token.
- No emmagatzemar dades sensibles directament al token.

### Cache del Navegador

El **cache del navegador** s'utilitza per emmagatzemar còpies temporals de recursos web per millorar el rendiment i reduir la càrrega del servidor.

#### Avantatges del Cache

- **Rendiment**: Redueix el temps de càrrega dels recursos.
- **Optimització**: Disminueix l'ample de banda requerit.

#### Desavantatges del Cache

- **Consistència**: Pot servir dades obsoletes si no es gestiona correctament.
- **Control**: Requereix configuració per evitar el caching indesitjat de dades dinàmiques.

#### Millors Pràctiques

- Configurar els encapçalaments HTTP correctament (`Cache-Control`, `ETag`) per gestionar l'actualització de recursos.

### Sincronització Offline

La **sincronització offline** es refereix a la capacitat d'una aplicació web de funcionar sense connexió a Internet, sincronitzant dades quan es recupera la connexió.

#### Tècniques i Eines

- **IndexedDB**: Emmagatzema grans volums de dades estructurades dins del navegador.
- **Service Workers**: Gestionen peticions de xarxa, proporcionant funcionalitats offline i cache avançat.

#### Millors Pràctiques

- Gestionar conflictes de dades quan es torna a estar en línia.
- Utilitzar estratègies de sincronització optimitzades per minimitzar l'ample de banda i el temps de sincronització.

### Seguretat de les Cookies i Sessions

La **seguretat** és fonamental en la gestió de cookies i sessions per protegir les dades dels usuaris de possibles atacs.

#### Pràctiques de Seguretat

- **CSRF**: Utilitzar tokens CSRF per validar sol·licituds d'accions sensibles.
- **XSS**: Sanear les dades d'entrada i utilitzar capçaleres de seguretat (`Content-Security-Policy`) per prevenir XSS.
- **Secure Flag**: Marcar les cookies amb l'atribut `Secure` perquè només s'enviïn a través de connexions HTTPS.

#### Conclusió

La selecció del mecanisme adequat per al manteniment de l'estat en una aplicació web depèn de les necessitats específiques de l'aplicació, el volum de dades, els requisits de seguretat i l'arquitectura del sistema. Avaluar cada tècnica pel que fa a avantatges i desavantatges ajudarà a prendre decisions informades i construir aplicacions web més segures i eficients.


## Exemples de Cookies i Sessions en PHP

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

