# Programació web amb PHP

??? abstract "Duració i criteris d'avaluació"

    Duració estimada: 20 hores

    <hr />

    | Resultat d'aprenentatge | Criteris d'avaluació|
    | -------                 | -------             |
    | 2. Escriu sentències executables per un servidor Web reconeixent i aplicant procediments d'integració del codi en llenguatges de marques. | a) S'han reconegut els mecanismes de generació de pàgines Web a partir de llenguatges de marques amb codi embegut. <br/> b) S'han identificat les principals tecnologies associades.  <br/> c) S'han utilitzat etiquetes per a la inclusió de codi en el llenguatge de marques.  <br/> d) S'ha reconegut la sintaxi del llenguatge de programació que s'ha d'utilitzar.  <br/> e) S'han escrit sentències simples i s'ha comprovat els seus efectes en el document resultant.  <br/> f) S'han utilitzat directives per a modificar el comportament predeterminat.  <br/> g) S'han utilitzat els diferents tipus de variables i operadors disponibles en el llenguatge.  <br/> h) S'han identificat els àmbits d'utilització de les variables.  <br/> |
    | 3. Genera pàgines web de forma dinàmica seguint especificacions rebudes. | a) S'han identificat els mecanismes de separació de la lògica de negoci.<br/>b) S'han utilitzat tecnologies adequades per a la generació dinàmica de pàgines web.<br/>c) S'han utilitzat tècniques d'accés a dades.<br/>d) S'han generat pàgines web dinàmiques que compleixen amb les especificacions rebudes.<br/>e) S'ha comprovat el funcionament de les pàgines web generades.<br/>f) S'han seguit les convencions de format i codificació establertes. |
    | 4. Desenvolupa aplicacions Web embegudes en llenguatges de marques analitzant i incorporant funcionalitats segons especificacions | a) S'han identificat els mecanismes disponibles per al manteniment de la informació que concerneix un client web concret i s'han assenyalat els seus avantatges.<br /> b) S'han utilitzat mecanismes per a mantindre l'estat de les aplicacions web.<br /> c) S'han utilitzat mecanismes per a emmagatzemar informació en el client web i per a recuperar el seu contingut.<br /> d) S'han identificat i caracteritzat els mecanismes disponibles per a l'autenticació d'usuaris.<br /> e) S'han escrit aplicacions que integren mecanismes d'autenticació d'usuaris.<br /> f) S'han utilitzat eines i entorns per a facilitar la programació, prova i depuració del codi. |



## SA2.1.Introducció a PHP

#### Què és PHP?
**PHP** (Hypertext Preprocessor) és un llenguatge de programació de codi obert, especialment dissenyat per al desenvolupament web del costat del servidor. Es pot incrustar fàcilment en codi HTML, cosa que el fa una opció popular per crear aplicacions web dinàmiques i interactives. PHP s'utilitza per gestionar el contingut dinàmic, les bases de dades, el seguiment de sessions i fins i tot per crear aplicacions completes.

 
#### Importància en el desenvolupament web
PHP és un dels llenguatges més utilitzats en el desenvolupament web per diverses raons:

* **Facilitat d'aprenentatge:** PHP és relativament fàcil d'aprendre per als principiants en programació web. La seva sintaxi és senzilla i similar a altres llenguatges com C i Perl.
* **Gran comunitat i suport:** PHP té una gran comunitat de desenvolupadors que proporcionen suport, biblioteques, extensions i eines. A més, hi ha nombrosos recursos en línia, tutorials i documentació.
* **Integració amb bases de dades:** PHP es pot integrar fàcilment amb una àmplia varietat de bases de dades, cosa que el fa ideal per a aplicacions web basades en dades.
* **Flexibilitat i escalabilitat:** PHP és altament flexible i es pot utilitzar per desenvolupar tant aplicacions petites com projectes grans i complexos. També és escalable, cosa que permet gestionar un gran volum de trànsit.
* **Cost efectiu:** Com que és de codi obert, PHP és gratuït per utilitzar i distribuir. Això redueix els costos de desenvolupament per a les empreses i els desenvolupadors.

 
### 1. Llenguatges imbricats en HTML
PHP permet incrustar codi dins de documents HTML, permetent la generació de contingut dinàmic. El codi PHP es delimita amb `<?php ... ?>`.
És comú utilitzar codi PHP dins de HTML per generar contingut dinàmic. També es pot incloure HTML dins de fitxers PHP.
```php
<!DOCTYPE html>
<html>
<body>
    <h1>Benvingut a la meva web</h1>
    <p>La data d'avui és: <?= date('Y-m-d') ?></p>
</body>
</html>
```
El codi HTML pot ser generat dins d'instruccions PHP.
```php
<?php
echo "<html><body>";
echo "<h1>Benvingut a la meva web</h1>";
echo "<p>La data d'avui és: " . date('Y-m-d') . "</p>";
echo "</body></html>";
?>
```

!!! tip "Només etiquetes d'obertura"
    Si el nostre codi només contindrà codi PHP i res d'html, com per exemple, quan codifiquem classes o interfícies, només posarem l'etiqueta d'obertura, per a així indicar que és una arxiu de php pur.

### 2. Etiquetes per a inserció de codi
Per inserir codi PHP dins de HTML, utilitzem les etiquetes:
```php
<?php
// Codi PHP aquí
?>
```
Per imprimir directament:
```php
<?= $variable ?>
```
Exemple:
```php
<!DOCTYPE html>
<html>
<body>
    <h1>Benvingut a la meva web</h1>
    <p>La data d'avui és: <?= date('Y-m-d') ?></p>
</body>
</html>
```

### 3. Tipus de dades. Conversions entre tipus de dades
PHP té diversos tipus de dades: enter, flotant, cadena, booleà, matriu, objecte, nul.
```php
$enter = 10; // Enter
$flotant = 3.14; // Flotant
$cadena = "Hola, món!"; // Cadena
$boolea = true; // Booleà
$matriu = array(1, 2, 3); // Matriu
$objecte = new stdClass(); // Objecte
$nul = null; // Nul
```
Conversions:
```php
$integer = (int) $variable;
$float = (float) $variable;
$string = (string) $variable;
```
Exemple:
```php
$cadena = "123";
$enter = (int)$cadena; // Converteix la cadena "123" a l'enter 123
```
### 4. Constants
Són variables el valor dels quals no varien. Existeixen dues possibilitats:

* `define(NOMBRE, valor);`
* `const NOMBRE; // PHP > 5.3`

``` php
<?php
define("PI", 3.1416);
const IVA = 0.21;

echo PI, " ", IVA; // No se pone el símbolo dolar
```

* Es declaren sempre en MAJÚSCULES
* Hi ha un conjunt de constants ja predefinides, també conegudes com *magic constants*: <https://www.php.net/manual/es/language.constants.predefined.php>

### 5. Variables. Operadors.  Àmbits de les variables

* No és necessari declarar-les prèviament.
* Comencen per `$`, per exemple `$nom`. Després del `$`, el següent caràcter ha de ser una lletra en minúscula (recomanació) o guió baix `_`. Després ja es poden posar números.
* Són case *sensitive*: `$*var != $*vAR`
* No es declara el seu tipus, el tipat és dinàmic. S'assigna en temps d'execució depenent del valor assignat.
* Convenient inicialitzar-les, sinó donen error a l'utilitzar-les.
```php
$variable = "valor";
```
Operadors:
- Aritmètics: `+`, `-`, `*`, `/`
- Assignació: `=`, `+=`, `-=`
- Comparació: `==`, `===`, `!=`
- Lògics: `&&`, `||`, `!`
- Concatenació: `.`

Els àmbits d'utilització d'una variable són:

Local: dins d'una funció.
Global: fora de qualsevol funció.
Estàtic: persisteixen el seu valor entre crides a la funció.

 
Exemple:
   
Assignacions
```php
$x = 5;
$y = "Hola món";
```
Operacions aritmètiques
```php
$suma = $x + 10;  // Resulta en 15
$producte = $x * 2;  // Resulta en 10
```
Operacions d'entrada i eixida:
```php
echo "Hola, món!";
print "Hola, món!";
```
Operacions amb cadenes:
```php
$nom = "Joan";
$salutacio = $y . ", " . $nom;  // Resulta en "Hola món, Joan"
```
 

### 6. Funcions 

1. **Sintaxi bàsica**:
    - La paraula clau `function` es fa servir per a definir la funció.
    - Després segueix el nom de la funció, que pot contenir lletres, nombres i guions baixos (però no pot començar amb un nombre).
    - Entre els parèntesis es poden passar arguments (opcionals).
    - El cos de la funció es defineix entre claudàtors `{}`.

```php
function nomFuncio() {
    // Codi de la funció
}
```

2. **Amb arguments**:
    - Els arguments es passen entre els parèntesis i poden ser utilitzats dins de la funció.

```php
function saluda($nom) {
    echo "Hola, $nom!";
}

saluda("Maria");  // Mostra "Hola, Maria!"
```

3. **Amb valor de retorn**:
    - La paraula clau `return` permet retornar un valor des de la funció. Es pot retornar qualsevol tipus de dades (enter, string, array, etc.).

```php
function suma($a, $b) {
    return $a + $b;
}

$resultat = suma(5, 3);  // $resultat conté 8
```


4. **Funcions amb valors per defecte**:
    - Si no es passa cap argument, la funció pot utilitzar un valor per defecte.

```php
function saludar($nom = "amic") {
    echo "Hola, " . $nom;
}

saludar();  // Mostra "Hola, amic"
saludar("Maria");  // Mostra "Hola, Maria"
```

5. **Tipus de dades en arguments i retorn** (des de PHP 7):
    - És possible especificar el tipus de dades dels arguments i el tipus de retorn. Això ajuda a assegurar que la funció rep i retorna els tipus esperats.

```php
function sumar(int $a, int $b): int {
    return $a + $b;
}

$resultat = sumar(5, 3);  // $resultat conté 8
```


### 7. Directives per a modificar el comportament predeterminat del codi

Include i require:
```php
include 'fitxer.php';
require 'fitxer.php';
```
Include_once i require_once:
```php
include_once 'fitxer.php';
require_once 'fitxer.php';
```
Exemple:
```php
// contingut de fitxer.php
<?php
function saludar() {
    echo "Hola!";
}
?>

// contingut de principal.php
<?php
include 'fitxer.php';
saludar(); // Mostra "Hola!"
?>
```
 
### 8. Mecanismes de decisió (if, switch)
If, else, elseif:
```php
if ($condicio) {
    // Codi si la condició és certa
} elseif ($altra_condicio) {
    // Codi si la segona condició és certa
} else {
    // Codi si cap de les condicions anteriors és certa
}
```
Switch:
```php
switch ($variable) {
    case 1:
        // Codi per al cas 1
        break;
    case 2:
        // Codi per al cas 2
        break;
    default:
        // Codi per al cas per defecte
}
```
Exemple:
```php
$dia = "dilluns";
switch ($dia) {
    case "dilluns":
        echo "Avui és dilluns";
        break;
    case "dimarts":
        echo "Avui és dimarts";
        break;
    default:
        echo "Avui no és dilluns ni dimarts";
}
```
Match: 
```php
$result = match ($variable) {
    valor1 => resultat1,
    valor2 => resultat2,
    valor3 => resultat3,
    // ...
    default => valorPerDefecte,
};
```
**Diferències amb switch**

    1. **Comparació estricta**: `match` utilitza comparació estricta (===) per comparar els valors.
    2. **Retorna un valor**: `match` és una expressió, la qual cosa significa que retorna un valor.
    3. **No necessita break**: A diferència de `switch`, no es necessita l'ús de `break` per evitar la caiguda (fall-through).
    4. **Més concís**: Permet una sintaxi més neta i concisa.

Exemple simple:
```php
$color = 'roig';

$resultat = match ($color) {
    'roig' => 'El color és vermell',
    'blau' => 'El color és blau',
    'verd' => 'El color és verd',
    default => 'Color desconegut',
};

echo $resultat;  // Sortida: El color és vermell
```
Exemple expressions complexes:
```php
$edat = 20;

$categoria = match (true) {
    $edat >= 0 && $edat <= 12 => 'Nen',
    $edat >= 13 && $edat <= 17 => 'Adolescent',
    $edat >= 18 && $edat <= 64 => 'Adult',
    $edat >= 65 => 'Gent gran',
    default => 'Edat desconeguda',
};

echo $categoria;  // Sortida: Adult
```
Exemples casos multiples:
```php
$dia = 'dimecres';

$tipusDia = match ($dia) {
    'dissabte', 'diumenge' => 'Cap de setmana',
    'dilluns', 'dimarts', 'dimecres', 'dijous', 'divendres' => 'Dia laborable',
    default => 'Dia desconegut',
};
echo $tipusDia;  // Sortida: Dia laborable
```

### 9. Bucles (for, while, foreach)
For:
```php
for ($i = 0; $i < 10; $i++) {
    echo $i;
}
```
While:
```php
$i = 0;
while ($i < 10) {
    echo $i;
    $i++;
}
```
Foreach:
```php
$matriu = array(1, 2, 3);
foreach ($matriu as $valor) {
    echo $valor;
}
```
Exemple:
```php
$fruites = array("poma", "plàtan", "maduixa");
foreach ($fruites as $fruita) {
    echo $fruita;
}
```

### 10. Arrays

Per a emmagatzemar dades compostes, podem utilitzar tant arrays senzills com arrays associatius (similars a un mapa). En realitat tots els arrays són mapes ordenats compostos de parells clau-valor.

!!! caution "Compte amb mesclar tipus"
    Com el tipat és dinàmic, nostres arrays poden contenir dades de diferents tipus. No es recomana mesclar els tipus.

De la mateixa manera que Java, es defineixen mitjançant claudàtors, són 0-index, i es pot assignar un valor a un posició determinada:

``` php
<?php
$frutas = array("naranja", "pera", "manzana");

$frutas2 = ["naranja", "pera", "manzana"];

$frutas3 = [];
$frutas3[0] = "naranja";
$frutas3[1] = "pera";
$frutas3[] = "manzana"; // lo añade al final
```

Podem obtindre la grandària del array mitjançant la funció `count(array)`. Per a recórrer el array farem ús d'un bucle `for`:

``` php
<?php
$tam = count($frutas); // tamaño del array

for ($i=0; $i<count($frutas); $i++) {
    echo "Elemento $i: $frutas[$i] <br />";
}
```

Una altra manera de recórrer els arrays, fins i tot més elegant, és fer ús de `foreach`. La seua sintaxi és `foreach (array as element)`:

``` php
<?php
// Mitjançant foreach no necessitem saber la grandària del array
foreach ($frutas as $fruta) {
    echo "$fruta <br />";
}
```

### 11. Arrays associatius

Cada element és un parell clau-valor. En comptes d'accedir per la posició, el fem mitjançant una clau. Així doncs, per a cada clau s'emmagatzema un valor.

A l'hora de recórrer aquest tipus de arrays, mitjançant `foreach` separem cada element en una parella `clau => valor`:

``` php
<?php
$capitales = ["Italia" => "Roma",
    "Francia" => "Paris",
    "Portugal" => "Lisboa"];
$capitalFrancia = $capitales["Francia"]; // se accede al elemento por la clave, no la posición

$capitales["Alemania"] = "Berlín"; // añadimos un elemento

echo "La capital de Francia es $capitalFrancia <br />";
echo "La capital de Francia es {$capitales["Francia"]} <br />";

$capitales[] = "Madrid"; // se añade con la clave 0 !!! ¡¡¡No asignar valores sin clave!!!

foreach ($capitales as $valor) { // si recorremos un array asociativo, mostraremos los valores
    echo "$valor <br />";
}

foreach ($capitales as $pais => $ciudad) { // separamos cada elemento en clave => valor
    echo "$pais : $ciudad <br />";
}
```

### 12. Com utilitzar les cometes en PHP

En PHP, les cometes dobles (`"`) i les cometes simples (`'`) s'utilitzen per definir cadenes de caràcters, però tenen comportaments diferents a l'hora de processar variables:

- **Cometes dobles (`"`)**: Interpolen variables i seqüències d'escapament especials. És a dir, el contingut de la variable es mostrarà dins de la cadena.

  ```php
  $nom = "Maria";
  echo "Hola, $nom!";  // Sortida: Hola, Maria!
  ```

- **Cometes simples (`'`)**: No interpolen variables ni seqüències d'escapament especials. La cadena es mostrarà exactament com es defineix.

  ```php
  $nom = "Maria";
  echo 'Hola, $nom!';  // Sortida: Hola, $nom!
  ```

#### Exemple d'ús de cometes dobles per imprimir variables

```php
$color = "blau";
$frase = "El meu color preferit és $color.";
echo $frase;  // Sortida: El meu color preferit és blau.
  ```

### 13. Comentaris en el codi
Comentaris d'una línia:
```php
// Això és un comentari d'una línia
```
Comentaris de diverses línies:
```php
/* Això és un comentari
   de diverses línies */
```
### 14. Variables de servidor

PHP emmagatzema la informació del servidor i de les peticions HTTP en sis arrays globals:

* `$_ENV`: informació sobre les variables d'entorn
* `$_GET`: paràmetres enviats en la petició GET
* `$_POST`: paràmetres enviats en el envio POST
* `$_COOKIE`: conté les cookies de la petició, les claus del array són els noms de les cookies
* `$_SERVER`: informació sobre el servidor
* `$_FILES`: informació sobre els fitxers carregats via upload

Si ens centrem en el array `$_SERVER` podem consultar les següents propietats:

* `PHP_SELF`: nom del script executat, relatiu al document root (p.ej: `/tenda/carret.php`)
* `SERVER_SOFTWARE`: (p.ej: Apatxe)
* `SERVER_NAME`: domini, àlies DNS (p.ej: `www.elche.es`)
* `REQUEST_METHOD`: GET
* `REQUEST_URI`: URI, sense el domini
* `QUERY_STRING`: tot el que va després de `?` en la URL (p.ej: `heroe=Batman&nomene=Bruce`)

Més informació en <https://www.php.net/manual/es/reserved.variables.server.php>

``` php
<?php
echo $_SERVER["PHP_SELF"]."<br>"; // /u4/401server.php
echo $_SERVER["SERVER_SOFTWARE"]."<br>"; // Apache/2.4.46 (Win64) OpenSSL/1.1.1g PHP/7.4.9
echo $_SERVER["SERVER_NAME"]."<br>"; // localhost

echo $_SERVER["REQUEST_METHOD"]."<br>"; // GET
echo $_SERVER["REQUEST_URI"]."<br>"; // /u4/401server.php?heroe=Batman
echo $_SERVER["QUERY_STRING"]."<br>"; // heroe=Batman
```

Altres propietats relacionades:

* `PATH_INFO`: ruta extra després de la petició. Si la URL és `http://www.php.com/php/pathinfo.php/algo/cosa?foo=bar`, llavors `$_SERVER['PATH_INFO']` serà `/alguna cosa/cosa`.
* `REMOTE_HOST`: hostname que va fer la petició
* `REMOTE_ADDR`: IP del client
* `AUTH_TYPE`: tipus d'autenticació (p.ej: Basic)
* `REMOTE_USER`: nom de l'usuari autenticat

Apatxe crea una clau per a cada capçalera HTTP, en majúscules i substituint els guions per subratllats:

* `HTTP_USER_AGENT`: agent (navegador)
* `HTTP_REFERER`: pàgina des de la qual es va fer la petició


``` php
<?php
echo $_SERVER["HTTP_USER_AGENT"]."<br>"; // Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.88 Safari/537.36
```

### 15. Formularis

A l'hora d'enviar un formulari, hem de tindre clar quan usar GET o POST

* GET: els paràmetres es passen en la URL
    * <2048 caràcters, només ASCII
    * Permet emmagatzemar la direcció completa (marcador / historial)
    * Idempotent: dues crides amb les mateixes dades sempre ha de donar el mateix resultat
    * El navegador pot cachejar les cridades

* POST: paràmetres ocults (no encriptats)
    * Sense límit de dades, permet dades binàries.
    * No es poden escorcollar
    * No idempotent → actualitzar la BBDD

Així doncs, per a recollir les dades accedirem al array depenent del mètode del formulari que ens ha invocat:

``` php
<?php
$par = $_GET["parametro"]
$par = $_POST["parametro"]
```

A l'hora d'enviar un formulari, hem de tindre clar quan usar GET o POST. Per als següents apartats ens basarem en el següent exemple:


### Validació

Respecte a la validació, és convenient sempre fer *validació doble*:

* En el client mitjançant JS
* En servidor, abans de cridar a la capa de negoci, és convenient tornar a validar les dades.

``` php
<?php
if (isset($_GET["parametro"])) {
    $par = $_GET["parametro"];
    // comprobar si $par tiene el formato adecuado, su valor, etc...
}
```

!!! info "Llibreries de validació"
Existeixen diverses llibreries que faciliten la validació dels formularis, com són [respect/validation](https://respect-validation.readthedocs.io/en/latest/) o [particle/validator](http://validator.particle-php.com/en/latest/).
Quan estudiem Laravel aprofundirem en la validació de manera declarativa.

### Parámetre multivalor

Existeixen elements HTML que envien diversos valors:

* `select multiple`
* `checkbox`

Per a recollir les dades, el nom de l'element ha de ser un array.

``` html
<select name="lenguajes[]" multiple="true">
    <option value="c">C</option>
    <option value="java">Java</option>
    <option value="php">PHP</option>
    <option value="python">Python</option>
</select>

<input type="checkbox" name="lenguajes[]" value="c" /> C<br />
<input type="checkbox" name="lenguajes[]" value="java" /> Java<br />
<input type="checkbox" name="lenguajes[]" value="php" /> Php<br />
<input type="checkbox" name="lenguajes[]" value="python" /> Python<br />
```

De manera que després en recollir les dades:

``` php
<?php
$lenguajes = $_GET["lenguajes"];

foreach ($lenguajes as $lenguaje) {
    echo "$lenguaje <br />";
}
```

### Tornant a emplenar un formulari

Un *sticky form* és un formulari que recorda els seus valors. Per a això, hem d'emplenar els atributs `value` dels elements HTML amb la informació que contenien:

``` html+php
<?php
if (!empty($_POST['modulos']) && !empty($_POST['nombre'])) {
  // Aquí se incluye el código a ejecutar cuando los datos son correctos
} else {
  // Generamos el formulario
  $nombre = $_POST['nombre'] ?? "";
  $modulos = $_POST['modulos'] ?? [];
  ?>
  <form action="<?php echo $_SERVER['PHP_SELF'];?>" method="POST">
   <p><label for="nombre">Nombre del alumno:</label>
    <input type="text" name="nombre" id="nombre" value="<?= $nombre ?>" /> 
   </p>
   <p><input type="checkbox" name="modulos[]" id="modulosDWES" value="DWES"
    <?php if(in_array("DWES",$modulos)) echo 'checked="checked"'; ?> />
    <label for="modulosDWES">Desarrollo web en entorno servidor</label>
   </p>
   <p><input type="checkbox" name="modulos[]" id="modulosDWEC" value="DWEC"
    <?php if(in_array("DWEC",$modulos)) echo 'checked="checked"'; ?> />
    <label for="modulosDWEC">Desarrollo web en entorno cliente</label>
   </p>
   <input type="submit" value="Enviar" name="enviar"/>
  </form>
<?php } ?>
```

### Pujant arxius

S'emmagatzemen en el servidor en el array `$_FILES` amb el nom del camp del tipus `file` del formulari.

``` html
<form enctype="multipart/form-data" action="<?php echo $_SERVER['PHP_SELF']; ?>"  method="POST">
    Archivo: <input name="archivoEnviado" type="file" />
    <br />
    <input type="submit" name="btnSubir" value="Subir" />
</form>
```

Configuració en `php.ini`

* `file_uploads`: on / off
* `upload_max_filesize`: 2M
* `upload_tmp_dir`: directori temporal. No és necessari configurar-ho, agafarà el predeterminat del sistema
* `post_max_size`: grandària màxima de les dades POST. Ha de ser major a upload_max_filesize.
* `max_file_uploads`: nombre màxim d'arxius que es poden carregar alhora.
* `max_input_estafe`: temps màxim emprat en la càrrega (GET/POST i upload → normalment es configura en 60)
* `memory_limit`: 128M
* `max_execution_estafe`: temps d'execució d'un script (no té en compte el upload)

Per a carregar els arxius, accedim al array `$_FILES`:

``` php
<?php
if (isset($_POST['btnSubir']) && $_POST['btnSubir'] == 'Subir') {
    if (is_uploaded_file($_FILES['archivoEnviado']['tmp_name'])) {
        // subido con éxito
        $nombre = $_FILES['archivoEnviado']['name'];
        move_uploaded_file($_FILES['archivoEnviado']['tmp_name'], "./uploads/{$nombre}");

        echo "<p>Archivo $nombre subido con éxito</p>";
    }
}
```

Cada arxiu carregat en `$_FILES` té:

* `name`: nom
* `tmp_name`: ruta temporal
* `size`: grandària en bytes
* `type`: tipus ACARONE
* `error`: si hi ha error, conté un missatge. Si ok → 0.

## SA2.2 Mecanismes per al Manteniment de la Informació en Aplicacions Web
 
### 1. Fonaments 

HTTP és un protocol **stateless**, sense estat. En les aplicacions web modernes, és essencial gestionar l'estat del client per proporcionar una experiència d'usuari fluida i personalitzada.
Per això, se simula l'estat mitjançant l'ús de cookies, tokens o la sessió. L'estat és necessari per a processos com ara el carret de la compra, operacions associades a un usuari, etc...
A continuació es detallen diversos mecanismes per mantenir aquesta informació, així com els seus avantatges i desavantatges.

#### Cookies

Les **cookies** són petits fitxers de text emmagatzemats al navegador de l'usuari. Són àmpliament utilitzades per mantenir l'estat del client entre sol·licituds HTTP, ja que HTTP és un protocol sense estat.

##### Avantatges de les Cookies

- **Persistència**: Les cookies poden mantenir-se durant períodes llargs definits per l'atribut `expires` o `max-age`.
- **Accessibilitat**: Es poden accedir des de qualsevol pàgina del mateix domini.
- **Simplicitat**: Fàcils d'implementar i gestionar.

##### Desavantatges de les Cookies

- **Seguretat**: Poden ser objectiu d'atacs com **XSS (Cross-Site Scripting)** si no es gestionen correctament.
- **Limitacions de mida**: Les cookies estan limitades a 4KB de dades.
- **Privadesa**: Les dades de l'usuari poden ser vulnerables si no es protegeixen adequadament.

 
#### Sessions

Les **sessions** són un mecanisme que permet associar dades a un usuari durant una sessió específica. Aquestes dades s'emmagatzemen al servidor, mentre que el client només guarda un identificador de sessió.

##### Avantatges de les Sessions

- **Seguretat**: Les dades sensibles es mantenen al servidor.
- **Capacitat d'emmagatzematge**: No limitades per la mida de les cookies.
- **Compartició de dades**: Facilita la compartició d'estat entre diferents components d'una aplicació web.

##### Desavantatges de les Sessions

- **Escalabilitat**: Requereix memòria addicional al servidor, la qual cosa pot ser problemàtica amb molts usuaris.
- **Persistència limitada**: Normalment només duren mentre el navegador està obert, tret que es configuri d'una altra manera.

 
#### Web Storage

El **Web Storage** és una API del navegador que permet emmagatzemar dades al client de manera més senzilla i amb més capacitat que les cookies tradicionals. Inclou dos mecanismes principals: `localStorage` i `sessionStorage`.

##### Característiques del Web Storage

- **`localStorage`**: Permet emmagatzemar dades que persisteixen fins que s'elimina explícitament, fins i tot després de tancar el navegador.
- **`sessionStorage`**: Les dades es mantenen només durant la sessió del navegador i s'esborren quan es tanca la pestanya o finestra.

##### Avantatges

- **Capacitat d'Emmagatzematge**: Ofereix més espai (fins a 5-10MB) que les cookies.
- **API Simple**: Proporciona una interfície senzilla per emmagatzemar i recuperar dades.

##### Usos Comuns

- **Manteniment de l'Estat del Client**: Pot guardar dades de sessió i preferències de l'usuari que no cal enviar al servidor.
- **Sincronització amb l'Entorn Servidor**: Es pot utilitzar per emmagatzemar dades que després es sincronitzen amb el servidor, millorant el rendiment i l'experiència d'usuari.

##### Consideracions de Seguretat

- **Accessibilitat**: Les dades són accessibles per JavaScript, per la qual cosa s'ha de tenir cura amb les vulnerabilitats XSS.
- **Dades Sensibles**: Evita emmagatzemar dades sensibles o confidencials.

Tot i que **Web Storage** s'executa al costat del client, entendre les seves funcionalitats pot ajudar els desenvolupadors del servidor a dissenyar sistemes més robustos i eficaços, on la cooperació entre client i servidor maximitza l'eficiència de l'aplicació web.

#### Tokens d'Autenticació

Els **JSON Web Tokens (JWT)** són un estàndard obert que defineix una manera compacta i autònoma d'enviar informació entre dues parts de manera segura com a objecte JSON. S'utilitzen habitualment per a l'autenticació en aplicacions web.

##### Avantatges dels JWT

- **Estatut autònom**: Porten tota la informació necessària, eliminant la necessitat de mantenir sessions al servidor.
- **Escalabilitat**: Milloren l'escalabilitat en aplicacions distribuïdes.
- **Seguretat**: Es poden signar digitalment per assegurar la seva autenticitat.

##### Desavantatges dels JWT

- **Revocació complexa**: Una vegada emesos, és difícil revocar-los sense mantenir una llista negra.
- **Sobrecarrega de dades**: Si els tokens són grans, poden afectar el rendiment, especialment en xarxes de baixa latència.

 
#### Cache del Navegador

El **cache del navegador** s'utilitza per emmagatzemar còpies temporals de recursos web per millorar el rendiment i reduir la càrrega del servidor.

##### Avantatges del Cache

- **Rendiment**: Redueix el temps de càrrega dels recursos.
- **Optimització**: Disminueix l'ample de banda requerit.

##### Desavantatges del Cache

- **Consistència**: Pot servir dades obsoletes si no es gestiona correctament.
- **Control**: Requereix configuració per evitar el caching indesitjat de dades dinàmiques.

 
### 2. Cookies i Sessions en PHP

#### Cookies

Les cookies s'emmagatzemen en el array global `$_COOKIE`. El que col·loquem dins del array, es guardarà en el client. Cal tindre present que el client pot no voler emmagatzemar-les.

Existeix una limitació de 20 cookies per domini i 300 en total en el navegador.

En PHP, per a crear una cookie s'utilitza la funció `setcookie`:

``` php
<?php
setcookie(
    'nom_cookie',
    'valor_cookie',
    [
        'expires' => time() + 3600, // 1 hora
        'path' => '/',
        'domain' => '', // Domini actual
        'secure' => true, // Només HTTPS
        'httponly' => true, // Només accessible via HTTP
        'samesite' => 'Lax' // o 'Strict' o 'None'
    ]
);
?>
```
Destacar que el nom no pot contindre espais ni el caràcter `;`. Respecte al contingut de la cookie, no pot superar els 4 KB.

##### Consideracions de seguretat per a cookies:

**HTTPOnly**: Assegura't que les cookies que contenen informació sensible no siguin accessibles per JavaScript utilitzant l'atribut HttpOnly.

**Secure**: Utilitza l'atribut Secure per assegurar que les cookies només es transmeten en connexions HTTPS.

**SameSite**: Defineix correctament l'atribut SameSite per a prevenir atacs CSRF (Cross-Site Request Forgery).


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

#### Sessió

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
session_regenerate_id(true); // regenera el id
session_id() // devuelve el id
$_SESSION[clave] = valor; // inserción
session_destroy(); // destruye la sesión
unset($_SESSION[clave]; // borrado
```

Veurem mitjançant un exemple com podem inserir en un pàgina dades en la sessió per a posteriorment en una altra pàgina accedir a aqueixes dades. Per exemple, en `sesion.php` tindríem

``` php
<?php
// Iniciar sessió
session_start();
session_regenerate_id(true);

// Establir valors de sessió
$_SESSION['usuari'] = 'JohnDoe';
$_SESSION['rol'] = 'admin';

?>

```

I posteriorment podem accedir a la sessió en `sesion1.php`:

``` php
<?php
session_start();
// Recuperar valors de sessió
echo 'Usuari: ' . $_SESSION['usuari'] . '<br>';
echo 'Rol: ' . $_SESSION['rol'] . '<br>';

// Tancar sessió de forma segura
session_unset();  // Eliminar totes les variables de sessió
session_destroy();  // Destruir la sessió
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

##### Serialització en PHP

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

##### Utilitzant serialització amb Sessions
Les sessions en PHP permeten emmagatzemar informació d'usuari per ser utilitzada en diverses pàgines. Pot ser útil serialitzar dades per a emmagatzemar-les en una sessió:

Iniciant una sessió i emmagatzemant dades serialitzades:

``` php
session_start();
session_regenerate_id(true);

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

### 3. Autenticació d'usuaris

#### Mecanismes d'Autenticació d'Usuaris

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
 `
## SA2.3 POO

#### 1. Introducció de la POO en php

PHP segueix un paradigma de programació orientada a objectes (POO) basada en classes.

Un classe és un plantilla que defineix les propietats i mètodes per a poder crear objectes. D'aquest manera, un objecte és una instància d'una classe.

Tant les propietats com els mètodes es defineixen amb una visibilitat (qui pot accedir)

* Privat - `private`: Només pot accedir la pròpia classe.
* Protegit - `protected`: Només pot accedir la pròpia classe o els seus descendents.
* Público - `public`: Pot accedir qualsevol altra classe.

Per a declarar una classe, s'utilitza la paraula clau `class` seguit del nom de la classe. Per a instanciar un objecte a partir de la classe, s'utilitza `new`:

``` php
<?php
class NomClase {
// propiedades
// y métodos
}

$ob = new NomClase();
```

!!! important "Classes amb majúscula"
Totes les classes comencen per lletra majúscula.

Quan un projecte creix, és normal modelar les classes mitjançant UML (recordeu Entorns de Desenvolupament?). La classes es representen mitjançant un quadrat, separant el nom, de les propietats i els mètodes:

![UML](imagenes/03/uml.png){ width=500 }

Una vegada que hem creat un objecte, s'utilitza l'operador `->` per a accedir a una propietat o un mètode:

``` php
$objeto->propiedad;
$objeto->método(parámetros);
```

Si des de dins de la classe, volem accedir a una propietat o mètode de la mateixa classe, utilitzarem la referència `$this`;

``` php
$this->propiedad;
$this->método(parámetros);  
```

Així doncs, com a exemple, codificaríem una persona en el fitxer `Persona.php` com:

``` php
<?php
class Persona {
    private string $nombre;

    public function setNombre(string $nom) {
        $this->nombre=$nom;
    }

    public function imprimir(){
        echo $this->nombre;
        echo '<br>';
    }
}

$bruno = new Persona(); // creamos un objeto
$bruno->setNombre("Bruno Díaz");
$bruno->imprimir();
```

Encara que es poden declarar diverses classes en el mateix arxiu, és una mala pràctica. Així doncs, cada fitxer contedrá una sola classe, i es nomenarà amb el nom de la classe.

### 2. Principis de la POO

### Encapsulació

Les propietats es defineixen privades o protegides (si volem que les classes heretades puguen accedir).

Per a cada propietat, s'afigen mètodes públics (*getter/setter*):

``` php
public setPropiedad(tipo $param)
public getPropiedad() : tipo
```

Les constants es defineixen públiques perquè siguen accessibles per tots els recursos.

``` php
<?php
class MayorMenor {
    private int $mayor;
    private int $menor;

    public function setMayor(int $may) {
        $this->mayor = $may;
    }

    public function setMenor(int $men) {
        $this->menor = $men;
    }

    public function getMayor() : int {
        return $this->mayor;
    }

    public function getMenor() : int {
        return $this->menor;
    }
}
```

#### Rebent i enviant objectes

És recomanable indicar-ho en la mena de paràmetres. Si l'objecte pot retornar nuls es posa `?` davant del nom de la classe.

!!! important "Objectes per referència"
Els objectes que s'envien i reben com a paràmetres sempre es passen per referència.

``` php hl_lines="2"
<?php
function maymen(array $numeros) : ?MayorMenor {
    $a = max($numeros);
    $b = min($numeros);

    $result = new MayorMenor();
    $result->setMayor($a);
    $result->setMenor($b);

    return $result;
}

$resultado =  maymen([1,76,9,388,41,39,25,97,22]);
echo "<br>Mayor: ".$resultado->getMayor();
echo "<br>Menor: ".$resultado->getMenor();
```

#### Constructor

El constructor dels objectes es defineix mitjançant el mètode màgic `__construct`.
Pot o no tindre paràmetres, però només pot haver-hi un únic constructor.
 
Una de les grans novetats que ofereix PHP 8 és la simplificació dels constructors amb paràmetres, la qual cosa es coneix com a promoció de les propietats del constructor*.

Per a això, en comptes d'haver de declarar les propietats com a privades o protegides, i després dins del constructor haver d'assignar els paràmetres a estàs propietats, el propi constructor promociona les propietats.

Vegem-ho millor amb un exemple. Imaginem una classe `Punt` on vulguem emmagatzemar les seues coordenades:

``` php
<?php
class Punto {
    protected float $x;
    protected float $y;
    protected float $z;

    public function __construct(
        float $x = 0.0,
        float $y = 0.0,
        float $z = 0.0
    ) {
        $this->x = $x;
        $this->y = $y;
        $this->z = $z;
    }
}
```

En PHP 8, quedaria de la següent manera (molt més curt, la qual cosa facilita la seua llegibilitat):

``` php
<?php
class Punto {
    public function __construct(
        protected float $x = 0.0,
        protected float $y = 0.0,
        protected float $z = 0.0,
    ) {}
}
```

!!! info "L'ordre importa"
A l'hora de codificar l'ordre dels elements ha de ser:

    ``` php
    <?php
    declare(strict_types=1);

    class NombreClase {
        // propiedades

        // constructor

        // getters - setters

        // resto de métodos
    }
    ?>
    ```

#### Classes estàtiques

Són aquelles que tenen propietats i/o mètodes estàtics (també es coneixen com *de classe*, perquè el seu valor es comparteix entre totes les instàncies de la mateixa classe).

Es declaren amb `static` i es referencien amb `::`.

* Si volem accedir a un mètode estàtic, s'anteposa el nom de la classe: `Producte::nuevoProducto()`.
* Si des d'un mètode volem accedir a una propietat estàtica de la mateixa classe, s'utilitza la referència `self`: `self::$numProductos`

``` php
<?php
class Producto {
    const IVA = 0.23;
    private static $numProductos = 0; 

    public static function nuevoProducto() {
        self::$numProductos++;
    }
}

Producto::nuevoProducto();
$impuesto = Producto::IVA;
```

També podem tindre classes normals que tinguen alguna propietat estàtica:

``` php
<?php
class Producto {
    const IVA = 0.23;
    private static $numProductos = 0; 
    private $codigo;

    public function __construct(string $cod) {
        self::$numProductos++;
        $this->codigo = $cod;
    }

    public function mostrarResumen() : string {
        return "El producto ".$this->codigo." es el número ".self::$numProductos;
    }
}

$prod1 = new Producto("PS5");
$prod2 = new Producto("XBOX Series X");
$prod3 = new Producto("Nintendo Switch");
echo $prod3->mostrarResumen();
```

  
#### Mètodes encadenats

Segueix el plantejament de la programació funcional, i també es coneix com *method chaining*. Planteja que sobre un objecte es realitzen diverses crides.

``` php
<?php
$p1 = new Libro();
$p1->setNombre("Harry Potter");
$p1->setAutor("JK Rowling");
echo $p1;

// Method chaining
$p2 = new Libro();
$p2->setNombre("Patria")->setAutor("Aramburu");
echo $p2;
```

Per a facilitar-ho, modificarem tots els seus mètodes mutants (que modifiquen dades, setters*, ...) perquè retornen una referència a `$this`:

``` php
<?php
class Libro {
    private string $nombre;
    private string $autor;

    public function getNombre() : string {
        return $this->nombre;
    }
    public function setNombre(string $nombre) : Libro { 
        $this->nombre = $nombre;
        return $this;
    }

    public function getAutor() : string {
        return $this->autor;
    }
    public function setAutor(string $autor) : Libro {
        $this->autor = $autor;
        return $this;
    }

    public function __toString() : string {
        return $this->nombre." de ".$this->autor;
    }
}
```

#### Mètodes màgics

Totes les classes PHP ofereixen un conjunt de mètodes, també coneguts com *magic methods* que es poden sobreescriure per a substituir el seu comportament. Alguns d'ells ja els hem utilitzats.

Davant qualsevol dubte, és convenient consultar la [documentació oficial](https://www.php.net/manual/es/language.oop5.magic.php).

Els més destacables són:

* `__construct()`
* `__destruct()` → s'invoca en perdre la referència. S'utilitza per a tancar una connexió a la BD, tancar un fitxer, ...
* `__toString()` → representació de l'objecte com a cadena. És a dir, quan fem `echo $objecte` s'executa automàticament aquest mètode.
* `__get(propietat)`, `__set(propietat, valor)` → Permetria accedir a les propietat privades, encara que sempre és més llegible/mantenible codificar els *getter/setter*.
* `__isset(propietat)`, `__unset(propietat)` → Permet esbrinar o llevar el valor a una propietat.
* `__sleep()`, `__wakeup()` → S'executen en recuperar (*unserialize^) o emmagatzemar un objecte que se serialitza (*serialize), i s'utilitzen per a permet definir quines propietats se serialitzen.
* `__call()`, `__callStatic()` → S'executen en cridar a un mètode que no és públic. Permeten sobrecarreguen mètodes.

 
## 3. Espai de noms

Des de PHP 5.3 i també coneguts com *Namespaces*, permeten organitzar les classes/interfícies, funcions i/o constants de manera similar als paquets a *Java*.

!!! tip "Recomanació"
Un només namespace per arxiu i crear una estructura de carpetes respectant els nivells/subnivells (igual que es fa a Java)

Es declaren en la primera línia mitjançant la paraula clau `namespace` seguida del nom de l'espai de noms assignat (cada subnivell se separa amb la barra invertida `\`):

Per exemple, per a col·locar la classe `Producte` dins del *namespace* `Dwes\Exemples` ho faríem així:

``` php
<?php
namespace Dwes\Exemples;

const IVA = 0.21;

class Producte {
    public $nombre;
      
    public function muestra() : void {
        echo"<p>Prod:" . $this->nombre . "</p>";
    }
}
```

#### Accés

Per a referenciar a un recurs que conté un namespace, primer hem de tindre'l disponible fent ús de `include` o `require`. Si el recurs està en el mateix *namespace*, es realitza un accés directe (es coneix com a accés sense qualificar).

Realment hi ha tres tipus d'accés:

* sense qualificar: `recurs`
* qualificat: `rutaRelativa\recurs` → no fa falta posar el *namespace* complet
* totalment qualificat: `\rutaAbsoluta\recurs`

``` php
<?php
namespace Dwes\Ejemplos;

include_once("Producto.php");

echo IVA; // sin cualificar
echo Utilidades\IVA; // acceso cualificado. Daría error, no existe \Dwes\Ejemplos\Utilidades\IVA
echo \Dwes\Ejemplos\IVA; // totalmente cualificado

$p1 = new Producto(); // lo busca en el mismo namespace y encuentra \Dwes\Ejemplos\Producto
$p2 = new Model\Producto(); // daría error, no existe el namespace Model. Está buscando \Dwes\Ejemplos\Model\Producto
$p3 = new \Dwes\Ejemplos\Producto(); // \Dwes\Ejemplos\Producto
```
 
Per a evitar la referència qualificada podem declarar l'ús mitjançant `use` (similar a fer `import` a Java). Es fa en la capçalera, després del `namespace`:

Els tipus Posibles són:

* `use const nombreCualificadoConstante`
* `use function nombreCualificadoFuncion`
* `use nombreCualificadoClase`
* `use nombreCualificadoClase as NuevoNombre` // per a canviar de nom elements

Per exemple, si volem utilitzar la classe `\Dwes\Exemples\Producte` des d'un recurs que es troba en l'arrel, per exemple en `inici.php`, faríem:

``` php
<?php
include_once("Dwes\Exemples\Producte.php");

use const Dwes\Exemples\IVA;
use \Dwes\Exemples\Producte;

echo IVA;
$p1 = new Producte();
```

!!! tip "To `use` or not to `use`"
En resum, `use` permet accedir sense qualificar a recursos que estan en un altre *namespace*. Si estem en el mateix espai de nom, no necessitem `use`.

#### Organització

Tot projecte, conforme creix, necessita organitzar el seu codi font. Es planteja una organització en la qual els arxius que interactuan amb el navegador es col·loquen en l'arrel, i les classes que definim van dins d'un namespace (i dins de la seua pròpia carpeta `src` o `app`).

<figure>
<img src="imagenes/03/03organizacion.png">
<figcaption>Organització del codi font</figcaption>
</figure>

!!! tip "Organització, includes i usos"
* Col·locarem cada recurs en un fitxer a part.
* En la primera línia indicarem la seua *namespace* (si no està en l'arrel).
* Si utilitzem altres recursos, farem un `include_once` d'aqueixos recursos (classes, interfícies, etc...).
* Cada recurs ha d'incloure tots els altres recursos que referencie: la classe de la qual hereta, interfícies que implementa, classes utilitzades/rebudes com a paràmetres, etc...
* Si els recursos estan en un espai de noms diferent al que estem, emprarem `use` amb la ruta completa per a després utilitzar referències sense qualificar.

#### Autoload

No és tediós haver de fer el `include` de les classes? El autoload ve al rescat.

Així doncs, permet carregar les classes (no les constants ni les funcions) que s'utilitzaran i evitar haver de fer el `include_once` de cadascuna d'elles. Per a això, es pot utilitzar el composer.

### 4. Composer

<figure style="float: right;">
    <img src="imagenes/05/logo-composer.png" width="200">
    <figcaption>Logo Composer</figcaption>
</figure>

Eina per excel·lència en PHP per a la gestió de llibreries i dependències, de manera que instal·la i les actualitza assegurant que tot l'equip de desenvolupament té el mateix entorn i versions. A més, ofereix *autoloading* del nostre codi, de manera que no hàgem de fer-lo nosaltres "a mà".

Està escrit en PHP, i podeu consultar tota la seua documentació en [https://getcomposer.org/](https://getcomposer.org/).

Utilitza [*Packagist*]( https://packagist.org/) com a repositori de llibreries.

Funcionalment, és similar a Maven (Java) / npm (JS).

#### Instal·lació

Si estem usant XAMPP, hem d'instal·lar *Composer* en el propi sistema operatiu. Es recomana seguir les [instruccions oficials](https://getcomposer.org/doc/00-intro.md) segons el sistema operatiu a emprar.

En canvi, si usem *Docker*, necessitem modificar la configuració del nostre contenidor. En el nostre cas, hem decidit modificar l'arxiu `Dockerfile` i afegir el següent comando:

``` docker
COPY --from=composer:2.0 /usr/bin/composer /usr/local/bin/composer
```

És important que dins del contenidor comprovem que tenim la v2:

``` bash
composer -V
```

#### Primers passos

Quan creem un projecte per primera vegada, hem d'inicialitzar el repositori. Per a això, executarem el comando `composer init` on:

* Configurem el nom del paquet, descripció, autor (nom <email>), tipus de paquet (project), etc...
* Definim les dependències del projecte (`require`) i les de desenvolupament (`require-dev`) de manera interactiva.
* En les de desenvolupament s'indica aquelles que no s'instal·laran a l'entorn de producció, per exemple, les llibreries de proves.

Després de la seua configuració, es crearà automàticament l'arxiu `composer.json` amb les dades introduïdes i descàrrega les llibreries en la carpeta `vendor`. La instal·lació de les llibreries sempre es realitza de manera local per a cada projecte.

``` json
{
    "name": "dwes/log",
    "description": "Pruebas con Monolog",
    "type": "project",
    "require": {
        "monolog/monolog": "^2.1"
    },
    "license": "MIT",
    "authors": [
        {
            "name": "Aitor Medrano",
            "email": "a.medrano@edu.gva.es"
        }
    ]
}
```

A l'hora d'indicar cada llibreria introduirem:

* el nom de la llibreria, composta tant pel creador o "vendor", com pel nom del projecte. Exemples: `monolog/monolog` o `laravel/installer`.
* la versió de cada llibreria. Tenim diverses opcions per a indicar-la:

    * Directament: 1.4.2
    * Amb comodins: 1.
    * A partir de: >= 2.0.3
    * Sense trencament de canvis: ^1.3.2 // >=1.3.2 <2.0.0

#### Actualitzar llibreries

Podem definir les dependències via l'arxiu `composer.json` o mitjançant comandos amb el format `composer require vendor/package:version`. Per exemple, si volem afegir phpUnit com a llibreria de desenvolupament, farem:

``` bash
composer require phpunit/phpunit –dev
```

Després d'afegir noves llibreries, hem d'actualitzar el nostre projecte:

``` bash
composer update
```

Si creem l'arxiu `composer.json` nosaltres directament sense inicialitzar el repositori, hem d'instal·lar les dependències:

``` bash
composer install
```

En fer aquest pas (tant instal·lar com actualitzar), com ja hem comentat, es descarreguen les llibreries en dins de la carpeta `vendor`. És molt important afegir aquesta carpeta a l'arxiu `.gitignore` per a no pujar-les a GitHub.

A més es crea l'arxiu `composer.lock`, que emmagatzema la versió exacta que s'ha instal·lat de cada llibreria (aquest arxiu no es toca).

#### `autoload.php`

*Composer* crea de manera automàtica en `vendor/autoload.php` el codi per a incloure de manera automàtica totes les llibreries que tinguem configurades en `composer.json`.

Per a utilitzar-ho, en la capçalera del nostre arxius posarem:

``` php
<?php
require 'vendor/autoload.php';
```

En el nostre cas, de moment només el podrem en els arxius on provem les classes

Si volem que Composer també s'encarregue de carregar de manera automàtica les nostres classes de domini, dins de l'arxiu `composer.json`, definirem la propietat `autoload`:

``` json
"autoload": {
    "psr-4": {"Dwes\\": "app/Dwes"}
},
```

Posteriorment, hem de tornar a generar el *autoload* de *Composer* mitjançant l'opció `dump-autoload` (o `du`):

``` bash
composer dump-autoload
```


### 5. Logger amb Monolog

Provarem *Composer* afegint la llibreria de [*Monolog*](https://github.com/seldaek/monolog) al nostre projecte. Es tracta d'un llibreria per a la gestió de logs de les nostres aplicacions, suportant diferents nivells (info, warning, etc...), eixides (fitxers, sockets, BBDD, Web Services, email, etc) i formats (text pla, HTML, JSON, etc...).

Per a això, inclourem la llibreria en el nostre projecte amb:

``` bash
composer require monolog/monolog
```

Monolog 2 requereix almenys PHP 7.2, compleix amb el estandar de logging PSR-3, i és la llibreria emprada per *Laravel* i *Symfony* per a la gestió de logs.

!!! info "Quan utilitzar un log"
* Seguir les acciones/moviments dels usuaris
* Registrar les transaccions
* Rastrejar els errors d'usuari
* Fallades/avisos a nivell de sistema
* Interpretar i col·leccionar dades per a posterior investigació de patrons

#### Nivells

A continuació vam mostrar els diferents nivells de menys a més restrictiu:

    * debug -100: Informació detallada amb propòsits de debug. No usar en entorns de producció.
    * info - 200: Esdeveniments interessants com l'inici de sessió d'usuaris.
    * notice - 250: Esdeveniments normals però significatius.
    * warning - 300: Ocurrències excepcionals que no arriben a ser error.
    * error - 400: Errors d'execució que permeten continuar amb l'execució de l'aplicació però que han de ser monitorats.
    * critical - 500: Situacions importants on es generen excepcions no esperades o no hi ha disponible un component.
    * alert - 550: S'han de prendre mesures immediatament.
      Caiguda completa de la web, base de dades no disponible, etc... A més, se solen enviar missatges per email.
    * emergency - 600: És l'error més greu i indica que tot el sistema està inutilitzable.


#### Hola Monolog

Per exemple, en l'arxiu `pruebaLog.php` que col·locaríem en l'arrel, primer incloem el **autoload**, importem els classes a utilitzar per a finalment usar els mètodes de **Monolog**:

``` php
<?php
include __DIR__ ."/vendor/autoload.php";

use Monolog\Level;
use Monolog\Logger;
use Monolog\Handler\StreamHandler;

$log = new Logger("MiLogger");
$log->pushHandler(new StreamHandler("logs/milog.log", Level::Debug));

$log->debug("Esto es un mensaje de DEBUG");
$log->info("Esto es un mensaje de INFO");
$log->warning("Esto es un mensaje de WARNING");
$log->error("Esto es un mensaje de ERROR");
$log->critical("Esto es un mensaje de CRITICAL");
$log->alert("Esto es un mensaje de ALERT");
```

En tots els mètodes de registre de missatges (`debug`, `info`, ...), a més del propi missatge, li podem passar informació com el contingut d'alguna variable, usuari de l'aplicació, etc.. com a segon paràmetre dins d'un array, el qual es coneix com **array de contexte**.
És convenient fer-ho mitjançant un array associatiu per a facilitar la lectura del log.

``` php
<?php
$log->warning("Producto no encontrado", [$producto]);
$log->warning("Producto no encontrado", ["datos" => $producto]);
```

#### Funcionament

Cada instància `Logger` té un nom de canal i una pila de manejadores (**handler**).
Cada missatge que manem al log travessa la pila de manejadores, i cadascun decideix si ha de registrar la informació, i si es dona el cas, finalitzar la propagació.
Per exemple, un `StreamHandler` en el fons de la pila que ho escriga tot en disc, i en el topall afig un `MailHandler` que envie un mail només quan hi haja un error.


Els manejadores més utilitzats són:

* `StreamHandler(ruta, nivel)`
* `RotatingFileHandler(ruta, maxFiles, nivel)`
* `NativeMailerHandler(para, asunto, desde, nivel)`
* `FirePHPHandler(nivel)`

Per exemple: Si volem que els missatges de l'aplicació isquen pel log del servidor,
en el nostre cas l'arxiu `error.log` de **Apatxe** utilitzarem com a ruta l'eixida d'error:

``` php
<?php
// error.log
$log->pushHandler(new StreamHandler("php://stderr", Level::Debug));
```

!!! tip "FirePHP"
Per exemple, mitjançant `FirePHPHandler`, podem utilitzar `FirePHP`, la qual és una eina per a fer debug en la consola de Firefox*.
Després d'instal·lar l'extensió en Firefox, habilitar les opcions i configurar el **Handler**, podem veure els missatges acolorits amb les seues dades:

    ``` php
    <?php
    $log = new Logger("MiFirePHPLogger");
    $log->pushHandler(new FirePHPHandler(Level::INFO));

    $datos = ["real" => "Bruce Wayne", "personaje" => "Batman"];
    $log->debug("Esto es un mensaje de DEBUG", $datos);
    $log->info("Esto es un mensaje de INFO", $datos);
    $log->warning("Esto es un mensaje de WARNING", $datos);
    // ...
    ```

    <figure style="align: center;">
        <img src="imagenes/05/firePhp.png">
        <figcaption>Ejemplo de uso de FirePHP</figcaption>
    </figure>


#### Manejadors

Si no s'indica cap, se li assigna un per defecte. L'últim manejador inserit serà el primer a executar-se.
Després es van executant conforme a la pila.


#### Processadors

Els processadors permeten afegir informació als missatges.
Per a això, s'apilen després de cada manejador mitjançant el mètode `pushProcessor($processador)`.

Alguns processadors coneguts són `IntrospectionProcessor` (mostren la línia, fitxer, classe i metodo des del qual s'invoca el log), `WebProcessor` (afig la URI, mètode i IP) o `GitProcessor` (afig la branca i el commit).

=== "PHP"

    ``` php
    <?php
    $log = new Logger("MiLogger");
    $log->pushHandler(new RotatingFileHandler("logs/milog.log", 0, Level::DEBUG));
    $log->pushProcessor(new IntrospectionProcessor());
    $log->pushHandler(new StreamHandler("php://stderr", Level::WARNING));
    // no usa Introspection pq lo hemos apilado después, le asigno otro
    $log->pushProcessor(new WebProcessor());
    ```

=== "Consola en format text"

    ``` log
    [2020-11-26T13:35:31.076138+01:00] MiLogger.DEBUG: Esto es un mensaje de DEBUG [] {"file":"C:\\xampp\\htdocs\\log\\procesador.php","line":12,"class":null,"function":null}
    [2020-11-26T13:35:31.078344+01:00] MiLogger.INFO: Esto es un mensaje de INFO [] {"file":"C:\\xampp\\htdocs\\log\\procesador.php","line":13,"class":null,"function":null}
    ```

#### Formatadors

S'associen als manejadores amb `setFormatter`. Els formateadores més utilitzats són `LineFormatter`, `HtmlFormatter` o `JsonFormatter`.

=== "PHP"

    ``` php
    <?php
    $log = new Logger("MiLogger");
    $rfh = new RotatingFileHandler("logs/milog.log", Level::Debug);
    $rfh->setFormatter(new JsonFormatter());
    $log->pushHandler($rfh);
    ```

=== "Consola en JSON"

    ``` json
    {"message":"Esto es un mensaje de DEBUG","context":{},"level":100,"level_name":"DEBUG","channel":"MiLogger","datetime":"2020-11-27T15:36:52.747211+01:00","extra":{}}
    {"message":"Esto es un mensaje de INFO","context":{},"level":200,"level_name":"INFO","channel":"MiLogger","datetime":"2020-11-27T15:36:52.747538+01:00","extra":{}}
    ```

!!! tip "Més informació"
Més informació sobre manejadores, formateadores i processadors en <https://github.com/Seldaek/monolog/blob/master/doc/02-handlers-formatters-processors.md>
 

## 19. Exercicis 

### Bateria d'Exercicis Solucionats per a la Unitat de PHP

#### Exercici 1: Introducció a PHP
1. Crea un fitxer  que imprimeixi "Hola, món!" a la pantalla.
2. Modifica el fitxer per tal que imprimeixi el teu nom utilitzant una variable.

<details>
<summary>Solució</summary>
    
    ```php
    <?php
    // Exercici 1
    $name = 'Ignasi':
    echo "Hola, món!" . "Hola, " .$name;
    ?>
    ```
</details>

#### Exercici 2: Ús de cometes
1. Crea un fitxer que definisca una variable `$name` amb el teu nom i imprimeixi la frase "Hola, [nom]!" utilitzant cometes dobles.
2. Fes-ho amb cometes simples i compara els resultats.

<details>
<summary>Solució</summary>

    ```php
    <?php
    // Exercici 2
    $name = 'Ignasi':
    echo "Hola, $name!";
    echo 'Hola, $name!';
    ?>
    ```
</details>

#### Exercici 3: Funcions bàsiques
1. Crea una funció `suma` que sume dos números i retorni el resultat. Invoca la funció amb els números 5 i 3 i imprimeix el resultat.
2. Crea una funció `multiplicacio` que multipliqui dos números i retorni el resultat. Invoca la funció amb els números 4 i 7 i imprimeix el resultat.

<details>
<summary>Solució</summary>

    ```php
    <?php
    // Exercici 2
    function suma($a, $b) {
        return $a + $b;
    }
    function multiplicacio($a, $b) {
        return $a * $b;
    }
    echo suma(5, 3);  // Sortida: 8
    echo multiplicacio(4, 7);  // Sortida: 28
    ?>
    ```

</details>

#### Exercici 4: Control de flux - Condicionals
1. Crea un fitxer que definisca una variable `$edat`. Si `$edat` és major o igual a 18, imprimeix "Ets major d'edat"; en cas contrari, imprimeix "Ets menor d'edat".
2. Modifica el fitxer `edat.php` per tal que imprimeixi "Edat invàlida" si `$edat` és un número negatiu.

<details>
    <summary>Solució</summary>

    ```php
    <?php
    // Exercici 4
    $edat = 20;
    if ($edat < 0) {
        echo "Edat invàlida";
    } else{
        if ($edat >= 18) {
            echo "Ets major d'edat";
        } else {
            echo "Ets menor d'edat";
        }
    }
    ?>
    ```    
</details>

#### Exercici 5: Control de flux - Bucles
1. Crea un fitxer que utilitzi un bucle `for` per imprimir els números del 0 al 9.
2. Fes-ho també amb un bucle `while` que faci el mateix.

<details>
    <summary>Solució</summary>
    
        ```php
            <?php
            // Exercici 5
            // Bucle for
            for ($i = 0; $i < 10; $i++) {
                echo $i . "<br>";
            }
            // Bucle while
            $i = 0;
            while ($i < 10) {
                echo $i . "<br>";
                $i++;
            }
            ?>
        ```
</details>

#### Exercici 6: Treballar amb arrays
1. Crea un fitxer que definisca un array `$fruites` amb tres elements: "poma", "plàtan" i "maduixa". Imprimeix el primer element de l'array.
2. Afegeix un quart element "taronja" a l'array i imprimeix tots els elements utilitzant un bucle `foreach`.

<details>
    <summary>Solució</summary>
        
        ```php
        <?php
        // Exercici 6
        // Punt 1
        $fruites = array("poma", "plàtan", "maduixa");
        echo $fruites[0] . "<br>";
        // Punt 2
        $fruites[] = "taronja";
        foreach ($fruites as $fruita) {
            echo $fruita . "<br>";
        }
        ?>
        ```
</details>

#### Exercici 7: Cometes dobles i variables
1. Crea un fitxer que definisca una variable `$color` amb el valor "blau". Utilitza cometes dobles per imprimir "El meu color preferit és [color]."
2. Ara,  utilitza cometes simples i concatenació.

<details>
<summary>Solució</summary>

    ```php
    <?php
    // Exercici 7
    $color = "blau";
    echo "El meu color preferit és $color.";
    echo 'El meu color preferit és ' . $color . '.';
    ?>
    ```
</details>

#### Exercici 8: Combinació de funcions i arrays
1. Crea una funció `afegir_element` que prenga un array i un element com a arguments, afegeisca l'element a l'array i retorne l'array modificat.
2. Crea un fitxer on defnisques un array `$animals` amb els elements "gat" i "gos". Utilitza la funció `afegir_element` per afegir "conill" a l'array i imprimeix tots els elements.

<details>
<summary>Solució</summary>
    
    ```php
    <?php
    // Exercici 8
    function afegir_element($array, $element) {
        $array[] = $element;
        return $array;
    }
    $animals = array("gat", "gos");
    $animals = afegir_element($animals, "conill");
    foreach ($animals as $animal) {
        echo $animal . "<br>";
    }
    ?>
    ```
</details>

#### Exercici 9: Utilitzant `match` per a categoritzar

Crea un fitxer  que utilitze la instrucció `match` per categoritzar una variable `$nota` segons el següent criteri:
     - Si la nota és 10, imprimir "Excel·lent".
     - Si la nota és 8 o 9, imprimir "Molt bé".
     - Si la nota és 5, 6 o 7, imprimir "Bé".
     - Per qualsevol altra nota, imprimir "Insuficient".

<details>
<summary>Solució</summary>

```php
$nota = 8;

$resultat = match (true) {
    $nota === 10 => 'Excel·lent',
    $nota >= 8 && $nota <= 9 => 'Molt bé',
    $nota >= 5 && $nota <= 7 => 'Bé',
    default => 'Insuficient',
};

echo $resultat;  // Sortida: Molt bé
```
</details>

#### Exercici 10: Llista de preus amb `match`

Crea un fitxer que utilitze la instrucció `match` per assignar un preu a una variable `$producte`. Els productes i preus són:
     - "pa" => 1.00
     - "llet" => 0.80
     - "formatge" => 2.50
     - Qualsevol altre producte => 0.00

<details>
<summary>Solució</summary>

```php
$producte = 'formatge';

$preu = match ($producte) {
    'pa' => 1.00,
    'llet' => 0.80,
    'formatge' => 2.50,
    default => 0.00,
};

echo "El preu de $producte és $preu euros.";  // Sortida: El preu de formatge és 2.5 euros.
```
</details>

#### Exercici 11: Calculadora simple amb `match`

Crea un fitxer que utilitze la instrucció `match` per fer operacions matemàtiques bàsiques (`+`, `-`, `*`, `/`). La variable `$operacio` ha de determinar l'operació a realitzar i les variables `$a` i `$b` seran els operands.

<details>
<summary>Solució</summary>

```php
$a = 10;
$b = 5;
$operacio = '+';

$resultat = match ($operacio) {
    '+' => $a + $b,
    '-' => $a - $b,
    '*' => $a * $b,
    '/' => $a / $b,
    default => 'Operació desconeguda',
};

echo "El resultat de $a $operacio $b és $resultat.";  // Sortida: El resultat de 10 + 5 és 15.
```
</details>

#### Exercici 12: Tractament de formulari

1. Crea un formulari en HTML que permeti als usuaris introduir el seu nom i edat. Després de l'enviament del formulari, mostra una pàgina PHP que processi les dades introduïdes i mostri un missatge de benvinguda personalitzat.

<details>
<summary>Solució</summary>

```php
<!DOCTYPE html>
<html lang="ca">
<head>
    <meta charset="UTF-8">
    <title>Formulari de Benvinguda</title>
</head>
<body>
    <h2>Formulari de Benvinguda</h2>
    <form action="benvinguda.php" method="post">
        <label for="nom">Nom:</label>
        <input type="text" id="nom" name="nom" required><br><br>
        <label for="edat">Edat:</label>
        <input type="number" id="edat" name="edat" required><br><br>
        <input type="submit" value="Enviar">
    </form>
</body>
</html>
```

```php
<!DOCTYPE html>
<html lang="ca">
<head>
    <meta charset="UTF-8">
    <title>Benvinguda</title>
</head>
<body>
    <?php
        if ($_SERVER["REQUEST_METHOD"] == "POST") {
            $nom = htmlspecialchars($_POST['nom']);
            $edat = htmlspecialchars($_POST['edat']);
            echo "<h2>Benvingut/da, $nom!</h2>";
            echo "<p>Tens $edat anys.</p>";
        } else {
            echo "<p>Si us plau, completa el formulari.</p>";
        }
    ?>
</body>
</html>
```
</details>

#### Exercici 13: Formulari en la mateixa pàgina

1.  Crea un formulari en HTML que permeta als usuaris introduir la seva adreça de correu electrònic i un missatge. Després de l'enviament del formulari, crea una pàgina PHP que processe les dades introduïdes, comprove que l'adreça de correu electrònic és vàlida i mostre el missatge introduït per l'usuari.

<details>
<summary>Solució</summary>
    
```php
<!DOCTYPE html>
<html lang="ca">
<head>
    <meta charset="UTF-8">
    <title>Formulari de Contacte</title>
</head>
<body>
    <?php
    if ($_SERVER["REQUEST_METHOD"] == "POST") {
        $email = htmlspecialchars($_POST['email']);
        $missatge = htmlspecialchars($_POST['missatge']);

        if (filter_var($email, FILTER_VALIDATE_EMAIL)) {
            echo "<h2>Gràcies per contactar-nos!</h2>";
            echo "<p>El teu correu electrònic: $email</p>";
            echo "<p>El teu missatge: $missatge</p>";
        } else {
            echo "<p>Adreça de correu electrònic no vàlida. Si us plau, torna-ho a intentar.</p>";
        }
    } else {
        ?>
        <h2>Formulari de Contacte</h2>
        <form action="<?php echo htmlspecialchars($_SERVER["PHP_SELF"]); ?>" method="post">
            <label for="email">Correu electrònic:</label>
            <input type="email" id="email" name="email" required><br><br>
            <label for="missatge">Missatge:</label><br>
            <textarea id="missatge" name="missatge" rows="4" cols="50" required></textarea><br><br>
            <input type="submit" value="Enviar">
        </form>
        <?php
    }
    ?>
</body>
</html>
```
</details>

#### Exercici 14: Validació de formulari amb `match`

1. Crea un fitxer que utilitze la instrucció `match` per validar un formulari amb camps per a nom, correu electrònic i edat. Si algun camp està buit, ha de retornar un missatge d'error corresponent.

<details>
<summary>Solució</summary>

```php
$nom = 'Joan';
$correu = 'joan@example.com';
$edat = '';

$validacio = match (true) {
empty($nom) => 'El camp nom és obligatori.',
!filter_var($correu, FILTER_VALIDATE_EMAIL) => 'El correu electrònic no és vàlid.',
empty($edat) => 'El camp edat és obligatori.',
default => 'Formulari vàlid.',
};

echo $validacio;  // Sortida: El camp edat és obligatori.
```

</details>

#### Exercici 15: Variables de servidor

1. Mostra en un fitxer les variables de servidor que conegues

<details>
<summary>Solució</summary>
    
```php
<!DOCTYPE html>
<html lang="ca">
<head>
    <meta charset="UTF-8">
    <title>Informació del Servidor</title>
</head>
<body>
    <h2>Informació del Servidor</h2>
    <?php
        echo "<p><strong>Nom del servidor:</strong> " . $_SERVER['SERVER_NAME'] . "</p>";
        echo "<p><strong>Adreça IP del servidor:</strong> " . $_SERVER['SERVER_ADDR'] . "</p>";
        echo "<p><strong>Software del servidor:</strong> " . $_SERVER['SERVER_SOFTWARE'] . "</p>";
        echo "<p><strong>Agent d'usuari del client:</strong> " . $_SERVER['HTTP_USER_AGENT'] . "</p>";
        echo "<p><strong>Mètode de la sol·licitud:</strong> " . $_SERVER['REQUEST_METHOD'] . "</p>";
        echo "<p><strong>URL de la sol·licitud:</strong> " . $_SERVER['REQUEST_URI'] . "</p>";
        echo "<p><strong>Referent:</strong> " . (isset($_SERVER['HTTP_REFERER']) ? $_SERVER['HTTP_REFERER'] : 'No disponible') . "</p>";
        echo "<p><strong>Protocol utilitzat:</strong> " . $_SERVER['SERVER_PROTOCOL'] . "</p>";
        echo "<p><strong>Port utilitzat:</strong> " . $_SERVER['SERVER_PORT'] . "</p>";
    ?>
</body>
</html>
```
</details>

#### Exercici 16: Pujar fitxers al servidor

1. Crea un formulari en HTML que permeti als usuaris pujar un fitxer i seleccionar una opció d'un checkbox. Les opcions del checkbox han de ser carregades des d'un array predefinit en PHP. Després de l'enviament del formulari, el fitxer pujat ha de ser processat i mogut a una ubicació específica del servidor, i s'ha de mostrar la informació del fitxer i l'opció seleccionada.

<details>
<summary>Solució</summary>

```php

<!DOCTYPE html>
<html lang="ca">
<head>
    <meta charset="UTF-8">
    <title>Pujar Fitxer i Selecció Opció</title>
</head>
<body>
    <?php
    // Definim les opcions per al checkbox
    $opcions = ["Opció 1", "Opció 2", "Opció 3"];

    // Comprovem si el formulari ha estat enviat
    if ($_SERVER["REQUEST_METHOD"] == "POST") {
        // Comprovem si el fitxer ha estat pujat sense errors
        if (isset($_FILES["fitxer"]) && $_FILES["fitxer"]["error"] == 0) {
            $nom_fitxer = $_FILES["fitxer"]["name"];
            $tipus_fitxer = $_FILES["fitxer"]["type"];
            $mida_fitxer = $_FILES["fitxer"]["size"];
            $ubicacio_temporal = $_FILES["fitxer"]["tmp_name"];

            // Movem el fitxer a una ubicació permanent
            $ubicacio_destinacio = "uploads/" . basename($nom_fitxer);
            if (move_uploaded_file($ubicacio_temporal, $ubicacio_destinacio)) {
                echo "<p>El fitxer <strong>$nom_fitxer</strong> ha estat pujat correctament.</p>";
                echo "<p>Tipus de fitxer: $tipus_fitxer</p>";
                echo "<p>Mida del fitxer: " . ($mida_fitxer / 1024) . " KB</p>";
                echo "<p>Ubicació del fitxer: $ubicacio_destinacio</p>";
            } else {
                echo "<p>Error al moure el fitxer a la ubicació final.</p>";
            }
        } else {
            echo "<p>Error al pujar el fitxer.</p>";
        }

        // Comprovem si una opció del checkbox ha estat seleccionada
        if (isset($_POST['opcio'])) {
            $opcio_seleccionada = $_POST['opcio'];
            echo "<p>Has seleccionat: $opcio_seleccionada</p>";
        } else {
            echo "<p>No has seleccionat cap opció.</p>";
        }
    } else {
        ?>
        <h2>Formulari per Pujar Fitxer i Selecció d'Opció</h2>
        <form action="<?php echo htmlspecialchars($_SERVER["PHP_SELF"]); ?>" method="post" enctype="multipart/form-data">
            <label for="fitxer">Selecciona un fitxer:</label>
            <input type="file" id="fitxer" name="fitxer" required><br><br>

            <label for="opcio">Selecciona una opció:</label><br>
            <?php
            foreach ($opcions as $opcio) {
                echo '<input type="checkbox" id="' . $opcio . '" name="opcio" value="' . $opcio . '">';
                echo '<label for="' . $opcio . '"> ' . $opcio . '</label><br>';
            }
            ?><br>

            <input type="submit" value="Enviar">
        </form>
        <?php
    }
    ?>
</body>
</html>
```
</details>

### Exercicis proposats 

#### Exercici 1: Manipulació de Variables i Operadors

Assigna múltiples variables i utilitza operadors aritmètics i lògics. Mostra el resultat de cada operació.

#### Exercici 2: Control de Flux amb Bucles

Utilitza un bucle `for` per imprimir els números parells del 0 al 20.
Fes-ho també amb un bucle `while`.

#### Exercici 3: Treballar amb Arrays i Funcions

Escriu una funció que prenga un array de números, calculi la mitjana i retorni el resultat. Utilitza aquesta funció per imprimir la mitjana d'un array de cinc números.

#### Exercici 4: Manipulació de Strings

Escriu un script que prenga una cadena de text i compti el nombre de vocals. Imprimeix el resultat.

#### Exercici 5: Arrays Multidimensionals

Crea un array multidimensional que represente una taula de multiplicar del 1 al 5 i imprimeix els resultats en forma de taula.

#### Exercici 6: Utilitzant `match` per a categoritzar

Crea un fitxer que utilitze la instrucció `match` per categoritzar una variable `$nota` segons el següent criteri:
- Si la nota és 10, imprimir "Excel·lent".
- Si la nota és 8 o 9, imprimir "Molt bé".
- Si la nota és 5, 6 o 7, imprimir "Bé".
- Per qualsevol altra nota, imprimir "Insuficient".

#### Exercici 7: Validació de Formularis

Crea un formulari en HTML que permetis als usuaris introduir el seu nom, el correu electrònic i un password (dues vegades). Després de l'enviament del formulari, valida que tots els camps han estat completats i que el correu electrònic és vàlid, que el password tinga complexitat i que coincidixen. Mostra un missatge d'error si alguna validació falla, i si tot és correcte, mostra un missatge confirmant que l'usuari s'ha registrat correctament.

#### Exercici 8: Processament de Formularis amb Select i Radio Buttons

A partir del formulari [newBook.php](recursos/newBook.php), fes que el mòdul i el estat els agafe de valors introduïts en arrays. Mostra el resultat en una taula.  
 
#### Exercici 9: Pujar imatges des de formulari

A partir del formulari anterior fes que es puga pujar una imatge. Mostra la imatge en la taula.

### [Solucions](10solucions.html#Tema 2: Introducció a PHP)

## 20. Enunciats dels Projectes

### Projecte "L'Ofegat"

**Enunciat:**
Implementa una versió simplificada del joc "L'Ofegat" utilitzant HTML i PHP. El joc ha de permetre als jugadors endevinar les lletres d'una paraula predefinida i mostrar l'estat actual de les lletres endevinades. No és necessari mantenir l'estat del joc entre sol·licituds ni comprovar si s'han esgotat els intents en aquesta fase inicial.

**Requisits:**

1. **Paraula a Endevinar:**
    - Defineix una paraula predefinida a endevinar.
2. **Inicialització de les Lletres Endevinades:**
    - Crea un array amb guions baixos per representar les lletres que l'usuari ha de trobar.
    - Crea una funció per imprimir este array i que serà el que ens mostre el progres del joc. **(les funcions aniran en un fitxer a part)**
3. **Funció per a Comprovar Intents:**
    - Crea una funció en PHP que prenga la paraula a endevinar, la lletra introduïda per l'usuari i l'array de lletres endevinades (passat per referència).
    - La funció ha de comprovar si la lletra introduïda per l'usuari forma part de la paraula.
    - Si la lletra és correcta, la funció substituirà els guions baixos per la lletra corresponent.
    - La funció retornarà un valor booleà que indique si la lletra és errònia o no.
    - Fes proves de la funció per comprovar que funciona correctament.
4. **Comprovació d'Intents:**
    - Utilitza la funció creada per comprovar si la lletra introduïda per l'usuari forma part de la paraula.
    - Mostra un missatge d'error si la lletra no és correcta.
5. **Interfície d'Usuari:**
    - Mostra les lletres introduïdes per l'usuari fins al moment en color verd si són encertades o roig si són errades.
    - Mostra les errades de l'usuari.
    - Crea un formulari HTML que permeta als jugadors introduir una lletra.

**Codi CSS Proporcionat**:

```css
.correct { color: green; }
.incorrect { color: red; }
```

### Projecte "4 en Ratlla"

**Enunciat:**
Implementa una versió simplificada del joc "4 en Ratlla" utilitzant HTML i PHP. El joc ha de permetre als jugadors introduir els seus moviments i mostrar l'estat actual de la graella. No és necessari mantenir l'estat del joc entre sol·licituds ni comprovar si hi ha un guanyador en aquesta fase inicial.

**Requisits:**

1. **Inicialització de la Graella**:
    - Crea una funció `inicialitzarGraella()` que inicialitze una graella buida de 6 files i 7 columnes.
2. **Pintar la Graella**:
    - Crea una funció `pintarGraella($graella)` que pinte la graella en HTML. Utilitza diferents colors per a les fitxes dels jugadors, aplicant el CSS adjunt.
3. **Realitzar Moviments**:
    - Crea una funció `ferMoviment(&$graella, $columna, $jugadorActual)` que realitze un moviment en la columna especificada pel jugador actual.
4. **Interfície d'Usuari**:
    - Crea un formulari HTML que permeta als jugadors introduir la columna on volen posar la seua fitxa. Aquest formulari ha de mantenir el jugador actual entre sol·licituds.

**Codi CSS Proporcionat**:

```css
table { border-collapse: collapse; }
td {
    width: 50px;
    height: 50px;
    border-radius: 50%;
    border: 10px dotted #fff; /* Cercle amb punts blancs */
    background-color: #000; /* Fons negre o pot ser un altre color */
    display: inline-block;
    margin: 10px;
    color: white;
    font-size: 2rem;
    text-align: center ;
    vertical-align: middle;
}
.player1 {
    background-color: red; /* Color vermell per un dels jugadors */
}
.player2 {
    background-color: yellow; /* Color groc per l'altre jugador */
}
.buid {
    background-color: white; /* Color blanc per cercles buits */
    border-color: #000; /* Puntes negres per millor visibilitat */
}

```

### Rúbrica

| Criteri                            | Puntuació Total | Complet(2)                          | A mitjes(1)                       | No(0)                              |
|------------------------------------|-----------------|-------------------------------------|-----------------------------------|------------------------------------|
| **Paraula a Endevinar**            | 1               | Paraula definida correctament       | Paraula definida però amb errors  | No s'ha definit la paraula         |
| **Inicialització de les Lletres**  | 3               | Array creat correctament            | Array creat però amb errors       | No s'ha creat l'array              |
| **Funció per a Comprovar Intents** | 5               | Funció creada i funcional           | Funció creada però amb errors     | No s'ha creat la funció            |
| **Comprovació d'Intents**          | 3               | Comprovació realitzada correctament | Comprovació amb errors            | No s'ha realitzat la comprovació   |
| **Inicialització de la Graella**   | 4               | Funció creada correctament          | Funció creada però amb errors     | No s'ha creat la funció            |
| **Pintar la Graella**              | 4               | Funció creada i funcional           | Funció creada però amb errors     | No s'ha creat la funció            |
| **Realitzar Moviments**            | 5               | Funció creada i funcional           | Funció creada però amb errors     | No s'ha creat la funció            |
| **Interfícies d'Usuari**           | 6               | Interfície correcta i funcional     | Interfície creada però amb errors | No s'ha creat la interfície        |
| **Estil CSS**                      | 2               | CSS aplicat correctament            | CSS aplicat però amb errors       | No s'ha aplicat el CSS             |
| **Comentaris i Claredat del Codi** | 1               | Codi ben comentat i clar            | Codi amb alguns comentaris        | Codi sense comentaris o desordenat |


## 21. Autoavaluació: Conceptes Bàsics de PHP

#### Exercici 1: Sintaxi Bàsica de PHP

##### Pregunta:
Quina és la manera correcta d'iniciar i finalitzar un bloc de codi PHP dins d'un fitxer HTML?

##### Opcions:
<form>
  <input type="radio" id="q1a" name="question1" value="a">
  <label for="q1a">a) `<?php ... ?>`</label><br>
  <input type="radio" id="q1b" name="question1" value="b">
  <label for="q1b">b) `<php> ... </php>`</label><br>
  <input type="radio" id="q1c" name="question1" value="c">
  <label for="q1c">c) `<?php ?> ... <?php end ?>`</label><br>
  <input type="radio" id="q1d" name="question1" value="d">
  <label for="q1d">d) `<script php> ... </script>`</label><br><br>
  <input type="button" value="Comprovar" onclick="checkAnswer1()">
</form>

<p id="result1"></p>

<script>
function checkAnswer1() {
    var correctAnswer = "a";
    var radios = document.getElementsByName('question1');
    var userAnswer;
    for (var i = 0; i < radios.length; i++) {
        if (radios[i].checked) {
            userAnswer = radios[i].value;
            break;
        }
    }
    var resultText = userAnswer === correctAnswer ? "Correcte!" : "Incorrecte. La resposta correcta és a) <?php ... ?>.";
    document.getElementById('result1').innerText = resultText;
}
</script>

#### Exercici 2: Variables i Tipus de Dades

##### Pregunta:
Quina opció mostra el tipus de dades assignat a la variable `$nom`?

##### Opcions:
<form>
  <input type="radio" id="q2a" name="question2" value="a">
  <label for="q2a">a) `echo gettype($nom);`</label><br>
  <input type="radio" id="q2b" name="question2" value="b">
  <label for="q2b">b) `print datatype($nom);`</label><br>
  <input type="radio" id="q2c" name="question2" value="c">
  <label for="q2c">c) `echo typeof($nom);`</label><br>
  <input type="radio" id="q2d" name="question2" value="d">
  <label for="q2d">d) `print type($nom);`</label><br><br>
  <input type="button" value="Comprovar" onclick="checkAnswer2()">
</form>

<p id="result2"></p>

<script>
function checkAnswer2() {
    var correctAnswer = "a";
    var radios = document.getElementsByName('question2');
    var userAnswer;
    for (var i = 0; i < radios.length; i++) {
        if (radios[i].checked) {
            userAnswer = radios[i].value;
            break;
        }
    }
    var resultText = userAnswer === correctAnswer ? "Correcte!" : "Incorrecte. La resposta correcta és a) echo gettype($nom);";
    document.getElementById('result2').innerText = resultText;
}
</script>

#### Exercici 3: Estructures de Control

##### Pregunta:
Quina és la sortida de l'estructura de control següent?
```php
$numero = 10;
if ($numero > 5) {
    echo "Major que 5";
} else {
    echo "Menor o igual a 5";
}
```
##### Opcions

<form>
  <input type="radio" id="q3a" name="question3" value="a">
  <label for="q3a">a) Major que 5</label><br>
  <input type="radio" id="q3b" name="question3" value="b">
  <label for="q3b">b) Menor o igual a 5</label><br>
  <input type="radio" id="q3c" name="question3" value="c">
  <label for="q3c">c) No imprimeix res</label><br>
  <input type="radio" id="q3d" name="question3" value="d">
  <label for="q3d">d) Error de sintaxi</label><br><br>
  <input type="button" value="Comprovar" onclick="checkAnswer3()">
</form>
<p id="result3"></p>
<script>
function checkAnswer3() {
    var correctAnswer = "a";
    var radios = document.getElementsByName('question3');
    var userAnswer;
    for (var i = 0; i < radios.length; i++) {
        if (radios[i].checked) {
            userAnswer = radios[i].value;
            break;
        }
    }
    var resultText = userAnswer === correctAnswer ? "Correcte!" : "Incorrecte. La resposta correcta és a) Major que 5.";
    document.getElementById('result3').innerText = resultText;
}
</script>

#### Exercici 4: Operadors en PHP

##### Pregunta:
Quin serà el valor de `$resultat` després d'executar el següent codi?
```php
$resultat = 5 + 2 * 3;
```
##### Opcions:

<form>
  <input type="radio" id="q4a" name="question4" value="a">
  <label for="q4a">a) 21</label><br>
  <input type="radio" id="q4b" name="question4" value="b">
  <label for="q4b">b) 11</label><br>
  <input type="radio" id="q4c" name="question4" value="c">
  <label for="q4c">c) 17</label><br>
  <input type="radio" id="q4d" name="question4" value="d">
  <label for="q4d">d) 13</label><br><br>
  <input type="button" value="Comprovar" onclick="checkAnswer4()">
</form>
<p id="result4"></p>
<script>
function checkAnswer4() {
    var correctAnswer = "b";
    var radios = document.getElementsByName('question4');
    var userAnswer;
    for (var i = 0; i < radios.length; i++) {
        if (radios[i].checked) {
            userAnswer = radios[i].value;
            break;
        }
    }
    var resultText = userAnswer === correctAnswer ? "Correcte!" : "Incorrecte. La resposta correcta és b) 11.";
    document.getElementById('result4').innerText = resultText;
}
</script>

#### Exercici 5: Arrays en PHP

##### Pregunta:

Com es pot afegir un element al final d'un array en PHP?

##### Opcions:
<form>
  <input type="radio" id="q5a" name="question5" value="a">
  <label for="q5a">a) array_add($array, $element);</label><br>
  <input type="radio" id="q5b" name="question5" value="b">
  <label for="q5b">b) $array[] = $element;</label><br>
  <input type="radio" id="q5c" name="question5" value="c">
  <label for="q5c">c) append($array, $element);</label><br>
  <input type="radio" id="q5d" name="question5" value="d">
  <label for="q5d">d) add_to_array($array, $element);</label><br><br>
  <input type="button" value="Comprovar" onclick="checkAnswer5()">
</form>
<p id="result5"></p>
<script>
function checkAnswer5() {
    var correctAnswer = "b";
    var radios = document.getElementsByName('question5');
    var userAnswer;
    for (var i = 0; i < radios.length; i++) {
        if (radios[i].checked) {
            userAnswer = radios[i].value;
            break;
        }
    }
    var resultText = userAnswer === correctAnswer ? "Correcte!" : "Incorrecte. La resposta correcta és b) $array[] = $element;";
    document.getElementById('result5').innerText = resultText;
}
</script>

#### Exercici 6: Funcions en PHP

##### Pregunta:

Com es defineix una funció en PHP?

##### Opcions:

<form>
  <input type="radio" id="q6a" name="question6" value="a">
  <label for="q6a">a) function: myFunction() { ... }</label><br>
  <input type="radio" id="q6b" name="question6" value="b">
  <label for="q6b">b) def myFunction() { ... }</label><br>
  <input type="radio" id="q6c" name="question6" value="c">
  <label for="q6c">c) function myFunction() { ... }</label><br>
  <input type="radio" id="q6d" name="question6" value="d">
  <label for="q6d">d) fn myFunction() => { ... }</label><br><br>
  <input type="button" value="Comprovar" onclick="checkAnswer6()">
</form>
<p id="result6"></p>
<script>
function checkAnswer6() {
    var correctAnswer = "c";
    var radios = document.getElementsByName('question6');
    var userAnswer;
    for (var i = 0; i < radios.length; i++) {
        if (radios[i].checked) {
            userAnswer = radios[i].value;
            break;
        }
    }
    var resultText = userAnswer === correctAnswer ? "Correcte!" : "Incorrecte. La resposta correcta és c) function myFunction() { ... }";
    document.getElementById('result6').innerText = resultText;
}
</script>

#### Exercici 7: Instrucció switch

##### Pregunta:

Quina instrucció s'utilitza per detenir l'execució d'un cas dins d'un switch en PHP?

##### Opcions:

<form>
  <input type="radio" id="q7a" name="question7" value="a">
  <label for="q7a">a) stop</label><br>
  <input type="radio" id="q7b" name="question7" value="b">
  <label for="q7b">b) exit</label><br>
  <input type="radio" id="q7c" name="question7" value="c">
  <label for="q7c">c) halt</label><br>
  <input type="radio" id="q7d" name="question7" value="d">
  <label for="q7d">d) break</label><br><br>
  <input type="button" value="Comprovar" onclick="checkAnswer7()">
</form>
<p id="result7"></p>
<script>
function checkAnswer7() {
    var correctAnswer = "d";
    var radios = document.getElementsByName('question7');
    var userAnswer;
    for (var i = 0; i < radios.length; i++) {
        if (radios[i].checked) {
            userAnswer = radios[i].value;
            break;
        }
    }
    var resultText = userAnswer === correctAnswer ? "Correcte!" : "Incorrecte. La resposta correcta és d) break.";
    document.getElementById('result7').innerText = resultText;
}
</script>
