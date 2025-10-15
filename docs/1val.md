# El llenguatge PHP

??? abstract "Duració i criteris d'avaluació"

    Duració estimada: 20 hores

    <hr />

    | Resultat d'aprenentatge | Criteris d'avaluació|
    | -------                 | -------             |
    | 2. Escriu sentències executables per un servidor Web reconeixent i aplicant procediments d'integració del codi en llenguatges de marques. | a) S'han reconegut els mecanismes de generació de pàgines Web a partir de llenguatges de marques amb codi embegut. <br/> b) S'han identificat les principals tecnologies associades.  <br/> c) S'han utilitzat etiquetes per a la inclusió de codi en el llenguatge de marques.  <br/> d) S'ha reconegut la sintaxi del llenguatge de programació que s'ha d'utilitzar.  <br/> e) S'han escrit sentències simples i s'ha comprovat els seus efectes en el document resultant.  <br/> f) S'han utilitzat directives per a modificar el comportament predeterminat.  <br/> g) S'han utilitzat els diferents tipus de variables i operadors disponibles en el llenguatge.  <br/> h) S'han identificat els àmbits d'utilització de les variables.  <br/> |
    | 3. Genera pàgines web de forma dinàmica seguint especificacions rebudes. | a) S'han identificat els mecanismes de separació de la lògica de negoci.<br/>b) S'han utilitzat tecnologies adequades per a la generació dinàmica de pàgines web.<br/>c) S'han utilitzat tècniques d'accés a dades.<br/>d) S'han generat pàgines web dinàmiques que compleixen amb les especificacions rebudes.<br/>e) S'ha comprovat el funcionament de les pàgines web generades.<br/>f) S'han seguit les convencions de format i codificació establertes. |



## 1. Introducció a PHP

#### Què és PHP?
**PHP** (Hypertext Preprocessor) és un llenguatge de programació de codi obert, especialment dissenyat per al desenvolupament web del costat del servidor. Es pot incrustar fàcilment en codi HTML, cosa que el fa una opció popular per crear aplicacions web dinàmiques i interactives. PHP s'utilitza per gestionar el contingut dinàmic, les bases de dades, el seguiment de sessions i fins i tot per crear aplicacions completes.

#### Història de PHP

PHP (Hypertext Preprocessor) és un llenguatge de programació de codi obert creat l'any 1994 per Rasmus Lerdorf. La primera versió pública va ser PHP/FI (Personal Home Page/Forms Interpreter), que va evolucionar fins a convertir-se en PHP 3 el 1998, el qual va ser completament reescrit per Zeev Suraski i Andi Gutmans.

Actualment, PHP és mantingut per The PHP Group i la versió estable més recent (a partir de juliol de 2024) és PHP 8.3. Aquesta versió inclou millores en el rendiment, noves funcions com les propietats llegibles i escriptibles per tipus, expressió `match`, i molt més.

#### Importància en el desenvolupament web
PHP és un dels llenguatges més utilitzats en el desenvolupament web per diverses raons:

* **Facilitat d'aprenentatge:** PHP és relativament fàcil d'aprendre per als principiants en programació web. La seva sintaxi és senzilla i similar a altres llenguatges com C i Perl.
* **Gran comunitat i suport:** PHP té una gran comunitat de desenvolupadors que proporcionen suport, biblioteques, extensions i eines. A més, hi ha nombrosos recursos en línia, tutorials i documentació.
* **Integració amb bases de dades:** PHP es pot integrar fàcilment amb una àmplia varietat de bases de dades, cosa que el fa ideal per a aplicacions web basades en dades.
* **Flexibilitat i escalabilitat:** PHP és altament flexible i es pot utilitzar per desenvolupar tant aplicacions petites com projectes grans i complexos. També és escalable, cosa que permet gestionar un gran volum de trànsit.
* **Cost efectiu:** Com que és de codi obert, PHP és gratuït per utilitzar i distribuir. Això redueix els costos de desenvolupament per a les empreses i els desenvolupadors.

#### Exemple de codi PHP simple
Aquí tens un exemple senzill de com funciona PHP:

=== "PHP" 

```php
<!DOCTYPE html>
<html>
<body>

<h1>El meu primer script PHP</h1>

<?php
echo "Hola, món!";
?>

</body>
</html>
```

En aquest exemple, el codi PHP s'incrusta dins del codi HTML i es delimina amb <?php i ?>. Quan el servidor processa aquest fitxer, executa el codi PHP i envia el resultat al navegador, generant el contingut dinàmic "Hola, món!".
Aquest és un altre exemple de com PHP pot generar HTML dinàmicament:


## 2. Llenguatges imbricats en HTML
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

## 3. Etiquetes per a inserció de codi
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

## 4. Tipus de dades. Conversions entre tipus de dades
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
## 5. Constants
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

## 6. Variables. Operadors.  Àmbits de les variables

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
```php
$global = 10; // Variable global    
function contar() {
    static $vegades = 0;
    $local = 0; // Variable local
    $local++;
    $vegades++;
    $global++;
    echo $local,$vegades,$global;
}
contar(); // Mostra 1,1,11
contar(); // Mostra 1,2,12
```

## 7. Sentències simples en PHP i els seus efectes

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
Exemple complet:
```php
<?php
// Assignació de valors
$x = 5;
$y = "Hola món";

// Operacions aritmètiques
$suma = $x + 10;
$producte = $x * 2;

// Concatenació de cadenes
$nom = "Joan";
$salutacio = $y . ", " . $nom;

// Impressió de resultats
echo $y;  // Hola món
echo $suma;  // 15
echo $producte;  // 10
echo $salutacio;  // Hola món, Joan
 
```

## 8. Funcions 

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


## 9. Directives per a modificar el comportament predeterminat del codi
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
 
## 10. Mecanismes de decisió (if, switch)
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

## 11. Bucles (for, while, foreach)
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

## 12. Arrays

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

## 13. Arrays associatius

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

## 14. Com utilitzar les cometes en PHP

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

## 15. Comentaris en el codi
Comentaris d'una línia:
```php
// Això és un comentari d'una línia
```
Comentaris de diverses línies:
```php
/* Això és un comentari
   de diverses línies */
```
## 16. Variables de servidor

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

## 17. Formularis

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

## Capçaleres de resposta

Ha de ser el primer a retornar. Es retornen mitjançant la funció `header(cadena)`. Mitjançant les capçaleres podem configurar el tipus de contingut, temps d'expiració, redirigir el navegador, especificar errors HTTP, etc.

``` php
<?php header("Content-Type: text/plain"); ?>
<?php header("Location: http://www.ejemplo.com/inicio.html");
exit(); 
```

Es pot comprovar en les eines del desenvolupador dels navegadors web mitjançant *Developer Tools --> Network --> Headers*.

És molt comú configurar les capçaleres per a evitar consultes a la cache o provocar la seua renovació:

``` php
<?php
header("Expires: Sun, 31 Jan 2021 23:59:59 GMT");
// tres horas
$now = time();
$horas3 = gmstrftime("%a, %d %b %Y %H:%M:%S GMT", $now + 60 * 60 * 3);
header("Expires: {$horas3}");
// un año
$now = time();
$anyo1 = gmstrftime("%a, %d %b %Y %H:%M:%S GMT", $now + 365 * 86440);
header("Expires: {$anyo1}");
// se marca como expirado (fecha en el pasado)
$pasado = gmstrftime("%a, %d %b %Y %H:%M:%S GMT");
header("Expires: {$pasado}");
// evitamos cache de navegador y/o proxy
header("Expires: Mon, 26 Jul 1997 05:00:00 GMT");
header("Last-Modified: " . gmdate("D, d M Y H:i:s") . " GMT");
header("Cache-Control: no-store, no-cache, must-revalidate");
header("Cache-Control: post-check=0, pre-check=0", false);
header("Pragma: no-cache");
// redirigimos a otra página
header("Location: http://www.ejemplo.com/inicio.html");
exit();
// devolvemos un error 404
header("HTTP/1.0 404 Not Found");
// enviamos un archivo para descargar
header("Content-Type: application/force-download");
// enviamos un archivo json
header("Content-Type: application/json");
```

## 18. Referències

### Llibres Recomanats
1. **[PHP and MySQL Web Development](https://www.pearson.com/us/higher-education/program/Welling-PHP-and-My-SQL-Web-Development-5th-Edition/PGM335533.html)** de Luke Welling i Laura Thomson
    - Aquest llibre proporciona una visió completa sobre el desenvolupament web amb PHP i MySQL, des de conceptes bàsics fins a tècniques avançades.

2. **[Learning PHP, MySQL & JavaScript: With jQuery, CSS & HTML5](https://www.oreilly.com/library/view/learning-php-mysql/9781491918661/)** de Robin Nixon
    - Ideal per a aquells que busquen una introducció pràctica al desenvolupament web modern utilitzant PHP juntament amb altres tecnologies web.

3. **[Modern PHP: New Features and Good Practices](https://www.oreilly.com/library/view/modern-php/9781491905180/)** de Josh Lockhart
    - Aquest llibre explora les novetats i bones pràctiques en les versions modernes de PHP, incloent-hi temes com la programació orientada a objectes i l'ús de frameworks.

### Documentació Oficial
- **[Documentació Oficial de PHP](https://www.php.net/manual/es/index.php)**
    - La documentació oficial de PHP és una referència essencial per a qualsevol desenvolupador que utilitzi PHP. Inclou guies de llenguatge, referències de funcions i exemples de codi.

### Cursos en Línia
- **[Curso de PHP en W3Schools](https://www.w3schools.com/php/)**
    - Un recurs en línia gratuït amb tutorials i exercicis interactius que cobreixen els conceptes bàsics i avançats de PHP.

- **[PHP for Beginners - Become a PHP Master - CMS Project](https://www.udemy.com/course/php-for-complete-beginners-includes-msql-object-oriented/)** a Udemy
    - Un curs complet de PHP en Udemy que inclou la creació d'un sistema de gestió de continguts (CMS) com a projecte final.

### Recursos Addicionals
- **[PHP: The Right Way](https://phptherightway.com/)**
    - Un recurs comunitari que ofereix bones pràctiques, consells i pautes per al desenvolupament amb PHP.

- **[Laravel Documentation](https://laravel.com/docs)**
    - Documentació oficial de Laravel, un dels frameworks de PHP més populars per al desenvolupament web.

### Exemples i Tutorials
- **[TutorialsPoint PHP Tutorial](https://www.tutorialspoint.com/php/index.htm)**
    - Proporciona una introducció detallada a PHP amb exemples de codi i explicacions pas a pas.

- **[GeeksforGeeks PHP Tutorials](https://www.geeksforgeeks.org/php/)**
    - Una col·lecció d'articles i tutorials sobre diversos temes relacionats amb PHP, des de conceptes bàsics fins a avançats.

### Repositoris de Codi
- **[GitHub PHP](https://github.com/search?q=PHP)**
    - Una col·lecció de repositoris de codi font en PHP, on pots trobar projectes de codi obert i exemples pràctics.


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
# Programació Web

??? abstract "Duració i criteris d'evaluació"

    Duració estimada: 10 hores

    <hr />

    | Resultat d'aprenentatge  | Criteris d'avaluació  |
    | ------                    | -----                |
    | 4. Desenvolupa aplicacions Web embegudes en llenguatges de marques analitzant i incorporant funcionalitats segons especificacions | a) S'han identificat els mecanismes disponibles per al manteniment de la informació que concerneix un client web concret i s'han assenyalat els seus avantatges.<br /> b) S'han utilitzat mecanismes per a mantindre l'estat de les aplicacions web.<br /> c) S'han utilitzat mecanismes per a emmagatzemar informació en el client web i per a recuperar el seu contingut.<br /> d) S'han identificat i caracteritzat els mecanismes disponibles per a l'autenticació d'usuaris.<br /> e) S'han escrit aplicacions que integren mecanismes d'autenticació d'usuaris.<br /> f) S'han utilitzat eines i entorns per a facilitar la programació, prova i depuració del codi. |



## 1.  Mecanismes per al Manteniment de la Informació en Aplicacions Web

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

El **Web Storage** és una API del navegador que permet emmagatzemar dades al client de manera més senzilla i amb més capacitat que les cookies tradicionals. Inclou dos mecanismes principals: `localStorage` i `sessionStorage`.

#### Característiques del Web Storage

- **`localStorage`**: Permet emmagatzemar dades que persisteixen fins que s'elimina explícitament, fins i tot després de tancar el navegador.
- **`sessionStorage`**: Les dades es mantenen només durant la sessió del navegador i s'esborren quan es tanca la pestanya o finestra.

#### Avantatges

- **Capacitat d'Emmagatzematge**: Ofereix més espai (fins a 5-10MB) que les cookies.
- **API Simple**: Proporciona una interfície senzilla per emmagatzemar i recuperar dades.

#### Usos Comuns

- **Manteniment de l'Estat del Client**: Pot guardar dades de sessió i preferències de l'usuari que no cal enviar al servidor.
- **Sincronització amb l'Entorn Servidor**: Es pot utilitzar per emmagatzemar dades que després es sincronitzen amb el servidor, millorant el rendiment i l'experiència d'usuari.

#### Consideracions de Seguretat

- **Accessibilitat**: Les dades són accessibles per JavaScript, per la qual cosa s'ha de tenir cura amb les vulnerabilitats XSS.
- **Dades Sensibles**: Evita emmagatzemar dades sensibles o confidencials.

Tot i que **Web Storage** s'executa al costat del client, entendre les seves funcionalitats pot ajudar els desenvolupadors del servidor a dissenyar sistemes més robustos i eficaços, on la cooperació entre client i servidor maximitza l'eficiència de l'aplicació web.

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


## 2.Exemples de Cookies i Sessions en PHP

### Cookies

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

#### Consideracions de seguretat per a cookies:

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

## 3.Autenticació d'usuaris

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

## 4. Referències Addicionals

A continuació es presenten diverses referències que poden ajudar-te a aprofundir en el tema de la gestió de sessions i cookies en PHP.

### Documentació Oficial de PHP

- **Sessions a PHP**: La documentació oficial de PHP proporciona informació detallada sobre l'ús de sessions, incloent-hi exemples pràctics i consells de millors pràctiques.
    - [Sessions a PHP](https://www.php.net/manual/es/book.session.php)

- **Cookies a PHP**: Trobaràs informació oficial sobre com treballar amb cookies en PHP, amb descripcions d'atributs com `HttpOnly`, `Secure` i `SameSite`.
    - [Cookies a PHP](https://www.php.net/manual/es/function.setcookie.php)

### Articles i Blocs Tècnics

- **PHP Sessions: Tips & Tricks**: Aquest article discuteix tècniques avançades per gestionar sessions en PHP, amb exemples i millors pràctiques per a la seguretat.
    - [PHP Sessions: Tips & Tricks](https://www.php.net/manual/en/features.sessions.php)

- **Handling Cookies Securely in PHP**: Una guia sobre com manejar cookies de manera segura, destacant estratègies per protegir les dades de l'usuari.
    - [Handling Cookies Securely in PHP](https://paragonie.com/blog/2015/04/secure-authentication-php-with-long-term-persistence)

### Llibres sobre PHP

- **"Modern PHP: New Features and Good Practices"** de Josh Lockhart: Aquest llibre cobreix les novetats de PHP i les millors pràctiques, incloent la seguretat de sessions i cookies.

- **"PHP Objects, Patterns, and Practice"** de M. Zandstra: Proporciona una visió profunda sobre el disseny de programari amb PHP, incloent-hi aspectes de seguretat relacionats amb sessions i cookies.

### Guies de Seguretat en Desenvolupament Web

- **OWASP Secure Coding Practices**: Aquesta guia de OWASP ofereix una ràpida referència sobre les millors pràctiques de codificació segura, útils per a protegir les teves aplicacions web.
    - [OWASP Secure Coding Practices](https://owasp.org/www-project-secure-coding-practices-quick-reference-guide/)

- **OWASP Cheat Sheet on Session Management**: Una fitxa de referència ràpida de OWASP sobre la gestió de sessions, proporcionant consells de seguretat essencials.
    - [OWASP Cheat Sheet on Session Management](https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html)

### Conferències i Vídeos Educatius

- **PHP Conference YouTube Channel**: El canal de YouTube de PHP Conference ofereix vídeos de conferències i xerrades que cobreixen una varietat de temes, incloent sessions i seguretat.
    - [PHP Conference YouTube Channel](https://www.youtube.com/user/phpvideos)

- **Laracasts**: Ofereix vídeos d'alta qualitat sobre desenvolupament en PHP i Laravel, amb temes rellevants per a sessions i cookies.
    - [Laracasts](https://laracasts.com/)

### Tutorials Online i Plataformes Educatives

- **Stack Overflow PHP Sessions Tag**: Un lloc de consulta on trobar respostes a preguntes freqüents sobre la gestió de sessions en PHP.
    - [Stack Overflow PHP Sessions Tag](https://stackoverflow.com/questions/tagged/php+session)

- **Cursos a Udemy sobre PHP**: Cursos que cobreixen des de conceptes bàsics fins a avançats de PHP, incloent-hi la gestió de sessions i cookies.
    - [Cursos a Udemy sobre PHP](https://www.udemy.com/topic/php/)

## 5.Exercicis

### Bateria d'Exercicis Solucionats per a la Unitat de Programació web

#### Exercici 1: Crear una sessió

1.Crea una pàgina PHP que inicialitze una sessió i emmagatzeme el nom i el rol d'un usuari en variables de sessió. Mostra aquests valors a la pàgina web.

<details>
<summary>Solució</summary>

    ```php
    <?php
    // Iniciar sessió
    session_start();
    
    // Emmagatzemar informació de l'usuari en la sessió
    $_SESSION['nom'] = 'Joan';
    $_SESSION['rol'] = 'Administrador';
    
    echo 'Benvingut, ' . $_SESSION['nom'] . '<br>';
    echo 'Rol: ' . $_SESSION['rol'] . '<br>';
    ?>
    ```
</details>

#### Exercici 2: Regenerar l'ID de sessió

1. Modifica l'exercici anterior per regenerar l'ID de sessió just després d'emmagatzemar la informació de l'usuari.

<details>
<summary>Solució</summary>

    ```php
    <?php
    // Iniciar sessió
    session_start();
    
    // Emmagatzemar informació de l'usuari en la sessió
    $_SESSION['nom'] = 'Joan';
    $_SESSION['rol'] = 'Administrador';
    
    // Regenerar l'ID de sessió
    session_regenerate_id(true);
    
    echo 'Benvingut, ' . $_SESSION['nom'] . '<br>';
    echo 'Rol: ' . $_SESSION['rol'] . '<br>';
    ?>
    ```
</details>

#### Exercici 3: Tancar la sessió

1. Escriu un script PHP que elimine totes les variables de sessió i destrueixi la sessió quan l'usuari tanqui sessió.

<details>
<summary>Solució</summary>

    ```php
    <?php
    // Iniciar sessió
    session_start();
    
    // Eliminar totes les variables de sessió
    session_unset();
    
    // Destruir la sessió
    session_destroy();
    ?>
    ```
</details>

#### Exercici 4: Crear una cookie segura

1. Escriu un script PHP per crear una cookie que emmagatzeme el nom d'usuari amb els atributs de seguretat `HttpOnly`, `Secure` i `SameSite`.

<details>
<summary>Solució</summary>

    ```php
    <?php
    // Crear una cookie segura
    setcookie(
        'nom_usuari',
        'Joan',
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
</details>

#### Exercici 5: Llegir i modificar una cookie

1. Crea una pàgina PHP que llegeixca el valor d'una cookie anomenada `nom_usuari` i la modifique afegint un prefix de salutació.

<details>
<summary>Solució</summary>

    ```php
    <?php
    // Llegir el valor de la cookie
    if (isset($_COOKIE['nom_usuari'])) {
        $nomUsuari = $_COOKIE['nom_usuari'];
        echo 'Hola, ' . $nomUsuari;
    
        // Modificar el valor de la cookie
        $salutacio = 'Hola, ' . $nomUsuari;
        setcookie('nom_usuari', $salutacio, time() + 3600, '/');
    } else {
        echo 'Cookie not found.';
    }
    ?>
    ```
</details>

#### Exercici 6: Aplicació de gestió d'usuaris amb sessions

1. Desenvolupa una aplicació PHP amb dos scripts: un per iniciar sessió i un altre per tancar sessió. L'aplicació ha de permetre que l'usuari introdueixca el seu nom d'usuari i vega un missatge de benvinguda una vegada haja iniciat sessió.

<details>
<summary>Solució</summary>

    ```php
    <!-- login.php -->
    <?php
    session_start();
    
    if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $nomUsuari = $_POST['nom_usuari'];
    
        // Emmagatzemar el nom d'usuari en la sessió
        $_SESSION['nom_usuari'] = $nomUsuari;
    
        // Redireccionar a la pàgina de benvinguda
        header('Location: welcome.php');
        exit();
    }
    ?>
    
    <!DOCTYPE html>
    <html>
    <head>
        <title>Iniciar Sessió</title>
    </head>
    <body>
        <h2>Iniciar Sessió</h2>
        <form method="post" action="login.php">
            <label for="nom_usuari">Nom d'usuari:</label>
            <input type="text" id="nom_usuari" name="nom_usuari" required>
            <button type="submit">Iniciar Sessió</button>
        </form>
    </body>
    </html>

    ```

    ```php
    <!-- logout.php -->
    <?php
    session_start();

    // Tancar sessió de forma segura
    session_unset();
    session_destroy();
    
    // Redireccionar a la pàgina de login
    header('Location: login.php');
    exit();
    ?>
    ```

    ```php
    <!-- wellcome.php -->
    <?php
    session_start();
    
    if (!isset($_SESSION['nom_usuari'])) {
        // Redireccionar a la pàgina de login si no s'ha iniciat sessió
        header('Location: login.php');
        exit();
    }
    
    $nomUsuari = $_SESSION['nom_usuari'];
    ?>
    
    <!DOCTYPE html>
    <html>
    <head>
        <title>Benvingut</title>
    </head>
    <body>
        <h2>Benvingut, <?php echo htmlspecialchars($nomUsuari); ?>!</h2>
        <p>Aquesta és la teva pàgina de benvinguda.</p>
        <a href="logout.php">Tancar Sessió</a>
    </body>
    </html>
    ```

</details>

#### Exercici 7: Aplicació de gestió de preferències amb cookies

1. Crea una aplicació PHP que permeta als usuaris seleccionar el seu color preferit, emmagatzemant aquesta informació en una cookie. La pàgina hauria de mostrar el color preferit de l'usuari en futures visites.

<details>
<summary>Solució</summary>

    ```php
    <?php
    // Llegir el color preferit de la cookie
    $colorPreferit = isset($_COOKIE['color_preferit']) ? $_COOKIE['color_preferit'] : 'blau';
    
    if ($_SERVER['REQUEST_METHOD'] === 'POST') {
        $colorPreferit = $_POST['color_preferit'];
    
        // Emmagatzemar el color preferit en una cookie
        setcookie('color_preferit', $colorPreferit, time() + 3600, '/');
    }
    ?>
    
    <!DOCTYPE html>
    <html>
    <head>
        <title>Preferències de Color</title>
    </head>
    <body style="background-color: <?php echo $colorPreferit; ?>">
        <h2>Preferències de Color</h2>
        <form method="post">
            <label for="color_preferit">Color preferit:</label>
            <select id="color_preferit" name="color_preferit">
                <option value="blau" <?php if ($colorPreferit === 'blau') echo 'selected'; ?>>Blau</option>
                <option value="vermell" <?php if ($colorPreferit === 'vermell') echo 'selected'; ?>>Vermell</option>
                <option value="verd" <?php if ($colorPreferit === 'verd') echo 'selected'; ?>>Verd</option>
            </select>
            <button type="submit">Guardar</button>
        </form>
    </body>
    </html>
    ```
</details>

### Exercicis proposats

#### Exercici 1: Sistema de Carret de Compres sense Base de Dades

1. **Descripció:**

   Desenvolupa una aplicació PHP que permeta als usuaris afegir productes a un carret de compres i mostrar el contingut del carret. Utilitza sessions per a mantindre l'estat del carret entre pàgines.

2. **Requisits:**
    - Crear una pàgina on l'usuari puga seleccionar productes.
    - Afegir els productes seleccionats a un carret emmagatzemat en una sessió.
    - Mostrar un resum del carret amb els productes afegits i les seues quantitats.
    - Permetre que l'usuari elimine productes del carret.


```html
<!DOCTYPE html>
<html lang="ca">
<head>
    <meta charset="UTF-8">
    <title>Selecció de productes</title>
</head>
<body>
    <h1>Afegir productes al carret</h1>
    <form action="carret.php" method="POST">
        <label for="producte">Tria un producte:</label>
        <select name="producte" id="producte">
            <option value="Poma">Poma</option>
            <option value="Plàtan">Plàtan</option>
            <option value="Taronja">Taronja</option>
        </select>
        <input type="submit" value="Afegir al carret">
    </form>
    <a href="carret.php">Veure carret</a>
</body>
</html>
```


#### Exercici 2: Autenticació Bàsica d'Usuaris amb Sessions

1. **Descripció:**

   Crea una aplicació PHP que permeta als usuaris iniciar sessió mitjançant un formulari. Utilitza sessions per a mantindre l'estat d'autenticació de l'usuari i mostrar missatges personalitzats basats en aquest estat.

2. **Requisits:**
    - Crear un formulari d'inici de sessió que sol·licite el nom d'usuari i la contrasenya.
    - Emmagatzemar l'estat d'autenticació en una sessió després de verificar les credencials.
    - Mostrar una pàgina de benvinguda personalitzada per a l'usuari autenticat.
    - Proporcionar un enllaç per a tancar sessió i destruir la sessió.
 
#### Exercici 3: Recordatori d'Usuari amb Cookies

1. **Descripció:**

   Afig una funcionalitat de "recordar-me" a l'exercici anterior que emmagatzeme el nom d'usuari en una cookie i permeta a l'usuari ser recordat en futures visites al lloc web.

2. **Requisits:**
    - Afig una opció de "recordar-me" al formulari d'inici de sessió.
    - Emmagatzemar el nom d'usuari en una cookie quan l'opció és seleccionada.
    - Comprovar la cookie en futures visites i iniciar sessió automàticament si la cookie existeix.
    - Assegurar que les cookies es configuren amb atributs de seguretat adequats (`HttpOnly`, `Secure`, `SameSite`).

#### Exercici 4: Formulari de Contacte amb Protecció CSRF

1. **Descripció:**

   Desenvolupa un formulari de contacte que permeta als usuaris enviar missatges i implementa protecció CSRF per a assegurar que les sol·licituds siguen legítimes.

2. **Requisits:**
    - Crear un formulari de contacte amb camps per al nom, correu electrònic i missatge.
    - Generar i emmagatzemar un token CSRF en una sessió quan es carrega el formulari.
    - Incloure el token CSRF com a camp ocult en el formulari.
    - Verificar el token CSRF quan s'envia el formulari i mostrar un missatge de confirmació si és vàlid.
    - Mostrar un missatge d'error si el token CSRF no és vàlid o no existeix.

#### Exercici 5: Seguiment d'Activitat de l'Usuari amb Sessions

1. **Descripció:**

   Crea un sistema que registre les pàgines visitades per l'usuari durant una sessió i mostre aquesta informació quan l'usuari visita una pàgina d'activitat.

2. **Requisits:**
    - Emmagatzemar una llista de pàgines visitades per l'usuari en una sessió.
    - Actualitzar la llista de pàgines cada vegada que l'usuari visite una nova pàgina.
    - Crear una pàgina que mostre l'historial de pàgines visitades durant la sessió actual.
    - Assegurar que l'historial es restableix quan l'usuari tanca la sessió.

### [Solucions](10solucions.html#tema-3-programacio-web)

## 6. Enunciats dels projectes

### Per als dos projectes 

1. **Autenticació de Jugadors:**
    - Implementa un sistema d'autenticació bàsic que permeta als jugadors iniciar sessió abans de començar el joc. Utilitza sessions per a mantindre l'estat d'autenticació.
    - Ha de servir per als dos jocs, "Penjat" i "4 en Ratlla".
    - Fes que una vegada autenticar l'usuari puga triar a quin joc vol jugar (en la mateix pàgina).
    - Protegeix els jocs per tal que no es puga jugar en cas de no estar autenticat.


### Projecte Penjat

1. **Manteniment de l'Estat del Joc amb Sessions:**
    - Utilitza sessions per a emmagatzemar l'estat actual del joc, incloent la paraula a endevinar, lletres endevinades, i el nombre d'intents restants.
  
2. **Gestió de la Sessió del Joc:**
    - Afegeix funcionalitats per a reiniciar el joc en qualsevol moment, reinicialitzant les variables de sessió per a començar una nova partida.
    - Afegeix una opció per a tancar sessió i finalitzar la partida actual.
    - Afegeix un funció per a saver si el joc ha acabat, ja siga perquè s'han endevinat totes les lletres o s'haguen arribat al màxim número d'intents permesos.
    - Controla el final del joc

3. **Cookies per a Recordar Jugadors:**
    - Implementa cookies per a recordar els jugadors entre visites, permetent que l'usuari siga recordat si selecciona una opció de "Recordar-me" durant l'inici de sessió.

4. **Seguretat i Autenticació:**
    - Implementa un sistema d'autenticació bàsic per a garantir que només els jugadors autenticats puguen accedir al joc.
    - Utilitza sessions per a mantenir l'estat d'autenticació i controlar l'accés a les funcionalitats del joc.
     

#### Consideracions Addicionals

- **Resiliència del Joc:** Implementa la lògica necessària per a manejar intents invàlids i mostrar missatges d'error adequats.
- **Millores d'Interfície:** Afegix un enllaç o botó per a tancar sessió i una opció per a reiniciar el joc.

---

### Projecte "4 en Ratlla"

1. **Gestió de l'Estat de la Graella amb Sessions:**
    - Utilitza sessions per a emmagatzemar l'estat actual de la graella i el torn del jugador. Això permet mantenir la partida entre sol·licituds.

2. **Manteniment de la Sessió entre Jugadors:**
    - Emmagatzema l'identificador de cada jugador en sessions per a assegurar que el torn actual siga persistent entre sol·licituds.
    - Afegeix funcionalitats per a reiniciar el joc en qualsevol moment, reinicialitzant les variables de sessió per a començar una nova partida.
    - Afegeix una opció per a tancar sessió i finalitzar la partida actual.
    - Afegeix un funció per a saver si el joc ha acabat, ja siga perquè s'ha fet 4 en ratlla  o s'haja completat el tauler.
    - Controla el final del joc.
 
3. **Cookies per a la Persistència d'Usuaris:**
    - Permet l'ús de cookies per a recordar els jugadors entre visites si han seleccionat "Recordar-me". Utilitza cookies per a emmagatzemar l'últim jugador autenticat.

4. **Seguretat i Autenticació:**
    - Implementa un sistema d'autenticació bàsic per a garantir que només els jugadors autenticats puguen accedir al joc.
    - Utilitza sessions per a mantenir l'estat d'autenticació i controlar l'accés a les funcionalitats del joc.

5. **Addicional**
    - Implementa la lògica per tal que el segon jugador siga la màquina (pots adaptar i/o millorar l'algorisme de baix).
    - Controla el joc per a que no es puga seguir jugant una vegada acabat.
    - Implementa un sistema de puntuació que otorgue 2 punts al guanyador i 1 a cadascú en cas d'empat.

```php    
 
function jugar(&$graella,$jugadorActual){

       $opponent = $jugadorActual === 1 ? 2 : 1;
   
       // Comprovar si pots guanyar
       for ($col = 1; $col <= COLUMNES; $col++) {
           if (isValidMove($graella, $col)) {
               $tempBoard = $graella;
               $coord = ferMoviment($tempBoard, $col, $jugadorActual);
               
               if (fi_joc($tempBoard, $coord)) {
                   return ferMoviment($graella,$col,$jugadorActual); // Guanyar immediatament
               }
           }
       }
   
       // Comprovar si l'oponent pot guanyar i bloquejar
       for ($col = 1; $col <= COLUMNES; $col++) {
           if (isValidMove($graella, $col)) {
               $tempBoard = $graella;
               $coord = ferMoviment($tempBoard, $col, $opponent);
               if (fi_joc($tempBoard, $coord )) {
                   return ferMoviment($graella,$col,$jugadorActual); // Bloquejar
               }
           }
       }
   
       // Estratègia: buscar el millor moviment
       // Podem afegir més lògica aquí per seleccionar el millor moviment
       $possibles = array();
       for ($col = 1; $col <= COLUMNES; $col++) {
           if (isValidMove($graella, $col)) {
               $possibles[] = $col; 
           }
       }
       if (count($possibles)>2) {
           $random = rand(-1,1);
       }
       $middle = (int) (count($possibles) / 2)+$random;
       $inthemiddle = $possibles[$middle];
       return ferMoviment($graella, $inthemiddle, $jugadorActual); 
   
       return -1; // Totes les columnes estan plenes
}

```

#### Consideracions Addicionals

- **Lògica de Torn de Jugadors:** Implementa la lògica necessària per a canviar de torn entre els jugadors utilitzant sessions.
- **Reinici de Partida:** Afegeix una opció per a reiniciar el joc, que ha de restablir les sessions i permetre començar de nou.
- **Interfície d'Usuari Amigable:** Assegura't que la interfície d'usuari és clara i proporciona indicacions visuals dels moviments i torns dels jugadors.

### Rúbrica d'Avaluació

| Criteri                     | Excel·lent (4)                                             | Bé (3)                                                           | Adequat (2)                                             | Insuficient (1)                                   |
|-----------------------------|------------------------------------------------------------|------------------------------------------------------------------|---------------------------------------------------------|---------------------------------------------------|
| **Funcionalitat del Joc**   | El joc està completament funcional i sense errors.         | El joc està majoritàriament funcional amb errors mínims.         | El joc és funcional, però conté errors significatius.   | El joc no és funcional o està incomplet.          |
| **Ús de Sessions**          | Sessions ben implementades per a mantenir l'estat del joc. | Sessions utilitzades correctament amb alguns problemes menors.   | Sessions utilitzades, però amb deficiències importants. | No s'han utilitzat sessions o són incorrectes.    |
| **Ús de Cookies**           | Cookies ben utilitzades per a recordar els jugadors.       | Cookies utilitzades adequadament amb algunes millores possibles. | Cookies utilitzades amb limitacions evidents.           | No s'han utilitzat cookies o són incorrectes.     |
| **Autenticació d'Usuaris**  | Autenticació segura i efectiva implementada.               | Autenticació implementada amb alguns problemes.                  | Autenticació present però amb deficiències notables.    | No s'ha implementat autenticació o és incorrecta. |
| **Interfície d'Usuari**     | Interfície atractiva i fàcil d'utilitzar.                  | Interfície clara amb algunes millores possibles.                 | Interfície funcional però poc intuïtiva.                | Interfície confusa i difícil d'utilitzar.         |
| **Seguretat**               | Totes les mesures de seguretat implementades correctament. | Seguretat adequada amb algunes millores possibles.               | Mesures de seguretat bàsiques implementades.            | No s'han tingut en compte mesures de seguretat.   |
| **Comentaris i Codi**       | Codi ben comentat i fàcilment llegible.                    | Codi clar amb comentaris adequats.                               | Codi llegible però amb pocs comentaris.                 | Codi desordenat i sense comentaris.               |
| **Innovació i Creativitat** | El projecte mostra innovació significativa.                | Algunes idees creatives han estat implementades.                 | Alguna creativitat present, però limitada.              | Cap creativitat o innovació en el projecte.       |
| **Punts addicionals**       | 1 punt per cadascúna aconseguida.                          |                                                                  |                                                         |                                                   |
  
### Explicació dels Criteris

#### Funcionalitat del Joc

- **Excel·lent (4):** El joc funciona completament segons les especificacions, amb totes les funcionalitats implementades i sense errors. Els jugadors poden interaccionar amb el joc tal com s'esperava i totes les accions es realitzen correctament.

- **Insuficient (1):** El joc no és funcional, falten parts importants del codi o el joc no es pot jugar correctament.

#### Ús de Sessions

- **Excel·lent (4):** Les sessions s'utilitzen eficaçment per a mantenir l'estat del joc i de l'usuari entre sol·licituds. Les dades de la sessió es gestionen de manera adequada per a preservar l'experiència de l'usuari.

- **Insuficient (1):** No s'han utilitzat sessions o la seva implementació és incorrecta, la qual cosa afecta negativament l'experiència de l'usuari.

#### Ús de Cookies

- **Excel·lent (4):** Les cookies s'utilitzen de manera efectiva per a recordar els jugadors entre sessions, amb la configuració adequada d'atributs de seguretat (`HttpOnly`, `Secure`, `SameSite`).

- **Insuficient (1):** No s'han utilitzat cookies o la seva implementació és incorrecta, amb una configuració de seguretat deficient.

#### Autenticació d'Usuaris

- **Excel·lent (4):** L'autenticació dels usuaris és segura i eficient, amb mecanismes adequats per a validar les credencials i protegir la informació dels usuaris.

- **Insuficient (1):** No s'ha implementat un sistema d'autenticació o el sistema present és insegur i defectuós.

#### Interfície d'Usuari

- **Excel·lent (4):** La interfície d'usuari és atractiva, clara i fàcil de navegar, proporcionant una experiència d'usuari òptima.

- **Insuficient (1):** La interfície és confusa, difícil d'utilitzar o inacabada.

#### Seguretat

- **Excel·lent (4):** Totes les mesures de seguretat necessàries han estat implementades, incloent-hi la validació de dades d'entrada, protecció CSRF i altres pràctiques de seguretat recomanades.

- **Insuficient (1):** No s'han tingut en compte mesures de seguretat, deixant el projecte vulnerable a possibles atacs.

#### Comentaris i Codi

- **Excel·lent (4):** El codi està ben comentat, és llegible i segueix bones pràctiques de programació.

- **Insuficient (1):** El codi està desordenat, difícil de llegir i manca de comentaris explicatius.

#### Innovació i Creativitat

- **Excel·lent (4):** El projecte mostra un alt grau d'innovació i creativitat, oferint característiques o enfocaments únics que milloren el joc.

- **Insuficient (1):** El projecte manca de creativitat o innovació, seguint únicament les instruccions bàsiques sense cap valor afegit.

---

#### Notes Addicionals

- **Consistència del Codi:** S'espera que el codi sigui consistent, utilitzant convencions de noms adequades i estructures de codi clares.
- **Adaptació de les Necessitats:** Els criteris poden ser adaptats segons les necessitats específiques del curs o dels projectes individuals.


## 7. Autoavaluació: Gestió de Sessions i Cookies

#### Exercici 1: Funcions de les Cookies

##### Pregunta:
Quina és la funció principal de les cookies en el context del desenvolupament web?

##### Opcions:
<form>
  <input type="radio" id="q1a" name="question1" value="a">
  <label for="q1a">a) Guardar els fitxers de l'usuari al servidor.</label><br>
  <input type="radio" id="q1b" name="question1" value="b">
  <label for="q1b">b) Emmagatzemar informació del client per personalitzar l'experiència d'usuari.</label><br>
  <input type="radio" id="q1c" name="question1" value="c">
  <label for="q1c">c) Executar codi al servidor.</label><br>
  <input type="radio" id="q1d" name="question1" value="d">
  <label for="q1d">d) Controlar la velocitat de la connexió a Internet.</label><br><br>
  <input type="button" value="Comprovar" onclick="checkAnswer1()">
</form>

<p id="result1"></p>

<script>
function checkAnswer1() {
    var correctAnswer = "b";
    var radios = document.getElementsByName('question1');
    var userAnswer;
    for (var i = 0; i < radios.length; i++) {
        if (radios[i].checked) {
            userAnswer = radios[i].value;
            break;
        }
    }
    var resultText = userAnswer === correctAnswer ? "Correcte!" : "Incorrecte. La resposta correcta és b) Emmagatzemar informació del client per personalitzar l'experiència d'usuari.";
    document.getElementById('result1').innerText = resultText;
}
</script>

#### Exercici 2: Seguretat de les Cookies

##### Pregunta:
Quins atributs de seguretat haurien de tindre les cookies per protegir-les contra atacs?

##### Opcions:
<form>
  <input type="checkbox" id="q2a" name="question2" value="a">
  <label for="q2a">a) Secure</label><br>
  <input type="checkbox" id="q2b" name="question2" value="b">
  <label for="q2b">b) HttpOnly</label><br>
  <input type="checkbox" id="q2c" name="question2" value="c">
  <label for="q2c">c) SameSite</label><br>
  <input type="checkbox" id="q2d" name="question2" value="d">
  <label for="q2d">d) CrossSite</label><br><br>
  <input type="button" value="Comprovar" onclick="checkAnswer2()">
</form>

<p id="result2"></p>

<script>
function checkAnswer2() {
    var correctAnswers = ["a", "b", "c"];
    var checkboxes = document.getElementsByName('question2');
    var userAnswers = [];
    for (var i = 0; i < checkboxes.length; i++) {
        if (checkboxes[i].checked) {
            userAnswers.push(checkboxes[i].value);
        }
    }
    userAnswers.sort();
    var resultText = (JSON.stringify(userAnswers) === JSON.stringify(correctAnswers))
        ? "Correcte!"
        : "Incorrecte. Les respostes correctes són a) Secure, b) HttpOnly, c) SameSite.";
    document.getElementById('result2').innerText = resultText;
}
</script>

#### Exercici 3: Creació de Sessions en PHP

##### Pregunta:
Quin dels següents passos és necessari per iniciar una sessió en PHP?

##### Opcions:
<form>
  <input type="radio" id="q3a" name="question3" value="a">
  <label for="q3a">a) Cridar a la funció session_start().</label><br>
  <input type="radio" id="q3b" name="question3" value="b">
  <label for="q3b">b) Utilitzar la funció session_open().</label><br>
  <input type="radio" id="q3c" name="question3" value="c">
  <label for="q3c">c) Assignar un valor a la variable $_SESSION.</label><br>
  <input type="radio" id="q3d" name="question3" value="d">
  <label for="q3d">d) No es necessita cap funció especial.</label><br><br>
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
    var resultText = userAnswer === correctAnswer ? "Correcte!" : "Incorrecte. La resposta correcta és a) Cridar a la funció session_start().";
    document.getElementById('result3').innerText = resultText;
}
</script>

#### Exercici 4: Manteniment d'Informació en Sessions

##### Pregunta:
Com es pot mantindre la informació d'un usuari durant la sessió d'una aplicació web?

##### Opcions:
<form>
  <input type="radio" id="q4a" name="question4" value="a">
  <label for="q4a">a) Utilitzant la variable global $GLOBALS.</label><br>
  <input type="radio" id="q4b" name="question4" value="b">
  <label for="q4b">b) Utilitzant la variable $_SESSION.</label><br>
  <input type="radio" id="q4c" name="question4" value="c">
  <label for="q4c">c) Utilitzant la variable $_COOKIE.</label><br>
  <input type="radio" id="q4d" name="question4" value="d">
  <label for="q4d">d) Utilitzant arxius temporals al servidor.</label><br><br>
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
    var resultText = userAnswer === correctAnswer ? "Correcte!" : "Incorrecte. La resposta correcta és b) Utilitzant la variable $_SESSION.";
    document.getElementById('result4').innerText = resultText;
}
</script>

#### Exercici 5: Funcions de PHP per a Sessions

##### Pregunta:
Quina funció de PHP es fa servir per destruir una sessió?

##### Opcions:
<form>
  <input type="radio" id="q5a" name="question5" value="a">
  <label for="q5a">a) session_destroy()</label><br>
  <input type="radio" id="q5b" name="question5" value="b">
  <label for="q5b">b) session_unset()</label><br>
  <input type="radio" id="q5c" name="question5" value="c">
  <label for="q5c">c) session_delete()</label><br>
  <input type="radio" id="q5d" name="question5" value="d">
  <label for="q5d">d) session_end()</label><br><br>
  <input type="button" value="Comprovar" onclick="checkAnswer5()">
</form>

<p id="result5"></p>

<script>
function checkAnswer5() {
    var correctAnswer = "a";
    var radios = document.getElementsByName('question5');
    var userAnswer;
    for (var i = 0; i < radios.length; i++) {
        if (radios[i].checked) {
            userAnswer = radios[i].value;
            break;
        }
    }
    var resultText = userAnswer === correctAnswer ? "Correcte!" : "Incorrecte. La resposta correcta és a) session_destroy().";
    document.getElementById('result5').innerText = resultText;
}
</script>

#### Exercici 6: Avantatges de les Sessions

##### Pregunta:
Quins són els avantatges d'utilitzar sessions en lloc de cookies per a mantenir l'estat de l'usuari?

##### Opcions:
<form>
  <input type="checkbox" id="q6a" name="question6" value="a">
  <label for="q6a">a) Les sessions poden emmagatzemar més informació perquè es guarden al servidor.</label><br>
  <input type="checkbox" id="q6b" name="question6" value="b">
  <label for="q6b">b) Les sessions són més segures perquè no s'envien al client.</label><br>
  <input type="checkbox" id="q6c" name="question6" value="c">
  <label for="q6c">c) Les sessions redueixen la càrrega del servidor.</label><br>
  <input type="checkbox" id="q6d" name="question6" value="d">
  <label for="q6d">d) Les sessions no necessiten ser configurades amb atributs de seguretat.</label><br><br>
  <input type="button" value="Comprovar" onclick="checkAnswer6()">
</form>

<p id="result6"></p>

<script>
function checkAnswer6() {
    var correctAnswers = ["a", "b"];
    var checkboxes = document.getElementsByName('question6');
    var userAnswers = [];
    for (var i = 0; i < checkboxes.length; i++) {
        if (checkboxes[i].checked) {
            userAnswers.push(checkboxes[i].value);
        }
    }
    userAnswers.sort();
    var resultText = (JSON.stringify(userAnswers) === JSON.stringify(correctAnswers))
        ? "Correcte!"
        : "Incorrecte. Les respostes correctes són a) Les sessions poden emmagatzemar més informació perquè es guarden al servidor, b) Les sessions són més segures perquè no s'envien al client.";
    document.getElementById('result6').innerText = resultText;
}
</script>

#### Exercici 7: Autenticació d'Usuaris

##### Pregunta:
Quina és la pràctica recomanada per assegurar la identitat d'un usuari en una aplicació web?

##### Opcions:
<form>
  <input type="radio" id="q7a" name="question7" value="a">
  <label for="q7a">a) Utilitzar noms d'usuari i contrasenyes emmagatzemades com a cookies.</label><br>
  <input type="radio" id="q7b" name="question7" value="b">
  <label for="q7b">b) Utilitzar sessions per mantenir l'estat d'autenticació després d'iniciar sessió.</label><br>
  <input type="radio" id="q7c" name="question7" value="c">
  <label for="q7c">c) Emmagatzemar la contrasenya de l'usuari a la URL.</label><br>
  <input type="radio" id="q7d" name="question7" value="d">
  <label for="q7d">d) No utilitzar cap forma d'autenticació.</label><br><br>
  <input type="button" value="Comprovar" onclick="checkAnswer7()">
</form>

<p id="result7"></p>

<script>
function checkAnswer7() {
    var correctAnswer = "b";
    var radios = document.getElementsByName('question7');
    var userAnswer;
    for (var i = 0; i < radios.length; i++) {
        if (radios[i].checked) {
            userAnswer = radios[i].value;
            break;
        }
    }
    var resultText = userAnswer === correctAnswer ? "Correcte!" : "Incorrecte. La resposta correcta és b) Utilitzar sessions per mantenir l'estat d'autenticació després d'iniciar sessió.";
    document.getElementById('result7').innerText = resultText;
}
</script>
# Desenvolupament d'Aplicacions Web: POO, Separació de Lògica i Presentació, Gestió d'Errors i Proves

??? abstract "Duració i criteris d'avaluació"

    Duració estimada: 20 hores

    <hr />

    | Resultat d'aprenentatge | Criteris d'avaluació |
    | --------                | --------             |
    | 5. Desenvolupa aplicacions Web identificant i aplicant mecanismes per a separar el codi de presentació de la lògica de negoci.| a) S'han identificat els avantatges de separar la lògica de negoci dels aspectes de presentació de l'aplicació. <br/> b) S'han analitzat tecnologies i mecanismes que permeten realitzar aquesta separació i les seues característiques principals. <br/> c) S'han utilitzat objectes i controls en el servidor per a generar l'aspecte visual de l'aplicació Web en el client. <br/> d) S’han utilitzat formularis generats de forma dinàmica per a respondre als esdeveniments de l'aplicació Web. <br/> e) S'han identificat i aplicat els paràmetres relatius a la configuració de l'aplicació Web. <br/> f) S'han escrit aplicacions Web amb manteniment d'estat i separació de la lògica de negoci. <br/> g) S'han aplicat els principis de la programació orientada a objectes. <br/> g) S'ha provat i documentat el codi. |


## 1. Concepte de classes i Objectes

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

## 2. Principis de la POO 

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

``` php hl_lines="5"
<?php
class Persona {
    private string $nombre;

    public function __construct(string $nom) {
        $this->nombre = $nom;
    }

    public function imprimir(){
      echo $this->nombre;
      echo '<br>';
    }
}

$bruno = new Persona("Bruno Díaz");
$bruno->imprimir();
```

##### Constructors en PHP 8

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

#### Introspecció

En treballar amb classes i objectes, existeixen un conjunt de funcions ja definides pel llenguatge que permeten obtindre informació sobre els objectes:

* `instanceof`: permet comprovar si un objecte és d'una determinada classe
* `get_class`: retorna el nom de la classe
* `get_declared_class`: retorna un array amb els noms de les classes definides
* `class_àlies`: crea un àlies
* `class_exists` / `method_exists` / `property_exists`: `true` si la classe / mètode / propietat està definida
* `get_class_methods` / `get_class_vars` / `get_object_vars`: Retorna un array amb els noms dels mètodes / propietats d'una classe / propietats d'un objecte que són accessibles des d'on es fa la crida.

Un exemple d'aquestes funcions pot ser el següent:

``` php
<?php
$p = new Producto("PS5");
if ($p instanceof Producto) {
    echo "Es un producto";
    echo "La clase es ".get_class($p);

    class_alias("Producto", "Articulo");
    $c = new Articulo("Nintendo Switch");
    echo "Un articulo es un ".get_class($c);

    print_r(get_class_methods("Producto"));
    print_r(get_class_vars("Producto"));
    print_r(get_object_vars($p));

    if (method_exists($p, "mostrarResumen")) {
        $p->mostrarResumen();
    }
}
```
!!! caution "Clonat"
    En assignar dos objectes no es copien, es crea una nova referència. Si volem una còpia, cal clonar-ho mitjançant el mètode `clone(object) : object`

    Si volem modificar el clonat per defecte, cal definir el mètode màgic `__clone()` que es dirà després de copiar totes les propietats.

    Més informació en <https://www.php.net/manual/es/language.oop5.cloning.php>

### Herència

PHP suporta herència simple, de manera que una classe només pot heretar d'una altra, no de dues classes alhora. Per a això s'utilitza la paraula clau `extends`. Si volem que la classe A hereta de la classe B farem:

``` php
class A extends B
```

El fill hereta els atributs i mètodes públics i protegits.

!!! warning "Cada classe en un arxiu"
Com ja hem comentat, hauríem de col·locar cada classe en un arxiu diferent per a posteriorment utilitzar-lo mitjançant `include`. En els següent exemple els hem col·locats junt per a facilitar la seua llegibilitat.

Per exemple, tenim una classe `Producte` i una `Tv` que hereta de `Producte`:

``` php
<?php
class Producto {
    public $codigo;
    public $nombre;
    public $nombreCorto;
    public $PVP;

    public function mostrarResumen() {
        echo "<p>Prod:".$this->codigo."</p>";
    }
}

class Tv extends Producto {
    public $pulgadas;
    public $tecnologia;
}
```

Podemos utilizar las siguientes funciones para averiguar si hay relación entre dos clases:

* `get_parent_class(object): string`
* `is_subclass_of(object, string): bool`

``` php
<?php
$t = new Tv();
$t->codigo = 33;
if ($t instanceof Producto) {
    echo $t->mostrarResumen();
}

$padre = get_parent_class($t);
echo "<br>La clase padre es: " . $padre;
$objetoPadre = new $padre;
echo $objetoPadre->mostrarResumen();

if (is_subclass_of($t, 'Producto')) {
    echo "<br>Soy un hijo de Producto";
}
```

### Polimorfisme

Podem crear mètodes en els fills amb el mateix nom que el pare, canviant el seu comportament.
Per a invocar als mètodes del pare -> `parent::nombreMetodo()`

``` php
<?php
class Tv extends Producto {
   public $pulgadas;
   public $tecnologia;

   public function mostrarResumen() {
      parent::mostrarResumen();
      echo "<p>TV ".$this->tecnologia." de ".$this->pulgadas."</p>";
   }
}
```

#### Constructor en fills

En els fills no es crea cap constructor de manera automàtica. Pel que si no n'hi ha, s'invoca automàticament al del pare. En canvi, si el definim en el fill, hem d'invocar al del pare de manera explícita.

=== "PHP7"

    ``` php
    <?php
    class Producto {
        public string $codigo;

        public function __construct(string $codigo) {
            $this->codigo = $codigo;
        }

        public function mostrarResumen() {
            echo "<p>Prod:".$this->codigo."</p>";
        }
    }
    
    class Tv extends Producto {
        public $pulgadas;
        public $tecnologia;

        public function __construct(string $codigo, int $pulgadas, string $tecnologia) {
            parent::__construct($codigo);
            $this->pulgadas = $pulgadas;
            $this->tecnologia = $tecnologia;
        }

        public function mostrarResumen() {
            parent::mostrarResumen();
            echo "<p>TV ".$this->tecnologia." de ".$this->pulgadas."</p>";
        }
    }
    ```

=== "PHP8"

    ``` php
    <?php
    class Producto {
        public function __construct(private string $codigo) { }

        public function mostrarResumen() {
            echo "<p>Prod:".$this->codigo."</p>";
        }        
    }
    
    class Tv extends Producto {

        public function __construct(
            string $codigo,
            private int $pulgadas,
            private string $tecnologia)
        {
            parent::__construct($codigo);
        }

        public function mostrarResumen() {
            parent::mostrarResumen();
            echo "<p>TV ".$this->tecnologia." de ".$this->pulgadas."</p>";
        }
    }
    ```

### Abstracció

Les classes abstractes obliguen a heretar d'una classe, ja que no es permet la seua instanciación. Es defineix mitjançant `abstract class NombreClase {`.
Una classe abstracta pot contindre propietats i mètodes no-abstractes, i/o mètodes abstractes.

``` php
<?php
// Clase abstracta
abstract class Producto {
    private $codigo;
    public function getCodigo() : string {
        return $this->codigo;
    }
    // Método abstracto
    abstract public function mostrarResumen();
}
```

Quan una classe hereta d'una classe abstracta, obligatòriament ha d'implementar els mètodes que té el pare marcats com a abstractes.

``` php
<?php
class Tv extends Producto {
    public $pulgadas;
    public $tecnologia;

    public function mostrarResumen() { //obligado a implementarlo
        echo "<p>Código ".$this->getCodigo()."</p>";
        echo "<p>TV ".$this->tecnologia." de ".$this->pulgadas."</p>";
    }
}

$t = new Tv();
echo $t->getCodigo();
```

#### Classes finals

Són classes oposades a abstractes, ja que eviten que es puga heretar una classe o mètode per a sobreescriure-ho.

``` php
<?php
class Producto {
    private $codigo;

    public function getCodigo() : string {
        return $this->codigo;
    }

    final public function mostrarResumen() : string {
        return "Producto ".$this->codigo;
    }
}

// No podremos heredar de Microondas
final class Microondas extends Producto {
    private $potencia;

    public function getPotencia() : int {
        return $this->potencia;
    }

    // No podemos implementar mostrarResumen()
}
```

#### Interfícies

Permet definir un contracte amb les signatures dels mètodes a complir. Així doncs, només conté declaracions de funcions i totes han de ser públiques.

Es declaren amb la paraula clau `interface` i després les classes que complisquen el contracte el realitzen mitjançant la paraula clau `implements`.

``` php
<?php
interface Nombreable {
// declaración de funciones
}
class NombreClase implements NombreInterfaz {
// código de la clase
```

Es permet l'herència d'interfícies. A més, una classe pot implementar diverses interfícies (en aquest cas, sí que suporta l'herència múltiple, però només d'interfícies).

``` php
<?php
interface Mostrable {
    public function mostrarResumen() : string;
}

interface MostrableTodo extends Mostrable {
    public function mostrarTodo() : string;
}

interface Facturable {
    public function generarFactura() : string;
}

class Producto implements MostrableTodo, Facturable {
    // Implementaciones de los métodos
    // Obligatoriamente deberá implementar public function mostrarResumen, mostrarTodo y generarFactura
}
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

#### Accés

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

## 4. Composer

<figure style="float: right;">
    <img src="imagenes/05/logo-composer.png" width="200">
    <figcaption>Logo Composer</figcaption>
</figure>

Eina per excel·lència en PHP per a la gestió de llibreries i dependències, de manera que instal·la i les actualitza assegurant que tot l'equip de desenvolupament té el mateix entorn i versions. A més, ofereix *autoloading* del nostre codi, de manera que no hàgem de fer-lo nosaltres "a mà".

Està escrit en PHP, i podeu consultar tota la seua documentació en [https://getcomposer.org/](https://getcomposer.org/).

Utilitza [*Packagist*]( https://packagist.org/) com a repositori de llibreries.

Funcionalment, és similar a Maven (Java) / npm (JS).

### Instal·lació

Si estem usant XAMPP, hem d'instal·lar *Composer* en el propi sistema operatiu. Es recomana seguir les [instruccions oficials](https://getcomposer.org/doc/00-intro.md) segons el sistema operatiu a emprar.

En canvi, si usem *Docker*, necessitem modificar la configuració del nostre contenidor. En el nostre cas, hem decidit modificar l'arxiu `Dockerfile` i afegir el següent comando:

``` docker
COPY --from=composer:2.0 /usr/bin/composer /usr/local/bin/composer
```

És important que dins del contenidor comprovem que tenim la v2:

``` bash
composer -V
```

### Primers passos

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

### Actualitzar llibreries

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

### `autoload.php`

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


## 5. Logger amb Monolog

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

### Nivells

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

    
### Hola Monolog

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

### Funcionament

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


### Manejadors

 Si no s'indica cap, se li assigna un per defecte. L'últim manejador inserit serà el primer a executar-se.
Després es van executant conforme a la pila.


### Processadors

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

### Formatadors

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


## 6.  Generació de PDF amb DOMPDF


Amb PHP podem manejar tot tipus d'arxius com ja hem vist però, què passa si volem generar fitxers PDF amb dades tretes d'una base de dades?

<div class="center img-small">
    <img src="imagenes/06/06-pdf.png">
</div>


Gràcies a una classe escrita en PHP, podem generar arxius PDF sense necessitat d'instal·lar llibreries addicionals en el nostre servidor.
Però anem a utilitzar una llibreria que permet transformar codi html en pdf.

### DOMPDF

Afegirem la llibreria de [*DOMPDF*](https://github.com/seldaek/monolog) al nostre projecte. Per a això, inclourem la llibreria en el nostre projecte amb:

``` bash
composer require dompdf/dompdf
```
Una vegada que DOMPDF està instal·lat, el procés per generar PDFs des de HTML és bastant directe. Els passos bàsics són:

Pas 1: Incloent DOMPDF
Primer, necessitarem incloure DOMPDF en el script PHP. Si estem utilitzant Composer, això es fa automàticament a través de l'auto-càrrega de Composer. Només cal afegir la següent línia al principi del'script:

```php
require 'vendor/autoload.php';
```

Pas 2: Creació d'una Instància de DOMPDF
A continuació, creem una nova instància de la classe DOMPDF:

```php

use Dompdf\Dompdf;

$dompdf = new Dompdf();
```

Pas 3: Carregar HTML
Després, carregem l'HTML en l'objecte DOMPDF. Això es pot fer directament com una cadena o carregant un fitxer HTML:

```php
$html = "<html><body>Hola, això és una prova.</body></html>";
$dompdf->loadHtml($html);
```

O bé carregar un fitxer HTML:

```php
$dompdf->loadHtml(file_get_contents('path/to/your/file.html'));
```

Pas 4: Configuració de la Mida del Paper i l'Orientació
Podem configurar la mida del paper i l'orientació si és necessari:

```php
$dompdf->setPaper('A4', 'portrait'); // o 'landscape'
```

Pas 5: Renderització del PDF
Ara, demanem a DOMPDF que renderitze el PDF:

```php
$dompdf->render();
```

Pas 6: Eixida del PDF
Finalment, podem enviar el PDF al navegador, guardar-lo en un fitxer o fer amb ell el que necessitem:

Per mostrar-lo al navegador:

```php
$dompdf->stream("document.pdf", array("Attachment" => false));
```

Per desar-lo en un fitxer:

```php
$output = $dompdf->output();
file_put_contents('path/to/save/document.pdf', $output);
```

##### Consells Addicionals
Cal assegurar-se que l'HTML és vàlid i ben format. DOMPDF intenta ser tolerant amb l'HTML, però l'HTML mal format pot causar problemes.
El CSS que s'utilitze pot afectar significativament com es veu el PDF. DOMPDF suporta una bona part de CSS 2.1, però no tot.
Si necessitem incloure imatges, cal assegurar-se que les rutes són absolutes i accessibles des del servidor on s'executa DOMPDF.
Aquesta és una guia bàsica per començar amb DOMPDF. Per a casos d'ús més avançats i opcions de configuració, cal consultar la documentació oficial de DOMPDF.


## 7. Documentación con **phpDocumentor**



[phpDocumentor](https://www.phpdoc.org/) és l'eina per a documentar el codi PHP. És similar en propòsit i funcionament a **Javadoc**.

Així doncs, és un eina que facilita la documentació del codi PHP, creant un lloc web amb l'API de l'aplicació.

Es basa en l'ús d'anotacions sobre els docblocks. Per a posar-ho en marxa, en el nostre cas ens decantarem per utilitzar la imatge que ja existeix de Docker.

### Instal·lació

##### Pas 1: Instal·lació amb Docker
Primer, cal assegurar-se tenir Docker instal·lat i funcionant al  sistema. Després, s'ha de descarregar i executar el contenidor de phpDocumentor utilitzant la següent comanda:

``` bash
docker pull phpdoc/phpdoc
```

#####  Pas 2: Generació de Documentació

Un cop tinguem la imatge, podem utilitzar-la per generar la documentació. El procés bàsic implica muntar els fitxers de codi dins del contenidor Docker i executar phpDocumentor sobre aquests fitxers.

Ací hi ha un exemple de com fer-ho:

En el cas d'usar *Docker*, usarem el següent comando per a executar-lo (crea el contenidor, executa el comando que li demanem, i automàticament l'esborra):

``` bash
docker run --rm -v $(pwd):/data phpdoc/phpdoc:latest run -d /data/src -t /data/src/docs

```
Aquesta comanda fa el següent:

        * -rm: Això elimina el contenidor després d'executar-lo, així no es queden contenidors inactius.
        * -v $(pwd):/data: Munta el directori actual del teu sistema ($(pwd)) al directori /data dins del contenidor. Hauràs de reemplaçar $(pwd) amb el camí on està el teu codi font si no estàs executant aquesta comanda des del directori del teu projecte.
        * -d /data/src: Especifica el directori dins del contenidor on es troba el teu codi font. Reemplaça /data/src amb el camí corresponent dins del contenidor si és diferent.
        * -t /data/src/docs: Especifica on vols que es generi la documentació dins del contenidor. En aquest cas, es generarà dins de /data/docs.

##### Pas 3: Accés a la Documentació Generada
Una vegada generada, la documentació estarà dins del directori que especificat (en aquest cas, `docs` dins del directori docs de projecte). Pots obrir els fitxers HTML amb qualsevol navegador per veure la documentació.


### DocBlock

Un *docblock* és el bloc de codi que es col·loca damunt d'un recurs. El seu format és:

``` php
<?php
/**
* Sumari*, una sola línia

* Descripció* que pot utilitzar diverses línies
* i que ofereix detalls de l'element o referències
* per a ampliar la informació

* @param string $miArgumento amb una descripció* de l'argument
* que pot usar diverses línies.

* @return void
*/
function miFuncion(tipo $miArgumento)
{
}
```
!!! tip "Visual Studio Code"
    Per tal que us ajude a documentar podeu utilitzar l'extensió  PHP DocBlocker.

### Documentant el codi

En tots els elements, ademas del sumari i/o descripció, posarem:

* En les classes:
    * `@author` nom <email>
    * `@package` ruta del namespace
* En les propietats:
    * `@var` tipus descripció
* En els mètodes:
    * `@param` tipus $nomene descripció
    * `@throws` ClaseException descripció
    * `@return` tipus descripció

Vegem-ho amb un exemple. Suposem que tenim una classe que representa un client:

``` php
<?php
/**
* Classe que representa un client
* 
* El client s'encarrega d'emmagatzemar els suports que té llogat,
* de manera que podem llogar i retornar productes mitjançant les operacions
* homònimes.
* 
* @package Dwes\Videoclub\Model
* @author Aitor Medrano <a.medrano@edu.gva.es>
*/
class Cliente {

    public string $nombre; 
    private string $numero;

    /**
    * Colecció de soports alquilats
    * @var array<Soporte> 
    */
    private $soportesAlquilados[];

    /*
    * Comprova si el suport rebut ja el té llogat el client
    * @param Suport $suporte Suport a comprovar
    * @return bool true si ho té llogat
    /
    public function tieneAlquilado(Soporte $soporte) : bool { 
        // ...
    }
```

Si generem la documentació i obrim amb un navegador l'arxiu `docs/api/index.html` podrem navegar fins a la classe `Client:

<figure style="align: center;">
    <img src="imagenes/05/phpdoc.png">
    <figcaption>phpDocumentor de Cliente</figcaption>
</figure>

## 8. Separar la lògica de negoci dels aspectes de presentació de l'aplicació

#### Lògica de Negoci
- Regles i procediments que defineixen el funcionament de l'aplicació.
- Inclou processament de dades, càlculs, interaccions amb la base de dades, etc.

#### Aspectes de Presentació
- Manera en què es mostra la informació a l'usuari.
- Inclou la interfície d'usuari, disseny, navegació, etc.

### Avantatges

1. **Mantenibilitat**
    - Facilita la modificació de la lògica de negoci sense afectar la presentació.
    - Permet actualitzar la interfície d'usuari sense modificar la lògica subjacent.

2. **Reutilització**
    - La lògica de negoci pot ser reutilitzada en diferents aplicacions amb interfícies variades.
    - Els components de presentació poden ser reutilitzats amb diferents lògiques de negoci.

3. **Escalabilitat**
    - Ajuda a escalar l'aplicació separant les preocupacions, permetent millorar una part sense impactar l'altra.

4. **Prova i Depuració**
    - Facilita les proves unitàries i la depuració en permetre provar la lògica de negoci per separat de la interfície.

5. **Col·laboració**
    - Permet que desenvolupadors de backend i frontend treballen de manera independent en les seues àrees respectives.

### Tecnologies i Mecanismes per a la Separació

A continuació es presenten diverses tecnologies i mecanismes que faciliten la separació de la lògica de negoci i la presentació en una aplicació web:

#### Frameworks PHP:
Laravel: Framework que segueix el patró MVC (Model-View-Controller). Laravel facilita la creació de codi net i ben organitzat, separant clarament la lògica de negoci de la presentació.
Symfony: Altres frameworks populars que també segueixen el patró MVC i ofereixen eines per a la separació de la lògica i la presentació.

#### Patró MVC:
Model-View-Controller: Patró de disseny que divideix una aplicació en tres components interconnectats:
Model: Gestiona la lògica de negoci i les dades.
Vista: Gestiona la presentació de la informació.
Controlador: Gestiona la comunicació entre el Model i la Vista.

#### Plantilles:
Blade (Laravel): Motor de plantilles que permet separar el codi HTML de la lògica de negoci.
Twig (Symfony): Motor de plantilles similar a Blade, utilitzat per separar la lògica de negoci del codi de presentació.

#### API REST:
Permet crear serveis web que exposen funcionalitats i dades a través de punts finals d'API, mantenint la lògica de negoci separada de la presentació.

### Exemple MVC

```php
// Model: Product.php
class Product {
    private string $name;
    private float $price;
    
    public function __construct(string $name, float $price) {
        $this->name = $name;
        $this->price = $price;
    }
    
    public function getName(): string {
        return $this->name;
    }
    
    public function getPrice(): float {
        return $this->price;
    }
}

// Controller: ProductController.php
class ProductController {
    public function showProduct() {
        $product = new Product("Laptop", 1200.00);
        include 'views/productView.php';
    }
}

// View: productView.php
<!DOCTYPE html>
<html>
<head>
    <title>Product Information</title>
</head>
<body>
    <h1>Product: <?php echo htmlspecialchars($product->getName()); ?></h1>
    <p>Price: $<?php echo htmlspecialchars($product->getPrice()); ?></p>
</body>
</html>
```
La separació de la lògica de negoci dels aspectes de presentació és crucial per al desenvolupament d'aplicacions web eficients, mantenibles i escalables.


## 9. Gestió d'Exempcions


La gestió d'excepcions forma part des de PHP 5. El seu funcionament és similar a Java*, fent ús d'un bloc `try / catch / finally`.
Si detectem una situació anòmala i volem llançar una excepció, haurem de realitzar `throw new Exception` (adjuntant el missatge que l'ha provocat).

``` php
<?php
try {
    if ($divisor == 0) {
        throw new Exception("División por cero.");
    }
    $resultado = $dividendo / $divisor;
} catch (Exception $e) {
    echo "Se ha producido el siguiente error: ".$e->getMessage();
}
```

La classe `Exception` és la classe pare de totes les excepcions. El seu constructor rep `missatge[,codigoError][,excepcionPrevia]`.

A partir d'un objecte `Exception`, podem accedir als mètodes `getMessage()`i `getCode()` per a obtindre el missatge i el codi d'error de l'excepció capturada.

El propi llenguatge ofereix un conjunt d'excepcions ja definides, les quals podem capturar (i llançar des de PHP 7). Es recomana la seua consulta en la [documentació oficial](https://www.php.net/manual/es/class.exception.php).

#### Creant exempcions

Per a crear una excepció, la forma més curta és crear una classe que únicament herete de `Exception`.

``` php
<?php
class HolaExcepcion extends Exception {}
```

Si volem, i és recomanable depenent dels requisits, podem sobrecarregar els mètodes màgics, per exemple, sobrecarregant el constructor i cridant al constructor del pare, o reescriure el mètode `__toString` per a canviar el seu missatge:

``` php
<?php
class MiExcepcion extends Exception {
    public function __construct($msj, $codigo = 0, Exception $previa = null) {
        // código propio
        parent::__construct($msj, $codigo, $previa);
    }
    public function __toString() {
        return __CLASS__ . ": [{$this->code}]: {$this->message}\n";
    }
    public function miFuncion() {
        echo "Una función personalizada para este tipo de excepción\n";
    }
}
```

Si definim una excepció d'aplicació dins d'un *namespace*, quan referenciem a `Exception`, haurem de referenciar-la mitjançant el seu nom totalment qualificat (`\Exception`), o utilitzant `use`:

=== "Mitjançant nom totalment qualificat"
    ``` php
    <?php
    namespace \Dwes\Ejemplos;

    class AppExcepcion extends \Exception {}
    ```
=== "Mitjançant `use`"
    ``` php
    <?php
    namespace \Dwes\Ejemplos;

    use Exception;

    class AppExcepcion extends Exception {}
    ```

##### Exempcions múltiples

Es poden usar excepcions múltiples per a comprovar diferents condicions. A l'hora de capturar-les, es fa de més específica a més general.

``` php
<?php
$email = "ejemplo@ejemplo.com";
try {
    // Comprueba si el email es válido
    if(filter_var($email, FILTER_VALIDATE_EMAIL) === FALSE) {
        throw new MiExcepcion($email);
    }
    // Comprueba la palabra ejemplo en la dirección email
    if(strpos($email, "ejemplo") !== FALSE) {
        throw new Exception("$email es un email de ejemplo no válido");
    }
} catch (MiExcepcion $e) {
    echo $e->miFuncion();
} catch(Exception $e) {
    echo $e->getMessage();
}
```

!!! question "Autoevaluación"
    ¿Qué pasaría al ejectuar el siguiente código?
    ``` php
    <?php
    class MainException extends Exception {}
    class SubException extends MainException {}

    try {
        throw new SubException("Lanzada SubException");
    } catch (MainException $e) {
        echo "Capturada MainException " . $e->getMessage();
    } catch (SubException $e) {
        echo "Capturada SubException " . $e->getMessage();
    } catch (Exception $e) {
        echo "Capturada Exception " . $e->getMessage();
    }
    ```

Si en el mateix `catch` volem capturar diverses excepcions, hem d'utilitzar l'operador `|`:

``` php
<?php
class MainException extends Exception {}
class SubException extends MainException {}

try {
    throw new SubException("Lanzada SubException");
} catch (MainException | SubException $e ) {
    echo "Capturada Exception " . $e->getMessage();
}
```

Des de PHP 7, existeix el tipus `Throwable`, el qual és una interfície que implementen tant els errors com les excepcions, i ens permet capturar els dos tipus alhora:

``` php
<?php
try {
    // tu codigo
} catch (Throwable $e) {
    echo 'Forma de capturar errores y excepciones a la vez';
}
```

Si només volem capturar els errors fatals, podem fer ús de la classe `Error`:

``` php
<?php
try {
    // Genera una notificación que no se captura
    echo $variableNoAsignada;
    // Error fatal que se captura
    funcionQueNoExiste();
} catch (Error $e) {
    echo "Error capturado: " . $e->getMessage();
}
```

#### Rellançar exempcions

En les aplicacions reals, és molt comuna capturar una excepció de sistema i llançar una d'aplicació que hem definit nostros.
També podem llançar les excepcions sense necessitat d'estar dins d'un `try/catch`.

``` php
<?php
class AppException extends Exception {}

try {
    // Código de negocio que falla
} catch (Exception $e) {
    throw new AppException("AppException: ".$e->getMessage(), $e->getCode(), $e);
}
```

## 10. Proves amb PHPUNIT

El curs passat, dins del mòdul de Entorns de Desenvolupament, estudiarieu la importància de la realització de proves, així com les proves unitàries mitjançant [JUnit](https://junit.org/junit5/).

<figure style="float: right;">
    <img src="imagenes/05/tdd.png" width="300">
    <figcaption>Test Driven Development</figcaption>
</figure>

Hui dia és de gran importància seguir una bona metodologia de proves, sent el desenvolupament dirigit per les proves (Test Driven Development / TDD) un dels enfocaments més emprats, el qual consisteix en:

1. Escriure el test, i com no hi ha codi implementat, la prova falle (roig).
2. Escriure el codi d'aplicació perquè la prova funcione (verda).
3. refactoritzar el codi de l'aplicació amb l'ajuda de la prova per a comprovar que no trenquem res (refactor).

En el cas de PHP, l'eina que s'utilitza és **PHPUnit** (<https://phpunit.de/>), que com el seu nom indica, està basada en JUnit. La versió actual és la 11.

### Introducció a PHPUnit

PHPUnit és un framework de proves popular per a PHP que suporta tant proves unitàries com proves d'integració. És àmpliament utilitzat en la comunitat PHP per la seua simplicitat i eficàcia. Les proves unitàries es centren en provar components o mètodes individuals, mentre que les proves d'integració asseguren que les diferents parts del sistema funcionen conjuntament com s'espera.

#### Instal·lació

Per començar a utilitzar PHPUnit, cal instal·lar-lo. La manera recomanada és a través de Composer. Executa la següent comanda en el terminal:

```bash
composer require --dev phpunit/phpunit
```
 
Aquesta comanda afegirà PHPUnit com a dependència de desenvolupament en el teu projecte.

!!! tip "Llibreries de desenvolupament"
    Les llibreries que es col·loquen en `require-dev` són les de desenvolupament i *testing*, de manera que no s'instal·laran en un entorn de producció.

Una vegada instal·lat, podem configurar PHPUnit creant un fitxer phpunit.xml en l'arrel del projecte per especificar la configuració de les proves:

```xml
<phpunit bootstrap="vendor/autoload.php">
    <testsuites>
        <testsuite name="Application Test Suite">
            <directory>tests</directory>
        </testsuite>
    </testsuites>
</phpunit>
```    
 
####  Estructura d’un test
Els tests en PHPUnit són classes PHP que hereten de PHPUnit\Framework\TestCase. Cada mètode dins d'aquestes classes que comence amb test serà executat com una prova.

``` php
use PHPUnit\Framework\TestCase;
use App\Models\Empleado;


class EmpleadoTest extends TestCase {
    private $empleado;

    protected function setUp(): void {
        $this->empleado = new Empleado('John', 'Doe', 4000, 30);
    }

    public function testGetSou() {
        $this->assertEquals(4000, $this->empleado->getSou());
    }

    public function testSetSou() {
        $this->empleado->setSou(4500);
        $this->assertEquals(4500, $this->empleado->getSou());
    }

    public function testGetTelefonos() {
        $this->assertIsArray($this->empleado->getTelefonos());
        $this->assertEmpty($this->empleado->getTelefonos());
    }

    public function testSetTelefono() {
        $this->empleado->setTelefono('123456789');
        $this->assertCount(1, $this->empleado->getTelefonos());
        $this->assertEquals('123456789', $this->empleado->getTelefonos()[0]);
    }

    public function testListarTelefonos() {
        $this->empleado->setTelefono('123456789');
        $this->empleado->setTelefono('987654321');
        $this->assertEquals('123456789, 987654321', $this->empleado->listarTelefonos());
    }

    public function testVaciarTelefonos() {
        $this->empleado->setTelefono('123456789');
        $this->empleado->vaciarTelefonos();
        $this->assertEmpty($this->empleado->getTelefonos());
    }

    public function testDebePagarImpuestos() {
        $this->assertTrue($this->empleado->debePagarImpuestos());
        $this->empleado->setSou(3000);
        $this->assertFalse($this->empleado->debePagarImpuestos());
    }
}


```

#### Execució de Proves
Per executar les proves, podem utilitzar la següent comanda:

vendor/bin/phpunit

Aquesta comanda cercarà els arxius de prova en el directori especificat (per defecte tests) i executarà totes les proves.


#### Tipus de  proves

Amb PHPUnit, podem realitzar diversos tipus de proves, entre elles:

* Proves Unitàries : Verifiquen el funcionament d'una unitat de codi individual, com una funció o mètode.
* Proves Funcionals: Verifiquen que un conjunt de mòduls funciona correctament conjuntament. Aquestes proves poden simular interaccions de l'usuari en un sistema web, encara que això es fa millor amb frameworks especialitzats per a proves funcionals.
* Proves d'Integració: Comproven que diferents mòduls o serveis funcionen correctament quan es combinen.


Exemple de prova unitària:
    
```php
public function testResta() {
    $calculadora = new Calculadora();
    $resultat = $calculadora->resta(5, 3);
    $this->assertEquals(2, $resultat);
}
```
 
#### Assercions

Les assercions permeten comprovar el resultat dels mètodes que volem provar. Les assercions esperen que el predicat sempre siga vertader.

PHPUnit ofereix les següent assercions:

* `assertTrue` / `assertFalse`: Comprova que la condició donada siga avaluada com true / false
* `assertEquals` / `assertSame`: Comprova que dues variables siguen iguals
* `assertNotEquals` / `assertNotSame`: Comprova que dues variables NO siguen iguals
* `assertNull`: Comprova que un valor és null.
* `Same` → comprova els tipus. Si no coincideixen els tipus i els valors, l'asserció fallarà
* `Equals` → sense comprovació estricta
* `assertArrayHasKey` / `assertArrayNotHasKey`: Comprova que un array posseïsca un *key* determinat / o NO ho posseïsca
* `assertArraySubset`: Comprova que un array posseïsca un altre array com subset del mateix
* `assertAttributeContains` / `assertAttributeNotContains`: Comprova que un atribut d'una classe continga una variable determinada / o NO continga una variable determinada
* `assertAttributeEquals`: Comprova que un atribut d'una classe siga igual a una variable determinada.

#### Proves amb dades

Les proves en PHPUnit poden utilitzar data providers per executar el mateix test amb diferents dades:

```php
/**
 * @dataProvider proveidorDeDades
 */
public function testMultiplica($a, $b, $esperat) {
    $calculadora = new Calculadora();
    $this->assertEquals($esperat, $calculadora->multiplica($a, $b));
}

public function proveidorDeDades() {
    return [
        [2, 3, 6],
        [0, 5, 0],
        [-1, 5, -5],
    ];
}

```

#### Mocks

Un mock és un objecte simulat que imita el comportament d'un objecte real en un entorn de proves. S'utilitza per simular la funcionalitat de certs components o dependències d'una classe, sense necessitat d'executar el codi real d'aquests components. Això permet provar una classe de manera aïllada i controlar el comportament de les seves dependències.

**Els mocks són útils quan:**

* No volem o no podem dependre del comportament real d'un component extern, com una connexió a una base de dades o una API.
* Necessitem verificar la interacció entre la classe provada i una dependència externa (per exemple, comprovar que un mètode s'ha cridat amb uns certs arguments).
* Volem millorar la velocitat i la fiabilitat de les proves en eliminar la dependència de sistemes externs.

**Com funciona un mock**

Quan utilitzem un mock, en lloc de cridar el mètode real d'una dependència, definim el comportament esperat manualment. També podem verificar que certs mètodes del mock s'hagin cridat, amb certs arguments, un nombre determinat de vegades, etc.

**Exemple senzill de mock amb PHPUnit**

Suposem que tenim una classe UserService que depèn d'una classe EmailService per enviar correus electrònics quan es crea un nou usuari. No volem enviar correus electrònics durant les proves, però sí que volem assegurar-nos que el mètode d'enviament de correus es crida quan es crea un usuari nou.

```php
<?php

class EmailService
{
    public function sendEmail($to, $subject, $message)
    {
        // Lògica per enviar un correu electrònic
    }
}

class UserService
{
    private $emailService;

    public function __construct(EmailService $emailService)
    {
        $this->emailService = $emailService;
    }

    public function createUser($user)
    {
        // Crear usuari...

        // Enviar un correu electrònic al nou usuari
        $this->emailService->sendEmail($user->email, 'Welcome!', 'Benvingut a la nostra plataforma!');
    }
}

```

```php
<?php

use PHPUnit\Framework\TestCase;

class UserServiceTest extends TestCase
{
    public function testCreateUserSendsEmail()
    {
        // Creem un mock de la classe EmailService
        $emailServiceMock = $this->createMock(EmailService::class);

        // Definim l'expectativa: esperem que el mètode sendEmail sigui cridat una vegada
        // amb els arguments concrets que especifiquem.
        $emailServiceMock->expects($this->once())
                         ->method('sendEmail')
                         ->with(
                             $this->equalTo('test@example.com'),
                             $this->equalTo('Welcome!'),
                             $this->stringContains('Benvingut a la nostra plataforma!')
                         );

        // Creem una instància de UserService passant el mock d'EmailService
        $userService = new UserService($emailServiceMock);

        // Simulem la creació d'un nou usuari
        $user = new stdClass();
        $user->email = 'test@example.com';
        $userService->createUser($user);

        // El mètode sendEmail del mock hauria de ser cridat una vegada amb els paràmetres especificats
    }
}

```


#### Provant excepcions

Les proves a més de comprovar que les classes funcionen com s'espera, han de cobrir tots els casos possibles. Així doncs, hem de poder fer proves que esperen que es llance una exempció (i que el missatge continga una certa informació):

Per a això, s'utilitzen les següent expectatives:

* `expectException(Excepcion::class)`
* `expectExceptionCode(codigoExcepcion)`
* `expectExceptionMessage(missatge)`

De la mateixa manera que abans, primer es posa l'expectativa, i després es provoca que es llance l'exempció:

``` php
<?php
public function testExcepcio() {
    $this->expectException(InvalidArgumentException::class);

    $calculadora = new Calculadora();
    $calculadora->divideix(5, 0);
}
```
#### Conclusió

Les proves són crucials per a assegurar que el nostre codi PHP és fiable i manté la seua funcionalitat al llarg del temps. Utilitzar PHPUnit ens proporciona les eines necessàries per a escriure proves eficaces i mantenir el nostre projecte en un estat saludable.


## 12. Referències Bibliogràfiques  

### Programació Orientada a Objectes en PHP

- **"PHP Objects, Patterns, and Practice"**  
  per M. Zandstra. Apress, 2017. ISBN: 978-1-4842-1361-3. Aquest llibre és un recurs essencial per entendre els fonaments de la programació orientada a objectes en PHP, així com patrons de disseny.

- **"Learning PHP, MySQL & JavaScript: With jQuery, CSS & HTML5"**  
  per Robin Nixon. O'Reilly Media, 2018. ISBN: 978-1-4919-2070-2. Ofereix una introducció completa a la programació amb PHP, incloent-hi el model d'objectes de PHP.

### Constructors i Destructors

- **PHP Manual: Constructors and Destructors**  
  Documentació oficial de PHP sobre constructors i destructors en la programació orientada a objectes. Disponible a [https://www.php.net/manual/en/language.oop5.decon.php](https://www.php.net/manual/en/language.oop5.decon.php).

### Encapsulació i Visibilitat

- **PHP Manual: Visibility**  
  Secció del manual oficial de PHP que explica les paraules clau `public`, `protected`, i `private`, així com el concepte d'encapsulació. Accessible a [https://www.php.net/manual/en/language.oop5.visibility.php](https://www.php.net/manual/en/language.oop5.visibility.php).

### Herència i Polimorfisme

- **"Programming PHP"**  
  per Kevin Tatroe, Peter MacIntyre, i Rasmus Lerdorf. O'Reilly Media, 2013. ISBN: 978-1-4493-5053-6. Aquest llibre cobreix àmpliament els conceptes d'herència i polimorfisme en PHP, proporcionant exemples pràctics.

- **PHP Manual: Inheritance**  
  Documentació oficial de PHP que tracta sobre l'herència en classes, incloent el polimorfisme. Disponible a [https://www.php.net/manual/en/language.oop5.inheritance.php](https://www.php.net/manual/en/language.oop5.inheritance.php).

### Classes Abstractes i Interfícies

- **PHP Manual: Interfaces and Abstract Classes**  
  Explicació oficial de les classes abstractes i les interfícies en PHP. Disponible a [https://www.php.net/manual/en/language.oop5.interfaces.php](https://www.php.net/manual/en/language.oop5.interfaces.php).

### Nombres màgics i Metodes màgics

- **PHP Manual: Magic Methods**  
  Guia completa sobre els mètodes màgics en PHP, com `__construct()`, `__destruct()`, `__get()`, `__set()`, entre altres. Disponible a [https://www.php.net/manual/en/language.oop5.magic.php](https://www.php.net/manual/en/language.oop5.magic.php).

### Trait en PHP

- **PHP Manual: Traits**  
  Documentació sobre traits en PHP, que permeten reutilitzar codi entre diferents classes. Disponible a [https://www.php.net/manual/en/language.oop5.traits.php](https://www.php.net/manual/en/language.oop5.traits.php).

### Excepcions en PHP

- **"The Pragmatic Programmer: Your Journey to Mastery"**  
  per David Thomas i Andrew Hunt. Addison-Wesley Professional, 2019. ISBN: 978-0-1359-5202-8. Inclou bones pràctiques per a la gestió d'excepcions, aplicables també a PHP.

- **PHP Manual: Exceptions**  
  Secció del manual de PHP dedicada a les excepcions, explicant com llençar i capturar excepcions en PHP. Accessible a [https://www.php.net/manual/en/language.exceptions.php](https://www.php.net/manual/en/language.exceptions.php).

### Proves amb PHPUnit

- **"Modern PHP: New Features and Good Practices"**  
  per Josh Lockhart. O'Reilly Media, 2015. ISBN: 978-1-4919-2904-0. Aquest llibre inclou una secció sobre proves amb PHPUnit.

- **PHPUnit Documentation**  
  Documentació oficial de PHPUnit, que cobreix com escriure i executar proves unitàries en PHP. Accessible a [https://phpunit.de/documentation.html](https://phpunit.de/documentation.html).

### Eines de Desenvolupament i Autocàrrega

- **Composer Documentation**  
  Accessible des de [https://getcomposer.org/doc/](https://getcomposer.org/doc/). Composer és l'eina estàndard per a la gestió de dependències en PHP, i inclou suport per a l'autocàrrega de classes.

- **PHP Manual: Autoloading Classes**  
  Guia sobre el mecanisme d'autocàrrega en PHP, que facilita la inclusió automàtica de classes en els teus projectes. Disponible a [https://www.php.net/manual/en/language.oop5.autoload.php](https://www.php.net/manual/en/language.oop5.autoload.php).

### POO Avançada: Patrons de Disseny

- **"Head First Design Patterns"**  
  per Eric Freeman i Elisabeth Robson. O'Reilly Media, 2020. ISBN: 978-1-4919-7175-9. Un recurs excel·lent per aprendre patrons de disseny aplicables a PHP.

- **"PHP Design Patterns"**  
  per Stephan Schmidt. Publicat per Packt Publishing, 2008. ISBN: 978-1-84719-255-3. Aquest llibre explora com aplicar patrons de disseny en projectes PHP.

### Webs de Referència Addicionals

- **PHP: The Right Way**  
  [https://phptherightway.com/](https://phptherightway.com/). Una guia per a desenvolupar aplicacions PHP seguint les millors pràctiques de la indústria.

- **Stack Overflow**  
  [https://stackoverflow.com/questions/tagged/php](https://stackoverflow.com/questions/tagged/php). Una font d'informació valuosa per resoldre problemes específics de PHP i discutir amb altres desenvolupadors.

---


## 13. Exercicis

### Bateria d'Exercicis Solucionats per a la Unitat de Programació Orientada a Objectes

##### Exercici 1: Crear una Classe Bàsica

1. Crea una classe `Cotxe` que tinga les propietats `marca` i `model`. Afegeix un mètode `mostraInformacio` que retorne un string amb la marca i el model del cotxe.
2. Crea una instància de la classe `Cotxe`, assigna-li una marca i un model, i mostra la informació utilitzant el mètode `mostraInformacio`.

<details>
<summary>Solució</summary>

```php
<?php
class Cotxe {
    public $marca;
    public $model;

    public function mostraInformacio() {
        return "Marca: " . $this->marca . ", Model: " . $this->model;
    }
}
 
$cotxe = new Cotxe();
$cotxe->marca = "Toyota";
$cotxe->model = "Corolla";
echo $cotxe->mostraInformacio(); // Output: Marca: Toyota, Model: Corolla
``` 
</details>
 
##### Exercici 2. Afegir un Constructor i destructor

1. Modifica la classe `Cotxe` per afegir un constructor que prenga com a paràmetres la `marca` i el `model`, i que establisca aquestes propietats automàticament.
2. Afegeix un destructor a la classe `Cotxe` que mostre un missatge quan l'objecte és destruït. Crea un objecte i permet que es destruïsca al final del programa.

<details>
<summary>Solució</summary>

```php
<?php
class Cotxe {
    public $marca;
    public $model;

    public function __construct($marca, $model) {
        $this->marca = $marca;
        $this->model = $model;
    }
    public function __destruct() {
        echo "L'objecte Cotxe ha estat destruït.\n";
    }

    public function mostraInformacio() {
        return "Marca: " . $this->marca . ", Model: " . $this->model;
    }
}
```
</details>

##### Exercici 3. Encapsulació de Propietats
 
1. Modifica la classe `Cotxe` per a que les propietats `marca` i `model` siguen privades. Afegeix mètodes públics `getMarca`, `setMarca`, `getModel`, i `setModel` per accedir i modificar aquestes propietats.

<details>
<summary>Solució</summary>

```php
<?php
class Cotxe {
    private $marca;
    private $model;

    public function __construct($marca, $model) {
        $this->marca = $marca;
        $this->model = $model;
    }

    public function getMarca() {
        return $this->marca;
    }

    public function setMarca($marca) {
        $this->marca = $marca;
    }

    public function getModel() {
        return $this->model;
    }

    public function setModel($model) {
        $this->model = $model;
    }

    public function mostraInformacio() {
        return "Marca: " . $this->getMarca() . ", Model: " . $this->getModel();
    }
}

$cotxe = new Cotxe("Ford", "Fiesta");
echo $cotxe->mostraInformacio(); // Output: Marca: Ford, Model: Fiesta
```
</details>
 
##### Exercici 4. Herència i Polimorfisme
 
1. Crea una classe `Vehicle` amb una propietat `tipus`. A continuació, crea una classe `Motocicleta` que herete de `Vehicle` i tinga una propietat `cilindrada`. Afegeix un mètode a `Motocicleta` que retorne el tipus i la cilindrada.
2. Crea una funció `mostraDetallsVehicle` que accepte un objecte de tipus `Vehicle` i mostre les seues propietats. Prova aquesta funció amb objectes de `Cotxe` i `Motocicleta`.

<details>
<summary>Solució</summary>

```php
<?php
class Vehicle {
    protected $tipus;

    public function __construct($tipus) {
        $this->tipus = $tipus;
    }

    public function mostraDetalls() {
        return "Tipus: " . $this->tipus;
    }
}

class Cotxe extends Vehicle {
    private $marca;
    private $model;

    public function __construct($marca, $model) {
        parent::__construct("Cotxe");
        $this->marca = $marca;
        $this->model = $model;
    }

    public function mostraDetalls() {
        return parent::mostraDetalls() . ", Marca: " . $this->marca . ", Model: " . $this->model;
    }
}

class Motocicleta extends Vehicle {
    private $cilindrada;

    public function __construct($cilindrada) {
        parent::__construct("Motocicleta");
        $this->cilindrada = $cilindrada;
    }

    public function mostraDetalls() {
        return parent::mostraDetalls() . ", Cilindrada: " . $this->cilindrada;
    }
}

function mostraDetallsVehicle(Vehicle $vehicle) {
    echo $vehicle->mostraDetalls() . "\n";
}

$cotxe = new Cotxe("Toyota", "Corolla");
$moto = new Motocicleta(600);

mostraDetallsVehicle($cotxe); // Output: Tipus: Cotxe, Marca: Toyota, Model: Corolla
mostraDetallsVehicle($moto);  // Output: Tipus: Motocicleta, Cilindrada: 600
```
</details>

##### Exercici 5. Implementació del Patró MVC amb Vehicles
 
Continuant amb l'exercici anterior on has creat les classes `Vehicle`, `Cotxe`, i `Motocicleta`, ara refactoritzaràs el codi per seguir el patró Model-Vista-Controlador (MVC). El teu objectiu és separar la lògica de negoci (models) de la presentació (vistes) i gestionar la interacció entre aquestes capes mitjançant un controlador.
   
1.  **Crear el Model**:
    - Refactoritza les classes `Vehicle`, `Cotxe`, i `Motocicleta` perquè representen el model de negoci i només contenen la lògica relacionada amb la gestió de vehicles.
    - Assegura't que els models no contenen cap codi de presentació.

2. **Crear les Vistes**:
    - Crea vistes separades per mostrar els detalls dels vehicles:
        - Una vista HTML que mostre la informació dels vehicles en format HTML.
        - Una vista en text simple que mostre els detalls dels vehicles en un format de text senzill.

3. **Crear el Controlador**:
    - Implementa un controlador que gestione la interacció entre els models i les vistes.
    - El controlador ha de ser capaç de rebre una sol·licitud per mostrar un vehicle i triar la vista adequada per mostrar-ne els detalls.

<details>
<summary>Solució</summary>

```php
<?php
// Models

class Vehicle {
    protected $tipus;

    public function __construct($tipus) {
        $this->tipus = $tipus;
    }

    public function getTipus() {
        return $this->tipus;
    }
}

class Cotxe extends Vehicle {
    private $marca;
    private $model;

    public function __construct($marca, $model) {
        parent::__construct("Cotxe");
        $this->marca = $marca;
        $this->model = $model;
    }

    public function getMarca() {
        return $this->marca;
    }

    public function getModel() {
        return $this->model;
    }
}

class Motocicleta extends Vehicle {
    private $cilindrada;

    public function __construct($cilindrada) {
        parent::__construct("Motocicleta");
        $this->cilindrada = $cilindrada;
    }

    public function getCilindrada() {
        return $this->cilindrada;
    }
}

// Vistes

class VehicleView {
    public function renderHtml(Vehicle $vehicle) {
        $output = "<p>Tipus: " . $vehicle->getTipus() . "</p>";
        if ($vehicle instanceof Cotxe) {
            $output .= "<p>Marca: " . $vehicle->getMarca() . "</p>";
            $output .= "<p>Model: " . $vehicle->getModel() . "</p>";
        } elseif ($vehicle instanceof Motocicleta) {
            $output .= "<p>Cilindrada: " . $vehicle->getCilindrada() . " cc</p>";
        }
        return $output;
    }

    public function renderText(Vehicle $vehicle) {
        $output = "Tipus: " . $vehicle->getTipus() . "\n";
        if ($vehicle instanceof Cotxe) {
            $output .= "Marca: " . $vehicle->getMarca() . "\n";
            $output .= "Model: " . $vehicle->getModel() . "\n";
        } elseif ($vehicle instanceof Motocicleta) {
            $output .= "Cilindrada: " . $vehicle->getCilindrada() . " cc\n";
        }
        return $output;
    }
}

// Controlador

class VehicleController {
    private $view;

    public function __construct(VehicleView $view) {
        $this->view = $view;
    }

    public function mostrarVehicle(Vehicle $vehicle, $format = 'html') {
        if ($format === 'html') {
            echo $this->view->renderHtml($vehicle);
        } else {
            echo $this->view->renderText($vehicle);
        }
    }
}

// Exemple d'ús

$view = new VehicleView();
$controller = new VehicleController($view);

$cotxe = new Cotxe("Toyota", "Corolla");
$moto = new Motocicleta(600);

// Mostrar en HTML
$controller->mostrarVehicle($cotxe, 'html');
$controller->mostrarVehicle($moto, 'html');

// Mostrar en Text
$controller->mostrarVehicle($cotxe, 'text');
$controller->mostrarVehicle($moto, 'text');
```
</details>

#### Exercici 5. Classes Abstractes i Interfícies
 
1. Crea una classe abstracta `Figura` amb un mètode abstracte `calculaArea`. Després, crea classes `Cercle` i `Rectangle` que estiguen basades en `Figura` i implementen el mètode `calculaArea`.
2. Defineix una interfície `OperacionsBàsiques` amb els mètodes `suma` i `resta`. Implementa aquesta interfície en una classe `CalculadoraSimple`.

<details>
<summary>Solució</summary>

```php
<?php
abstract class Figura {
    abstract public function calculaArea();
}

class Cercle extends Figura {
    private $radi;

    public function __construct($radi) {
        $this->radi = $radi;
    }

    public function calculaArea() {
        return pi() * $this->radi * $this->radi;
    }
}

class Rectangle extends Figura {
    private $ample;
    private $llarg;

    public function __construct($ample, $llarg) {
        $this->ample = $ample;
        $this->llarg = $llarg;
    }

    public function calculaArea() {
        return $this->ample * $this->llarg;
    }
}

$cercle = new Cercle(5);
$rectangle = new Rectangle(4, 6);

echo "Àrea del cercle: " . $cercle->calculaArea() . "\n"; // Output: Àrea del cercle: 78.5398
echo "Àrea del rectangle: " . $rectangle->calculaArea() . "\n"; // Output: Àrea del rectangle: 24

``` 

```php
<?php
interface OperacionsBàsiques {
    public function suma($a, $b);
    public function resta($a, $b);
}

class CalculadoraSimple implements OperacionsBàsiques {
    public function suma($a, $b) {
        return $a + $b;
    }

    public function resta($a, $b) {
        return $a - $b;
    }
}

$calculadora = new CalculadoraSimple();
echo "Suma: " . $calculadora->suma(5, 3) . "\n"; // Output: Suma: 8
echo "Resta: " . $calculadora->resta(5, 3) . "\n"; // Output: Resta: 2
```
</details>

#### Exercici 6.  Utilitzar Traits

1. Crea un trait `Informacio` amb un mètode `mostraInformacio`. Inclou aquest trait en les classes `Cotxe` i `Motocicleta`, i utilitza'l per mostrar informació addicional.

<details>
<summary>Solució</summary>

```php
<?php
trait Informacio {
    public function mostraInformacio() {
        return "Aquest és un objecte de tipus " . get_class($this);
    }
}

class Cotxe {
    use Informacio;
}

class Motocicleta {
    use Informacio;
}

$cotxe = new Cotxe();
$moto = new Motocicleta();

echo $cotxe->mostraInformacio() . "\n"; // Output: Aquest és un objecte de tipus Cotxe
echo $moto->mostraInformacio() . "\n"; // Output: Aquest és un objecte de tipus Motocicleta
```
</details>

#### Exercici 7.  Gestionar Excepcions

1. Escriu una funció `divideix` que prenga dos nombres com a paràmetres i retorne el resultat de la divisió. Si el segon nombre és zero, llença una excepció amb un missatge adequat. Captura aquesta excepció quan crides a la funció i mostra un missatge d'error.

<details>
<summary>Solució</summary>

```php
<?php
function divideix($a, $b) {
    if ($b == 0) {
        throw new Exception("No es pot dividir per zero.");
    }
    return $a / $b;
}

try {
    echo divideix(10, 2) . "\n"; // Output: 5
    echo divideix(10, 0) . "\n"; // Aquesta línia llançarà una excepció
} catch (Exception $e) {
    echo "Error: " . $e->getMessage() . "\n"; // Output: Error: No es pot dividir per zero.
}
```
</details>

#### Exercici 8. Proves amb PHPUnit
 
1. Crea una classe `Calculadora` amb els mètodes `suma` i `resta`. Escriu una prova unitària amb PHPUnit per verificar que aquests mètodes funcionen correctament.
2. Afegeix un mètode `divideix` a la classe `Calculadora` que llance una excepció quan es divideix per zero. Escriu una prova unitària que assegure que aquesta excepció es llança correctament.

<details>
<summary>Solució</summary>

```php
<?php
// Arxiu: tests/CalculadoraTest.php
use PHPUnit\Framework\TestCase;

class Calculadora {
    public function suma($a, $b) {
        return $a + $b;
    }

    public function resta($a, $b) {
        return $a - $b;
    }
}

class CalculadoraTest extends TestCase {
    public function testSuma() {
        $calculadora = new Calculadora();
        $resultat = $calculadora->suma(2, 3);
        $this->assertEquals(5, $resultat);
    }

    public function testResta() {
        $calculadora = new Calculadora();
        $resultat = $calculadora->resta(5, 3);
        $this->assertEquals(2, $resultat);
    }
}
``` 
```php
 
// Arxiu: tests/CalculadoraTest.php
use PHPUnit\Framework\TestCase;

class Calculadora {
    public function divideix($a, $b) {
        if ($b == 0) {
            throw new InvalidArgumentException("No es pot dividir per zero.");
        }
        return $a / $b;
    }
}

class CalculadoraTest extends TestCase {
    public function testDivideix() {
        $this->expectException(InvalidArgumentException::class);
        
        $calculadora = new Calculadora();
        $calculadora->divideix(5, 0);
    }
}
```
</details>

#### Exercici 9. Espais de Noms (Namespaces)

1. Crea un espai de noms `App\Models` i defineix una classe `Usuari` dins d'aquest espai de noms. Afegeix un mètode `getNomComplet` que retorne el nom complet de l'usuari.
2. En un fitxer separat, importa la classe `Usuari` de l'espai de noms `App\Models` i crea una instància d'aquesta classe. Utilitza el mètode `getNomComplet` per mostrar el nom complet d'un usuari.

<details>
<summary>Solució</summary>

```php
<?php
// Arxiu: src/Models/Usuari.php
namespace App\Models;

class Usuari {
    private $nom;
    private $cognom;

    public function __construct($nom, $cognom) {
        $this->nom = $nom;
        $this->cognom = $cognom;
    }

    public function getNomComplet() {
        return $this->nom . " " . $this->cognom;
    }
}
``` 
```php

// Arxiu: index.php
require 'vendor/autoload.php';

use App\Models\Usuari;

$usuari = new Usuari("Joan", "Garcia");
echo $usuari->getNomComplet(); // Output: Joan Garcia
```
</details>

#### Exercici 10. Autoloading i Composer

1. Configura un projecte PHP amb Composer que utilitze l'autoloading PSR-4. Crea l'estructura de directoris `src/Models` i col·loca una classe `Producte` dins de `src/Models`. Verifica que l'autoloading funcione correctament instanciant la classe `Producte` en un fitxer separat.
2. Afegeix la llibreria `monolog/monolog` al projecte utilitzant Composer. Crea una instància de `Logger` i afegeix una entrada al registre de logs.

<details>
<summary>Solució</summary>

1. Crea l'estructura de directoris src/Models i col·loca el següent codi a src/Models/Producte.php:

```php
<?php
namespace App\Models;

class Producte {
    private $nom;

    public function __construct($nom) {
        $this->nom = $nom;
    }

    public function getNom() {
        return $this->nom;
    }
}
```

2. Configura l'autoloading en composer.json:

```json
{
    "autoload": {
        "psr-4": {
            "App\\": "src/"
        }
    }
}
```

3. Executa composer dump-autoload per generar els fitxers d'autoload.
4. Utilitza la classe producte:

```php
<?php
// Arxiu: index.php
require 'vendor/autoload.php';

use App\Models\Producte;

$producte = new Producte("Ordinador");
echo $producte->getNom(); // Output: Ordinador
```
5. Afegeix Monolog a composer.json:

```bash
composer require monolog/monolog
```
6. Utilitza Monolog per crear un logger:

```php
<?php
require 'vendor/autoload.php';

use Monolog\Logger;
use Monolog\Handler\StreamHandler;

$log = new Logger('nom_aplicacio');
$log->pushHandler(new StreamHandler('app.log', Logger::WARNING));

// Afegeix una entrada al log
$log->warning('Aquesta és una entrada d'advertència');
$log->error('Aquesta és una entrada d'error');

```
</details>
 
#### Exercici 11. Logger

1. Utilitzant la llibreria `Monolog`, crea un logger que escriga missatges a un fitxer `app.log`. Configura el logger per registrar missatges d'informació i d'error.
2. Configura un logger que escriga missatges de registre tant a un fitxer com a la consola. Prova el logger registrant missatges d'error.

<details>
<summary>Solució</summary>

```php
<?php
require 'vendor/autoload.php';

use Monolog\Logger;
use Monolog\Handler\StreamHandler;

$log = new Logger('nom_aplicacio');
$log->pushHandler(new StreamHandler('app.log', Logger::INFO));
$log->pushHandler(new StreamHandler('app.log', Logger::ERROR));

// Registra missatges d'informació i d'error
$log->info('Aquesta és una entrada d’informació');
$log->error('Aquesta és una entrada d’error');

```

```php
<?php
require 'vendor/autoload.php';

use Monolog\Logger;
use Monolog\Handler\StreamHandler;
use Monolog\Handler\ErrorLogHandler;

$log = new Logger('nom_aplicacio');
$log->pushHandler(new StreamHandler('app.log', Logger::WARNING));
$log->pushHandler(new ErrorLogHandler());

// Registra missatges d’error al fitxer i a la consola
$log->error('Aquesta és una entrada d’error');

```

</details>

#### Exercici 12. Documentació

1. Documenta la classe `Producte` creada en l'exercici anterior utilitzant comentaris PHPDoc. Assegura't d'incloure la descripció de la classe, les propietats, i els mètodes.
2. Utilitza una eina com `phpDocumentor` per generar la documentació automàtica del codi PHP del projecte, incloent-hi la classe `Producte`.

<details>
<summary>Solució</summary>

```php
<?php
namespace App\Models;

/**
 * Classe Producte
 *
 * Representa un producte amb un nom.
 */
class Producte {
    /**
     * @var string El nom del producte
     */
    private $nom;

    /**
     * Constructor de la classe Producte
     *
     * @param string $nom El nom del producte
     */
    public function __construct($nom) {
        $this->nom = $nom;
    }

    /**
     * Obté el nom del producte
     *
     * @return string El nom del producte
     */
    public function getNom() {
        return $this->nom;
    }
}
```

1. Instal·la phpDocumentor globalment o com a dependència de desenvolupament:

```bash
composer require --dev phpdocumentor/phpdocumentor
```

2. Genera la documentació:

```bash
vendor/bin/phpdoc -d src -t docs
```

Aquest comandament generarà la documentació a la carpeta docs.
 
</details>

#### Exercici 13. Generació de PDFs amb DomPDF

1. Instal·la la llibreria `dompdf/dompdf` amb Composer. Crea un script PHP que genere un PDF senzill amb un títol i un paràgraf de text.
2. Crea un PDF utilitzant DomPDF que incloga una taula amb dades i una imatge. Assegura't que el PDF es renderitze correctament i que la imatge s'incloga en el document.

<details>
<summary>Solució</summary>

1. Instal·la DomPDF amb Composer:

```bash
composer require dompdf/dompdf
```

2. Crea un script PHP que generi un PDF senzill:

```php
<?php
require 'vendor/autoload.php';

use Dompdf\Dompdf;

$dompdf = new Dompdf();
$html = '<h1>Informe de Vendes</h1><p>Aquest és un informe de les vendes.</p>';

$dompdf->loadHtml($html);
$dompdf->setPaper('A4', 'landscape');
$dompdf->render();
$dompdf->stream('informe.pdf');
```

3. Crea un PDF amb una taula i una imatge:

```php
<?php
require 'vendor/autoload.php';

use Dompdf\Dompdf;

$dompdf = new Dompdf();
$html = '
    <h1>Informe de Productes</h1>
    <table border="1" cellpadding="10">
        <thead>
            <tr>
                <th>Producte</th>
                <th>Preu</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>Ordinador</td>
                <td>500€</td>
            </tr>
            <tr>
                <td>Teclat</td>
                <td>20€</td>
            </tr>
        </tbody>
    </table>
    <img src="https://example.com/imatge.png" alt="Imatge de Producte" />
';

$dompdf->loadHtml($html);
$dompdf->setPaper('A4', 'portrait');
$dompdf->render();
$dompdf->stream("informe_productes.pdf");
```

</details>


##  Exercicis proposats
 
#### Exercici 1. Creació de la Classe Bàsica i Gestió de Propietats

* Crea una classe `Persona` amb les propietats privades `nom`, `cognoms`, i `edat`. Encapsula aquestes propietats mitjançant getters i setters. Afig els següents mètodes:

      - `getNomComplet(): string` – Retorna el nom complet de la persona.
      - `estaJubilat(): bool` – Retorna `true` si l'edat és major o igual a 65, `false` en cas contrari.

* Modifica la classe `Persona` afegint un constructor que assigna nom i cognoms. Si es proporciona un tercer paràmetre, assigna l'edat; en cas contrari, assigna una edat per defecte de 25 anys.

* Modifica la classe `Persona` per utilitzar una constant `LIMITE_EDAT` amb el valor de 66 anys i utilitza-la en el mètode `estaJubilat`.

#### Exercici 2. Herència i Polimorfisme

* Crea una classe `Empleado` que herete de `Persona`. Afig les següents propietats i mètodes:

    - `private float $sou`
    - `private array $telefons`
    - `anyadirTelefono(int $telefon): void` – Afig un número de telèfon a l'array.
    - `listarTelefonos(): string` – Retorna els números de telèfon separats per comes.
    - `vaciarTelefonos(): void` – Buida l'array de telèfons.
    - `debePagarImpuestos(): bool` – Retorna `true` si el sou és superior a 3333€, `false` en cas contrari.

* Afig un mètode estàtic `toHtml(Empleado $emp): string` que genere un codi HTML que mostre el nom complet de l'empleat dins d'un paràgraf i els seus telèfons dins d'una llista ordenada.
* Afig un mètode estàtic `toHtml(Persona $p)` a la classe Persona que mostre el nom complet de la persona dins d'un paràgraf. Modifica el mètode `toHtml` de `Empleado` per rebre una `Persona` com a paràmetre i comprovar si es tracta d'un `Empleado` amb `instanceof`.
* Transforma `Persona` en una classe abstracta. Redefineix el mètode estàtic `toHtml(Persona $p)` en totes les seues subclasses. 
 
#### Exercici 3. Integració d'Espais de Noms, Autoloading, i Composer

* Crea una classe `Empresa` que incloga una propietat amb un array de `Empleados` . Implementa:

    - `public function addWorker(Empleado $t)`
    - `public function listWorkersHtml(): string` – Genera la llista de treballadors en format HTML.
    - `public function getCosteNominas(): float` – Calcula el cost total de les nòmines.

* Configura el projecte PHP amb Composer que utilitze l'autoloading PSR-4.  

#### Exercici 4. Logger i Documentació

* Utilitza la llibreria `Monolog` per configurar un logger que escriga missatges a un fitxer `app.log`. Afig funcionalitat perquè el logger registre missatges d'informació i d'error en diferents arxius segons la gravetat.

* Configura un logger que escriga missatges de registre tant a un fitxer com a la consola. Prova el logger registrant missatges d'error i advertència.

* Documenta la classe `Empleado` creada en exercicis anteriors utilitzant comentaris PHPDoc. Inclou la descripció de la classe, les propietats, i els mètodes. Utilitza una eina com `phpDocumentor` per generar documentació automàtica.

* Escriu proves unitàries per als mètodes de les classes `Persona`, `Empleado`, i `Empresa` utilitzant PHPUnit. Prova els mètodes `getNomComplet`, `estaJubilat`, `addWorker`, i `getCosteNominas`. Assegura't que les proves cobreixen diferents escenaris, incloent errors potencials.

* Escriu una prova unitària que comprove que el logger està registrant correctament els missatges d'error a l'arxiu corresponent. Utilitza un mock per assegurar-te que el logger funciona sense necessitat d'escriure en un fitxer real durant la prova.

#### Exercici 5. Generació de PDFs amb DomPDF

* Instal·la la llibreria `dompdf/dompdf` amb Composer. Crea un script PHP que genere un PDF senzill amb un títol i un paràgraf de text.

* Crea un PDF utilitzant DomPDF que incloga una taula amb dades i una imatge. Assegura't que el PDF es renderitze correctament i que la imatge s'incloga en el document.

* Utilitzant la classe `Empresa` i `Empleado`, genera un informe en PDF amb la llista de treballadors i el seu sou. Utilitza DomPDF per generar aquest informe.

#### Exercici 6. Serialització i JSON

* Crea una interfície `JSerializable` que incloga els mètodes:

    - `toJSON(): string` – Converteix l'objecte a un JSON utilitzant `json_encode()`.
    - `toSerialize(): string` – Serialitza l'objecte utilitzant `serialize()`.

* Modifica les classes `Persona`, `Empleado`, i `Empresa` per implementar aquesta interfície. Assegura't que les propietats privades es puguen serialitzar correctament.

* Escriu mètodes per deserialitzar un objecte a partir d'una cadena JSON o d'una cadena serialitzada. Prova aquests mètodes amb PHPUnit per assegurar-te que la deserialització funciona correctament.

#### Exercici 7. Separació del Model de Negoci i la Presentació (MVC)
 
Fins ara, has creat diverses classes que gestionen la lògica del joc i les dades (models), com `Persona`, `Empleado`, i `Empresa`, i has generat sortides HTML i PDFs amb DomPDF. Ara és el moment de refactoritzar la teua aplicació per assegurar una separació clara entre la lògica del negoci i la presentació, seguint el patró Model-Vista-Controlador (MVC).
  
* **Crear el Model**:
    - Refactoritza les classes `Persona`, `Empleado`, i `Empresa` per assegurar que només gestionen la lògica de negoci (per exemple, càlcul de nòmines, gestió d'empleats, etc.).
    - Assegura't que aquestes classes no contenen codi relacionat amb la presentació (HTML o PDF).

* **Crear les Vistes**:
    - Crea vistes separades per presentar la informació als usuaris:
        - Una vista HTML per mostrar la informació de `Empleado` i `Empresa` com a llistats.
        - Una vista PDF per generar informes amb DomPDF, basant-se en les dades proporcionades pel model.

* **Crear el Controlador**:
    - Implementa un controlador que reba les sol·licituds dels usuaris, interactue amb el model (`Persona`, `Empleado`, `Empresa`), i tria la vista adequada per mostrar els resultats (HTML o PDF).
    - El controlador ha d'encapsular tota la lògica necessària per a gestionar la interacció entre la vista i el model, assegurant que el model no estiga lligat a la capa de presentació.



#### Exercici 8. Creació de Proves Unitàries per al Patró MVC

Després de refactoritzar l'aplicació per separar la lògica del negoci de la presentació seguint el patró Model-Vista-Controlador (MVC), és fonamental assegurar-se que tots els components funcionen correctament i que la interacció entre ells es realitza tal com s'espera. Per això, has de crear una sèrie de proves unitàries utilitzant PHPUnit per verificar el funcionament del model, les vistes i els controladors.
  
* **Proves del Model**:
    - Escriu proves unitàries per verificar el funcionament dels mètodes de les classes `Persona`, `Empleado`, i `Empresa`.
    - Assegura't que els mètodes funcionen correctament, com ara:
        - `getNomComplet()`
        - `debePagarImpuestos()`
        - `addWorker()` i `getCosteNominas()`
    - Prova que els càlculs es realitzen correctament i que les dades es gestionen segons el que s'espera.

* **Proves del Controlador**:
    - Escriu proves unitàries per assegurar-te que els controladors interactuen correctament amb els models i que seleccionen la vista adequada per a cada situació.
    - Prova que les dades es passen correctament del model a la vista a través del controlador.
    - Implementa proves per verificar que el controlador respon correctament a diferents sol·licituds de l'usuari, per exemple:
        - Mostrar una llista d'empleats en HTML.
        - Generar un informe en PDF utilitzant DomPDF.



* **Proves de les Vistes**:
    - Escriu proves unitàries per comprovar que les vistes reben i mostren correctament la informació proporcionada pel controlador.
    - Prova que la generació de contingut HTML o PDF es realitza correctament a partir de les dades proporcionades pel model.
 
## 14. Enunciat dels projectes
   
### Projecte "4 en Ratlla"

#### 1. Crear l'entorn del 4 en ratlla

- Dins de php crear les carpetes App,Views i Helpers.
- Dins de la carpeta App crea les carpetes Models, Controllers , Services i Exceptions. 
 - Dins de la carpeta src tindrem el index.php i el css.



#### 2. Integració de Composer i Autoloading
- **Configuració de Composer**: Defineix un `composer.json` per al projecte, configurant l'autoloading PSR-4 per carregar automàticament les classes de `Joc4enRatlla`.
- **Estructura del Projecte**:
    - Organitza el codi en directoris com `App/Models` per a les classes del joc i `App/Controllers` per a la gestió del flux del joc.
    - Configura Composer per gestionar les dependències del projecte.


#### 3. Refactorització amb Programació Orientada a Objectes (POO) i amb MVC 

##### Models

- Dins de la carpeta Models:
 
  - **Classe `Board`**: Crea una classe `Board` per representar la graella del joc. Aquesta classe ha de gestionar la configuració inicial de la graella, els moviments dels jugadors, i la comprovació de si hi ha un guanyador.

```php
  
namespace Joc4enRatlla\Models;
 
class Board
{
    public const FILES = 6;
    public const COLUMNS = 7;
    public const DIRECTIONS = [
        [0, 1],   // Horizontal derecha
        [1, 0],   // Vertical abajo
        [1, 1],   // Diagonal abajo-derecha
        [1, -1]   // Diagonal abajo-izquierda
    ];

    private array $slots; // graella

    public function __construct(){
      // TODO: Ha d'inicializar $slots
    }
    
    // TODO: Getters i Setters 
    
    private static function initializeBoard(): array{
        // TODO: Inicialitza la graella amb valors buits
    }
    public function setMovementOnBoard(int $column, int $player): array {
        // TODO: Realitza un moviment en la graella
    }
    public function checkWin(array $coord): bool {
        // TODO: Comprova si hi ha un guanyador
    }
    public function isValidMove(int $column): bool {
        // TODO: Comprova si el moviment és vàlid
    }
    
    public function isFull(): bool {
        // TODO: El tauler està ple?
    }
     


}
```

  - **Classe  `Jugador`**: Crea una classe `Player` per representar els jugadors del joc, amb propietats com el `name`, el `color` de les fitxes, forma de jugar `isAutomatic`.

```php
namespace Joc4enRatlla\Models;

 
class Player {
    private $name;      // Nom del jugador
    private $color;     // Color de les fitxes
    private $isAutomatic; // Forma de jugar (automàtica/manual)
 
    public function __construct( $name, $color, $isAutomatic = false) {
        // TODO: Inicialitzar variables 
    }

    // TODO: Getters i Setters 
 
}

```
 
  - **Classe `Game`**: Refactoritza la lògica del joc en una classe `Game` que gestione la graella, el torn del jugador, i la lògica per determinar el guanyador, la puntuació.
   
```php

namespace Joc4enRatlla\Models;

use Joc4enRatlla\Models\Board;
use Joc4enRatlla\Models\Player;

class Game
{
    private Board $board;
    private int $nextPlayer;
    private array $players;
    private ?Player $winner;
    private array $scores = [1 => 0, 2 => 0];
    
    public function __construct( Player $jugador1, Player $jugador2){
        // TODO: S'han d'inicialitzar les variables tenint en compte que el array de jugador ha de començar amb l'index 1 
    }
     
    // TODO: getters i setters
       
    public function reset(): void{
        // TODO: Reinicia el joc
    }
    public function play($columna){
        // TODO: Realitza un moviment
    }
    /**
    * Realitza moviment automàtic
    * @return void
    */                                          
    public function playAutomatic(){
        $opponent = $this->nextPlayer === 1 ? 2 : 1;

        for ($col = 1; $col <= Board::COLUMNS; $col++) {
            if ($this->board->isValidMove($col)) {
                $tempBoard = clone($this->board);
                $coord = $tempBoard->setMovementOnBoard($col, $this->nextPlayer);

                if ($tempBoard->checkWin($coord)) {
                    $this->play($col);
                    return;
                }
            }
        }

        for ($col = 1; $col <= Board::COLUMNS; $col++) {
            if ($this->board->isValidMove($col)) {
                $tempBoard = clone($this->board);
                $coord = $tempBoard->setMovementOnBoard($col, $opponent);
                if ($tempBoard->checkWin($coord )) {
                    $this->play($col);
                    return;
                }
            }
        }

        $possibles = array();
        for ($col = 1; $col <= Board::COLUMNS; $col++) {
            if ($this->board->isValidMove($col)) {
                $possibles[] = $col;
            }
        }
        if (count($possibles)>2) {
            $random = rand(-1,1);
        }
        $middle = (int) (count($possibles) / 2)+$random;
        $inthemiddle = $possibles[$middle];
        $this->play($inthemiddle);
    }
    public function save(){
        // TODO: Guarda l'estat del joc a les sessions
    }
    public static function restore(){
        // TODO: Restaura l'estat del joc de les sessions
    }
 
}

```
  - **Documentació**:
    - Totes les classes i mètodes han d'estar documentats amb comentaris PHPDoc.

##### Controladors

- Dins de la carpeta Controllers:

    - **Classe `JocController`**: Crea un controlador `JocController` que gestione el  joc. Aquest controlador ha de permetre als jugadors realitzar moviments, comprovar l'estat del joc, i gestionar les vistes.
     
 ```php
  namespace Joc4enRatlla\Controllers;

    use Joc4enRatlla\Models\Player;
    use Joc4enRatlla\Models\Game;
    
    
    class GameController
    {
    private Game $game;
    
    // Request és l'array $_POST
    
    public function __construct($request=null)
    {
        // TODO: Inicialització del joc.Ha d'inicializar el Game si és la primera vegada o agafar les dades de la sessió si ja ha estat inicialitzada
         
        $this->play($request);

    }
 
    public function play(Array $request)  
    {
        // TODO : Gestió del joc. Ací es on s'ha de vore si hi ha guanyador, si el que juga es automàtic  o manual, s'ha polsat reiniciar...
        
       
        
        $board = $this->game->getBoard();
        $players = $this->game->getPlayers();
        $winner = $this->game->getWinner();
        $scores = $this->game->getScores();

        loadView('index',compact('board','players','winner','scores'));
     }
}
```

##### Serveis i funcions

- Dins de la carpeta Services:

    - **Funció `loadView`**: Crea una funció `loadView` que carregue les vistes del joc. Aquesta funció ha de rebre el nom de la vista i les dades a passar a la vista, i ha de mostrar la vista amb les dades proporcionades.

```php
<?php

namespace Joc4enRatlla\Services;

class Service
{
    public static function loadView($view, $data = [])
    {
        $viewPath = str_replace('.', '/', $view);
        extract($data);

        include  $_SERVER['DOCUMENT_ROOT'] . "/../Views/$viewPath.view.php";

    }
}
```

i la funció `loadView` en un fitxer de funcions

```php
  function loadView($view, $data = [])
    {
       Joc4enRatlla\Services\Service::loadView($view, $data);
    }

    function dd(...$data )
    {
        echo "<pre>";
        foreach ($data as $d) {
            var_dump($d);
        }

        echo "</pre>";
        die();
    }
``` 
 
##### Vistes

- Dins de la carpeta Views:

    - **Vista `index.php`**: Crea una vista `index.php` que mostre la graella del joc, el torn actual del jugador, i els resultats finals (guanyador o empat). Aquesta vista ha de permetre als jugadors realitzar moviments en la graella.
    
```php

<html>
<head>
    <link rel="stylesheet" href="4ratlla.css?v=<?php echo time(); ?>">
    <title>4 en ratlla</title>
    <style>
        .player1 {
            background-color: <?= $players[1]->getColor() ?> ; /* Color   per un dels jugadors */
        }

        .player2 {
            background-color:  <?= $players[2]->getColor() ?>; /* Color   per l'altre jugador */
        }

    </style>
</head>
<body>
<?php include_once $_SERVER['DOCUMENT_ROOT'].'/../Views/partials/error.view.php'  ?>
 <form action="<?php echo htmlspecialchars($_SERVER["PHP_SELF"]); ?>" method="post">
    <?php include_once $_SERVER['DOCUMENT_ROOT'].'/../Views/partials/board.view.php'  ?>
     <input type="submit" name="reset" value="Reiniciar joc">
     <input type="submit" name="exit" value="Acabar joc">
</form>
 <?php include_once $_SERVER['DOCUMENT_ROOT'].'/../Views/partials/panel.view.php'  ?>
</body>
</html>

```

board.view.php

```php
<div class="board">
    <table>
     <tr>
       <?php if (!$winner ):
        for ($j=1;$j<= $board::COLUMNS ;$j++): ?>
         <td><input type='submit' name='columna' value='<?=$j ?>' /></td>";
      <?php endfor ; else: ?>
        <h1>El guanyador es el jugador <?=  $winner ->getName() ?></h1>
      <?php endif ?>
     </tr>
      <?php for ($i=1;$i<= $board::FILES ;$i++):  ?>
          <tr>
         <?php for ($j=1;$j<= $board::COLUMNS ;$j++):  ?>
             <?php echo match ($board->getSlots()[$i][$j]){
                0 => '<td class="buid"></td>',
                1 => '<td class="player1"></td>',
                2 => '<td class="player2"></td>'};
                endfor ;
            endfor   ?>
         </tr>
    </table>
</div>
```
##### SPA

Creen la pàgina index.php que carregarà el joc 4 en ratlla.

```php
<?php
session_start();
require_once $_SERVER['DOCUMENT_ROOT'] . '/../vendor/autoload.php';
require_once $_SERVER['DOCUMENT_ROOT'] . '/../Helpers/functions.php';
use Joc4enRatlla\Controllers\GameController;

if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $gameController = new GameController($_POST); 
} else {
    loadView('jugador');
}
``` 
 
#### 4. Proves amb PHPUnit
- **Escriu Proves Unitàries**: Crea proves unitàries per a la classe `Joc4enRatlla` utilitzant PHPUnit. Les proves poden incloure:
    - Verificació de la configuració inicial de la graella.
    - Proves per assegurar que un moviment s'aplica correctament a la graella.
    - Proves per assegurar que el joc detecta correctament un guanyador o un empat.
- **Proves de Gestió de Sessions**: Afig proves per assegurar que l'estat del joc i el torn del jugador es mantenen correctament a través de les sessions.

#### 5. Logger amb Monolog
- **Configuració de Logger**: Utilitza `Monolog` per registrar esdeveniments importants del joc, com quan un jugador fa un moviment, quan s'inicia una nova partida, o quan es produeixen errors.
- **Diversos Handlers**:
    - Registra els moviments dels jugadors i els resultats del joc en un fitxer `game.log`.
    - Registra errors greus o problemes amb les sessions en un fitxer d'errors separat.

### Consideracions Addicionals pel  Projecte 

#### 1. Documentació amb PHPDoc
- **Documentació Completa**: Documenta totes les classes i mètodes amb comentaris PHPDoc. Això inclou les descripcions dels paràmetres i els valors de retorn per a cada mètode.
- **Generació Automàtica**: Utilitza `phpDocumentor` o una eina similar per generar la documentació automàticament. Afig la documentació generada al projecte per facilitar el manteniment i la comprensió del codi.

#### 2. Implementació d'Interfícies
- **Interfície `JocInterface`**: Crea una interfície que definisca els mètodes bàsics que qualsevol joc  ha de tindre (`iniciarJoc`, `ferMoviment`, `comprovaGuanyador`, etc.). Assegura't que la  `Joc4enRatlla` implemente  aquesta interfície.

#### 3. Serialització i Persistència
- **Serialització de l'Estat del Joc**: Implementa funcionalitats per serialitzar l'estat del joc (usant JSON o `serialize()`) i deserialitzar-lo per mantenir la persistència entre sessions o guardar l'estat per a reprendre la partida posteriorment.

#### 4. Exempcions
- **Gestió d'Excepcions**: Utilitza excepcions per gestionar el que un jugador jugue una columna que ja estiga plena. Afig el missatge  d'error al jocs.
   
#### 5. Fes que el jugador puga triar nom i color

- **Triar Nom i Color**: Permet als jugadors triar el seu nom i el color de les fitxes al començar una partida. Aquesta informació ha de ser guardada en les sessions i mostrada en la vista del joc.

#### Rúbrica de l'Avaluació

##### Funcionalitat del Joc
| Punts | Descripció |
|-------|-------------|
| 0     | El joc no és funcional o està incomplet. |
| 1     | El joc és funcional, però conté errors significatius. |
| 2     | El joc està majoritàriament funcional amb errors mínims. |
| 3     | El joc està completament funcional i sense errors. |

##### Implementació de Programació Orientada a Objectes (POO)
| Punts | Descripció |
|-------|-------------|
| 0     | No s'han utilitzat classes o s'ha fet de forma poc coherent. |
| 1     | Tots els models tenen la seua classe i és operativa. |
| 2     | L'aplicatiu funciona amb classes. |

##### Separació del Model de Negoci de la Presentació (MVC)
| Punts | Descripció |
|-------|-------------|
| 0     | No s'ha implementat la separació de model i presentació; el codi de lògica i presentació està mesclat. |
| 1     | Hi ha una separació parcial, però algunes parts de la lògica del negoci es barregen amb la presentació o a l'inrevés. |
| 2     | La separació entre model, vista i controlador està ben implementada, però podria millorar en alguns aspectes. |
| 3     | Excel·lent separació entre el model, vista i controlador, seguint els principis del patró MVC i mantenint un codi net. |

##### Integració de Composer i Autoloading
| Punts | Descripció |
|-------|-------------|
| 0     | No. |
| 1     | Sí. |

##### Implementació de Proves amb PHPUnit
| Punts | Descripció |
|-------|-------------|
| 0     | No s'han creat proves, o les proves creades són mínimes i no adequades per a verificar la funcionalitat. |
| 1     | Es presenten proves bàsiques amb PHPUnit, però cobreixen parcialment les funcionalitats requerides. |
| 2     | Proves unitàries completes que cobreixen la majoria dels casos, incloent proves de gestió de sessions i lògica de joc. |
| 3     | Proves exhaustives que cobreixen totes les funcionalitats i consideren casos límit, amb ús de mocks quan necessari. |

##### Ús de Logger amb Monolog
| Punts | Descripció |
|-------|-------------|
| 0     | No s'ha implementat el logger o no s'utilitza de manera efectiva per registrar esdeveniments importants. |
| 1     | Logger implementat, però amb ús limitat o incorrecte en la registració d'esdeveniments i errors. |
| 2     | Logger ben implementat, amb esdeveniments i errors registrats adequadament en diferents fitxers o canals. |

##### Documentació amb PHPDoc
| Punts | Descripció |
|-------|-------------|
| 0     | Falta documentació o és insuficient per comprendre les classes i mètodes del projecte. |
| 1     | Documentació bàsica amb PHPDoc, però amb omisions o descripcions poc clares. |
| 2     | Documentació completa amb PHPDoc per a totes les classes i mètodes, amb descripcions clares i detallades. |

##### Exempcions
| Punts | Descripció |
|-------|-------------|
| 0     | No hi ha. |
| 1     | Si hi ha però no es mostra missatge d'error. |
| 2     | Es tracta perfectament i hi ha missatge d'error. |

##### Interfície
| Punts | Descripció |
|-------|-------------|
| 0     | No hi ha. |
| 1     | Implementada. |

##### Elecció color Jugador i panell de resultats
| Punts | Descripció |
|-------|-------------|
| 0     | No. |
| 1     | Un dels dos. |
| 2     | Els dos. |

##### Qualitat del Codi i Bones Pràctiques
| Punts | Descripció |
|-------|-------------|
| 0     | Codi desordenat i sense comentaris. |
| 1     | Codi desorganitzat, amb molts errors de sintaxi, mala nomenclatura, o sense bones pràctiques de codi. |
| 2     | Codi ben escrit, seguint les convencions de nomenclatura i bones pràctiques de desenvolupament. |

##### Innovació i Creativitat
| Punts | Descripció |
|-------|-------------|
| 0     | Cap creativitat o innovació en el projecte. |
| 1     | Algunes idees creatives han estat implementades. |
| 2     | El projecte mostra innovació significativa. |


## 15. Autoavaluació: Programació Orientada a Objectes en PHP

#### Exercici 1: Constructors en PHP

##### Pregunta:
Quina és la funció principal d'un constructor en una classe PHP?

##### Opcions:
<form>
  <input type="radio" id="q1a" name="question1" value="a">
  <label for="q1a">a) Destruir els objectes de la classe quan ja no són necessaris.</label><br>
  <input type="radio" id="q1b" name="question1" value="b">
  <label for="q1b">b) Inicialitzar les propietats de l'objecte quan es crea.</label><br>
  <input type="radio" id="q1c" name="question1" value="c">
  <label for="q1c">c) Executar una funció arbitrària abans de cada mètode.</label><br>
  <input type="radio" id="q1d" name="question1" value="d">
  <label for="q1d">d) Crear mètodes màgics automàticament.</label><br><br>
  <input type="button" value="Comprovar" onclick="checkAnswer1()">
</form>

<p id="result1"></p>

<script>
function checkAnswer1() {
    var correctAnswer = "b";
    var radios = document.getElementsByName('question1');
    var userAnswer;
    for (var i = 0; i < radios.length; i++) {
        if (radios[i].checked) {
            userAnswer = radios[i].value;
            break;
        }
    }
    var resultText = userAnswer === correctAnswer ? "Correcte!" : "Incorrecte. La resposta correcta és b) Inicialitzar les propietats de l'objecte quan es crea.";
    document.getElementById('result1').innerText = resultText;
}
</script>

#### Exercici 2: Herència en PHP

##### Pregunta:
Quina és l'avantatge principal de l'herència en la programació orientada a objectes?

##### Opcions:
<form>
  <input type="radio" id="q2a" name="question2" value="a">
  <label for="q2a">a) Permet reutilitzar codi definint classes noves basades en classes existents.</label><br>
  <input type="radio" id="q2b" name="question2" value="b">
  <label for="q2b">b) Permet ocultar totes les propietats i mètodes de la classe.</label><br>
  <input type="radio" id="q2c" name="question2" value="c">
  <label for="q2c">c) Permet definir funcions globals sense necessitat de classes.</label><br>
  <input type="radio" id="q2d" name="question2" value="d">
  <label for="q2d">d) Permet cridar a funcions de JavaScript des de PHP.</label><br><br>
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
    var resultText = userAnswer === correctAnswer ? "Correcte!" : "Incorrecte. La resposta correcta és a) Permet reutilitzar codi definint classes noves basades en classes existents.";
    document.getElementById('result2').innerText = resultText;
}
</script>

#### Exercici 3: Polimorfisme

##### Pregunta:
Què permet el polimorfisme en el context de la POO?

##### Opcions:
<form>
  <input type="radio" id="q3a" name="question3" value="a">
  <label for="q3a">a) Permet que una funció tinga múltiples implementacions depenent de l'objecte que la cride.</label><br>
  <input type="radio" id="q3b" name="question3" value="b">
  <label for="q3b">b) Permet la creació d'objectes a partir de funcions anònimes.</label><br>
  <input type="radio" id="q3c" name="question3" value="c">
  <label for="q3c">c) Permet la connexió entre PHP i bases de dades relacionals.</label><br>
  <input type="radio" id="q3d" name="question3" value="d">
  <label for="q3d">d) Permet executar múltiples scripts PHP alhora.</label><br><br>
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
    var resultText = userAnswer === correctAnswer ? "Correcte!" : "Incorrecte. La resposta correcta és a) Permet que una funció tinga múltiples implementacions depenent de l'objecte que la cride.";
    document.getElementById('result3').innerText = resultText;
}
</script>

#### Exercici 4: Espais de Noms

##### Pregunta:
Per a què s'utilitzen els espais de noms (namespaces) en PHP?

##### Opcions:
<form>
  <input type="radio" id="q4a" name="question4" value="a">
  <label for="q4a">a) Per executar codi PHP de forma asincrònica.</label><br>
  <input type="radio" id="q4b" name="question4" value="b">
  <label for="q4b">b) Per evitar conflictes entre noms de classes, funcions o constants en diferents parts del codi.</label><br>
  <input type="radio" id="q4c" name="question4" value="c">
  <label for="q4c">c) Per definir variables globals accessibles des de qualsevol punt del codi.</label><br>
  <input type="radio" id="q4d" name="question4" value="d">
  <label for="q4d">d) Per importar codi d'altres llenguatges de programació com JavaScript.</label><br><br>
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
    var resultText = userAnswer === correctAnswer ? "Correcte!" : "Incorrecte. La resposta correcta és b) Per evitar conflictes entre noms de classes, funcions o constants en diferents parts del codi.";
    document.getElementById('result4').innerText = resultText;
}
</script>

#### Exercici 5: Traits en PHP

##### Pregunta:
Quin avantatge ofereixen els traits en PHP?

##### Opcions:
<form>
  <input type="radio" id="q5a" name="question5" value="a">
  <label for="q5a">a) Permet escriure codi reutilitzable que es pot incloure en múltiples classes, independentment de la jerarquia d'herència.</label><br>
  <input type="radio" id="q5b" name="question5" value="b">
  <label for="q5b">b) Permet la creació de funcions globals en PHP.</label><br>
  <input type="radio" id="q5c" name="question5" value="c">
  <label for="q5c">c) Permet la comunicació entre diferents servidors web.</label><br>
  <input type="radio" id="q5d" name="question5" value="d">
  <label for="q5d">d) Permet executar codi PHP dins de plantilles HTML.</label><br><br>
  <input type="button" value="Comprovar" onclick="checkAnswer5()">
</form>

<p id="result5"></p>

<script>
function checkAnswer5() {
    var correctAnswer = "a";
    var radios = document.getElementsByName('question5');
    var userAnswer;
    for (var i = 0; i < radios.length; i++) {
        if (radios[i].checked) {
            userAnswer = radios[i].value;
            break;
        }
    }
    var resultText = userAnswer === correctAnswer ? "Correcte!" : "Incorrecte. La resposta correcta és a) Permet escriure codi reutilitzable que es pot incloure en múltiples classes, independentment de la jerarquia d'herència.";
    document.getElementById('result5').innerText = resultText;
}
</script>

#### Exercici 6: Excepcions en PHP

##### Pregunta:
Quina és la finalitat d'utilitzar excepcions en PHP?

##### Opcions:
<form>
  <input type="radio" id="q6a" name="question6" value="a">
  <label for="q6a">a) Evitar l'execució de codi mal format.</label><br>
  <input type="radio" id="q6b" name="question6" value="b">
  <label for="q6b">b) Gestionar errors i condicions excepcionals de manera controlada dins d'una aplicació.</label><br>
  <input type="radio" id="q6c" name="question6" value="c">
  <label for="q6c">c) Declarar funcions dins d'una classe.</label><br>
  <input type="radio" id="q6d" name="question6" value="d">
  <label for="q6d">d) Garantir que totes les variables estiguen inicialitzades abans del seu ús.</label><br><br>
  <input type="button" value="Comprovar" onclick="checkAnswer6()">
</form>

<p id="result6"></p>

<script>
function checkAnswer6() {
    var correctAnswer = "b";
    var radios = document.getElementsByName('question6');
    var userAnswer;
    for (var i = 0; i < radios.length; i++) {
        if (radios[i].checked) {
            userAnswer = radios[i].value;
            break;
        }
    }
    var resultText = userAnswer === correctAnswer ? "Correcte!" : "Incorrecte. La resposta correcta és b) Gestionar errors i condicions excepcionals de manera controlada dins d'una aplicació.";
    document.getElementById('result6').innerText = resultText;
}
</script>

#### Exercici 7: Autoloading en PHP

##### Pregunta:
Quin avantatge ofereix l'autoloading en PHP?

##### Opcions:
<form>
  <input type="radio" id="q7a" name="question7" value="a">
  <label for="q7a">a) Permet que les classes es carreguen automàticament quan s'utilitzen, sense necessitat de fer incloure manualment cada fitxer.</label><br>
  <input type="radio" id="q7b" name="question7" value="b">
  <label for="q7b">b) Permet l'execució de múltiples scripts alhora.</label><br>
  <input type="radio" id="q7c" name="question7" value="c">
  <label for="q7c">c) Permet la manipulació de fitxers en el servidor.</label><br>
  <input type="radio" id="q7d" name="question7" value="d">
  <label for="q7d">d) Permet la connexió amb bases de dades.</label><br><br>
  <input type="button" value="Comprovar" onclick="checkAnswer7()">
</form>

<p id="result7"></p>

<script>
function checkAnswer7() {
    var correctAnswer = "a";
    var radios = document.getElementsByName('question7');
    var userAnswer;
    for (var i = 0; i < radios.length; i++) {
        if (radios[i].checked) {
            userAnswer = radios[i].value;
            break;
        }
    }
    var resultText = userAnswer === correctAnswer ? "Correcte!" : "Incorrecte. La resposta correcta és a) Permet que les classes es carreguen automàticament quan s'utilitzen, sense necessitat de fer incloure manualment cada fitxer.";
    document.getElementById('result7').innerText = resultText;
}
</script>
# Desenvolupament d'aplicacions web: Accés a Dades.

??? abstract "Duració i criteris d'avaluació"

    Duració estimada: 10 hores

    <hr />

    | Resultat d'aprenentatge | Criteris d'avaluació |
    | --------                | --------             |
    | 6. Desenvolupa aplicacions web d'accés a magatzems de dades, aplicant mesures per a mantindre la seguretat i la integritat de la informació.| a) S'han analitzat les tecnologies que permeten l'accés mitjançant programació a la informació disponible en magatzems de dades. <br/> b) S'han creat aplicacions que establisquen connexions amb bases de dades. <br/> c) S'ha recuperat informació emmagatzemada en bases de dades. <br/> d) S'ha publicat en aplicacions web la informació recuperada. <br/> e) S'han utilitzat conjunts de dades per a emmagatzemar la informació. <br/> f) S'han creat aplicacions web que permeten l'actualització i l'eliminació  d'informació disponible en una base de dades.<br/> g) S'han provat i documentat les aplicacions web. |


En aquesta unitat aprendrem a accedir a dades que es troben en un servidor; recuperant, editant i creant aquestes dades a través d'una base de dades.

A través de les diferents capes o nivells, de les quals 2 d'elles ja coneixem (*Nginx*, *PHP*) i *MySQL* la que estudiarem en aquest tema.

<div class="center img-large">
    <img src="imagenes/06/06-bbdd-arquitectura-3-niveles.png">
</div>

## 1. Introducció a les tecnologies per accedir a dades

### Bases de dades relacionals (SQL)
Les bases de dades relacionals utilitzen llenguatge SQL per emmagatzemar i recuperar dades de taules relacionades. En PHP, les tecnologies més utilitzades per accedir-hi són **PDO** i **MySQLi**. **PDO** suporta múltiples sistemes de bases de dades (MySQL, PostgreSQL, etc.), mentre que **MySQLi** està dissenyat específicament per a MySQL.

### Bases de dades NoSQL
Les bases de dades NoSQL, com **MongoDB** o **Firebase**, emmagatzemen dades en formats no estructurats, com JSON. Aquestes són ideals per a aplicacions que gestionen grans volums de dades o dades no estructurades. **MongoDB** és un sistema orientat a documents, mentre que **Firebase** és conegut per les seves capacitats en temps real.

### Accés a APIs
Les **APIs REST** permeten accedir a dades de serveis web externs utilitzant sol·licituds HTTP i respostes en formats com JSON o XML. **GraphQL** és una alternativa moderna que permet sol·licituds més específiques, només retornant les dades necessàries, en contrast amb les sol·licituds REST, que poden ser més generals.

### Web Scraping
El **web scraping** és el procés d'extracció automàtica de dades de pàgines web. Aquesta tècnica es pot utilitzar per recuperar informació d'una pàgina web quan no hi ha una API disponible. En PHP, es poden utilitzar diverses biblioteques per descarregar i analitzar contingut HTML, com ara **cURL** i **DOMDocument**.

### Consideracions de seguretat
És fonamental garantir la seguretat quan es treballa amb l'accés a dades. Això inclou protegir les aplicacions contra vulnerabilitats comunes, com les **injeccions SQL**, i assegurar les connexions utilitzant **SSL/TLS** quan es comuniqui amb bases de dades remotes o APIs externes.


## 2. Bases de dades relacionals (SQL)

### Instal·lació
A través de **XAMPP** és molt senzill, simplement ens descarregaríem el programa i l'activaríem. Per a descarregar XAMPP [prem ací](https://www.apachefriends.org/es/download.html).

Amb ***Docker*** utilitzarem un altre  repositori que inclou el mysql i el phpMyAdmin i llancem
``` bash
docker-compose up -d
```

Si tot ha eixit bé i el contenidor està en marxa, podrem visitar la pàgina de phpMyAdmin de la següent manera
``` html
http://localhost:8000
```

<div class="center img-medium">
    <img src="imagenes/06/06-bbdd-phpMyAdmin-login.png">
</div>

Per a accedir hem d'utilitzar les següents credencials que venen configurades en el arxiu `docker-compose.yml`

```
usuario: root
contraseña: 1234
```

### Estructura d'una base de dades

Sabem que una base de dades té molts camps amb els seus noms i valors, però a més sabem que la base de dades ha de tindre un nom. per tant tindríem la següent estructura per a una base de dades:
    
    NombreBaseDeDatos
        |__Tabla-#1
        |       |__DatosTabla-#1
        |
        |__Tabla-#2
        |       |__DatosTabla-#2
        |
        |__Tabla-#3
        |       |__DatosTabla-#3
        [...]


Vegem-ho en un exemple real

    Ryanair
        |__pasajero
        |    |__id[*]
        |    |__nombre
        |    |__apellidos
        |    |__edad
        |    |__id_vuelo[^]
        |
        |__vuelo
        |    |__id[*]
        |    |__n_plazas
        |    |__disponible
        |    |__id_pais[^]
        |
        |__pais
             |__id[*]
             |__nombre

<div class="leyenda">
    [*] Clau primària [^] Clave Forània
</div>

<div class="center img-large">
    <img src="imagenes/06/06-bbdd-estructura.png">
</div>

### SQL

Aquest llenguatge de consulta estructurada (*Structured Query Language*) és el que utilitzarem per a realitzar les consultes a les nostres bases de dades per a mostrar el contingut en les diferents interfícies web que creem al llarg de la unitat. Si vols saber més detalls visita [Wiki SQL](https://es.wikipedia.org/wiki/sql)

Exemple d'una sentència SQL on seleccionem totes les files i columnes de la nostra taula anomenada **'pais'**

``` sql
SELECT * FROM pais
```

Estas sentencias pueden invocarse desde la consola de comandos mediante el intérprete *mysql* (previamente instalado en el sistema) o a través de la herramienta phpMyAdmin.

Las sentencias SQL también las podemos usar dentro de nuestro código php, de tal manera que cuando se cargue nuestra interfaz web, lance una sentecia SQL para mostrar los datos que queramos.

``` php
<?php
    // Llistat de clients, adreçats per DNI de manera ASCendent
    $clientesOrdenadosPorDNI = "SELECT * FROM `pasajero` ORDER BY `dni`" ASC;
?>
```

### phpMyAdmin

<div class="center img-medium">
    <img src="imagenes/06/06-bbdd-phpMyAdmin-logo.png">
</div>

Aquest programari funciona sota Ngingx i PHP i és més que res una interfície web per a gestionar les bases de dades que tinguem disponibles en el nostre servidor local. Molts **hostings* ofereixen aquesta eina per defecte per a poder gestionar les BBDD que tinguem configurades sota el nostre compte.

#### Creant una base de dades dins de phpMyAdmin

<div class="center img-large">
    <img src="imagenes/06/06-bbdd-phpMyAdmin.gif">
</div>

1.  Per a crear una nova base de dades hem d'entrar en *phpMyAdmin* com a *usuari root* i punxar en l'opció <span class="warning">*Nova*</span> del menú de l'esquerra.

2. En la nova finestra de creació posarem un **nom** a nostra *bbdd*.

3. També establirem el **cotejamiento** <span class="warning">*utf8m4_unicode_ci*</span> perquè nostra *bbdd* suporte tot tipus de caràcters (com els asiàtics) i fins i tot *emojis* ;)

4. Li donem al botó de **Crear** per a crear la *bbdd* i començar a escriure les diferents taules que anem a introduir en ella.

El sistema generarà el codi SQL per a crear tot el que li hem posat i crearà la base de dades amb les taules que li hàgem ficat.
``` sql
CREATE TABLE `persona`. ( `id` INT NOT NULL AUTO_INCREMENT , `nombre` TINYTEXT NOT NULL , `apellidos` TEXT NOT NULL , `telefono` TINYTEXT NOT NULL , PRIMARY KEY (`id`)) ENGINE = InnoDB;
```

#### Opcions en phpMyAdmin

Quan seleccionem una base de dades de la llista, el sistema ens mostra diverses pestanyes amb les quals interactuar amb la base de dades en qüestió:

- `Estructura`: Podem veure les diferents taules que consoliden la nostra base de dades

- `SQL`: Per si volem injectar codi SQL perquè el sistema l'interprete

- `Buscar`: Serveix per a buscar per termes, en la nostra base de dades, aplicant diferents filtres de cerca

- `Generar consulta`: semblança a SQL però d'una manera més gràfica, sense haver de saber res del llenguatge

- `Exportar i importar`: Com el seu nom indica, per a fer qualsevol de les 2 operacions sobre la base de dades

- `Operacions`: Diferents opcions avançades per a realitzar en la nostra base de dades, de la qual destacarem l'opció *Cotejamiento* on podrem canviar el *cotejamiento* de la nostra taula però <span class="alert">*ULL AMB ACÔ* perquè podem eliminar dades sense voler, ja que en canviar el *cotejamiento* podem suprimir caràcters no suportats pel nou *cotejamiento*</span>

No aprofundirem en la resta d'opcions però, en la pestanya **Més** existeix l'opció **Dissenyador** per a poder editar les relacions entre taules d'una manera gràfica (punxant i arrossegant) que veurem més endavant.

## 3. PHP Data Objects :: PDO

La classe PDO de PHP s'utilitza per connectar-se a una base de dades i executar consultes SQL de manera segura. Quan construeixes una instància de PDO, pots passar-li diferents atributs en el constructor i opcions per configurar el comportament de la connexió. Aquí tens els atributs principals i el seu propòsit:

### Constructor de la classe PDO

El constructor de la classe PDO accepta tres paràmetres obligatoris i un opcional:

``` php
<?php
    $pdo = new PDO(string $dsn, string $username, string $password, array $options);

```

* $dsn (Data Source Name): És una cadena que especifica el tipus de base de dades i la informació necessària per connectar-s'hi.
  * Format per tipus de base de dades i configuració, per exemple:
    * Mysql:host=localhost;dbname=testdb (per a MySQL).
    * pgsql:host=localhost;port=5432;dbname=testdb (per a PostgreSQL).
    * sqlite:/path/to/database.db (per a SQLite).
  * $username: El nom d'usuari per a la connexió a la base de dades.
  * $password: La contrasenya associada al nom d'usuari.
  * $options (Opcional): Un array d'opcions per definir el comportament de la connexió. Aquests són alguns dels valors més comuns que es poden definir en aquest array:
    * PDO::ATTR_ERRMODE: Controla com es gestionen els errors. Alguns valors comuns són:
      * PDO::ERRMODE_SILENT: Els errors no generen cap missatge.
      * PDO::ERRMODE_WARNING: Els errors generen un avís.
      * PDO::ERRMODE_EXCEPTION: Els errors generen una excepció, que és el més recomanable per controlar errors.
    * PDO::ATTR_DEFAULT_FETCH_MODE: Defineix el mode de recuperació de dades per defecte, com ara:
      * PDO::FETCH_ASSOC: Retorna les dades com un array associatiu.
      * PDO::FETCH_OBJ: Retorna les dades com un objecte.
      * PDO::FETCH_BOTH: Retorna les dades com un array associatiu i numèric.
    * PDO::ATTR_PERSISTENT: Habilita connexions persistents. Una connexió persistent pot millorar el rendiment mantenint la connexió activa per múltiples peticions en lloc de crear-ne una nova cada vegada.
    * PDO::ATTR_TIMEOUT: Defineix un temps límit per a la connexió en segons.

##### Exemple de connexió amb PDO

``` php     
$dsn = "mysql:host=localhost;dbname=testdb";
$username = "usuari";
$password = "contrasenya";
$options = [
    PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION,
    PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_ASSOC,
    PDO::ATTR_PERSISTENT => true,
    PDO::MYSQL_ATTR_INIT_COMMAND => "SET NAMES utf8"
];

try {
    $pdo = new PDO($dsn, $username, $password, $options);
    echo "Connexió establerta amb èxit!";
} catch (PDOException $e) {
    echo "Error de connexió: " . $e->getMessage();
}
```

Aquest codi estableix una connexió a una base de dades MySQL amb un joc de caràcters utf8, una connexió persistent, i llança excepcions en cas d'errors.

 
Qualsevol error que es llance a través de **PDO**, el sistema llançarà una  **PDOException** .

### Fitxer de configuració de la BD

De la mateixa manera que podem tenir el nostre arxiu de funcions `funciones.php` i alberguem totes les funcions que s'usen de manera global en l'aplicació, podem establir un arxiu de constants on definim els paràmetres de connexió amb la base de dades.
```php
<?php

    //  ▒▒▒▒▒▒▒▒ conexion.php ▒▒▒▒▒▒▒▒

    constDSN = "mysql:host=localhost;dbname=dwes";
    constUSUARIO = "dwes";
    constPASSWORD = "abc123";

    /*  ▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒

        ▒▒▒▒▒▒▒▒ NO SUBAS ESTE ARCHIVO A git ▒▒▒▒▒

        ▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒ */

```

Aquest arxiu conté informació <span class="alert">**molt sensible**</span> així que no és recomanable que puges aquest arxiu a **git**.

### Sentències preparades

Es tracta de sentències que s'estableixen com si foren plantilles de la SQL que llançarem, acceptant paràmetres que són establits a posteriori de la declaració de la sentència preparada.

Les sentències preparades eviten la **injecció** de SQL (SQL Injection) i milloren el rendiment de nostres *aplicacions* o pàgines web.

``` php
<?php
    $sql = "INSERT INTO Clientes VALUES (?, ?, ?, ?)";
```

Cada interrogant és un paràmetre que establirem després, unes quantes línies més a baix.

Una vegada tenim la plantilla de la nostra consulta, hem de seguir amb la preparació juntament amb 3 mètodes més de **PHP** per a la seua completa execució:

- `prepare:` prepara la **sentencia** abans de ser executada.
- `bind`: el tipus d'unió (**bind*^) de dada que pot ser mitjançant ' ? ' o ' :parametre '
- `execute` s'executa la consulta unint la plantilla amb les *variables* o paràmetres que hem establit.

### Exemple paràmetros

```php
<?php
     

    include "config/database.inc.php";

    $conexion = null;

    try { 
        $cantidad = $_GET["cantidad"];

        $conexion = new PDO(DSN, USUARIO, PASSWORD);
        $conexion -> setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);

        $sql = "DELETE FROM stock WHERE unidades = ?";
        $sentencia = $conexion -> prepare($sql);

        $isOk = $sentencia -> execute([$cantidad]);
        $cantidadAfectada = $sentencia -> rowCount();

        echo $cantidadAfectada;
    } catch (PDOException $e) {
        echo $e -> getMessage();
    }

    $conexion = null
```

### Exemple bindParam

Molt semblant a utilitzar paràmetres però aquesta vegada la variable està dins de la sentència SQL, en aquest cas l'hem anomenada `:cant`

```php
<?php
    include "config/database.inc.php";

    $conexion=null;

    try {
        $cantidad = $_GET["cantidad"] ?? 0;

        $conexion = new PDO(DSN, USUARIO, PASSWORD);
        $conexion -> setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);

        $sql = "DELETE FROM stock WHERE unidades = :cant";

        $sentencia = $conexion -> prepare($sql);
        $sentencia -> bindParam(":cant", $cantidad);
        
        $isOk = $sentencia -> execute();
        
        $cantidadAfectada = $sentencia -> rowCount();
        
        echo $cantidadAfectada;
    } catch (PDOException $e) {
        echo $e -> getMessage();
    }

    $conexion = null;
```

### bindParam VS bindValue

Utilitzarem `bindValue()` quan hàgem d'inserir dades només una vegada, en canvi, haurem d'usar `bindParam()` quan hàgem de passar dades múltiples, com per exemple, un *array*.

```php
<?php
    // se asignan nombre a los parámetros
    $sql = "DELETE FROM stock WHERE unidades = :cant";
    $sentencia = $conexion -> prepare($sql);

    // bindParam enlaza por referencia
    $cantidad = 0;

    $sentencia -> bindParam(":cant", $cantidad);
    $cantidad = 1;

    // se eliminan con cant = 1
    $isOk = $sentencia -> execute();

    // bindValue enlaza por valor
    $cantidad = 0;

    $sentencia -> bindValue(":cant", $cantidad);
    $cantidad = 1;

    // se eliminan con cant = 0
    $isOk = $sentencia->execute();
```

Per a més informació i ús de les variables *PDO* [consulta el manual de PHP](https://www.php.net/manual/es/pdo.constants.php).

### Inserint registres

A l'hora d'inserir registres en una base de dades, hem de tindre en compte que en la taula pot haver-hi valors autoincrementats. Per a salvaguardar açò, el que hem de fer és deixar aqueix camp autoincrementat buit, però a l'hora de fer la connexió, hem de recuperar-ho amb el mètode `lastInsertId()`.

``` php
<?php
    $nombre = $_GET["nombre"] ?? "SUCURSAL X";
    $telefono = $_GET["telefono"] ?? "636123456";

    $sql="INSERT INTO tienda(nombre, tlf) VALUES (:nombre, :telefono)";

    $sentencia = $conexion -> prepare($sql);
    $sentencia -> bindParam(":nombre", $nombre);
    $sentencia -> bindParam(":telefono", $telefono);

    $isOk = $sentencia -> execute();
    $idGenerado = $conexion -> lastInsertId();

    echo $idGenerado;
```

### Consultant registres

A l'hora de recuperar els resultats d'una consulta, bastarà amb invocar al mètode `PDOStatement::fetch` per a llistar les files generades per la consulta.

Però hem de triar el tipus de dada que volem rebre entre els 3 que hi ha disponibles:

- `PDO::FETCH_ASSOC:` array indexat que els seus keys són el nom de les columnes.
- `PDO::FETCH_NUM:` array indexat que els seus keys són números.
- `PDO::FETCH_BOTH:` valor per defecte. Retorna un array indexat que els seus keys són tant el nom de les columnes com números.

<div class="center img-large">
    <img src="imagenes/06/06-pdo-listado-fetch.png">
</div>

``` php
<?php
    //  ▒▒▒▒▒▒▒▒ consulta con array asociativo.php ▒▒▒▒▒▒▒▒

    include "config/database.inc.php";

    $conexion = null;

    try{
        $conexion = new PDO(DSN, USUARIO, PASSWORD);
        $conexion -> setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);

        $sql = "select * from tienda";

        $sentencia = $conexion -> prepare($sql);
        $sentencia -> setFetchMode(PDO::FETCH_ASSOC);
        $sentencia -> execute();
        
        while($fila = $sentencia -> fetch()){
            echo "Codigo:" . $fila["cod"] . "<br />";
            echo "Nombre:" . $fila["nombre"] . "<br />";
            echo "Teléfono:" . $fila["tlf"] . "<br />";
        }

    }catch(PDOException $e) {
        echo $e -> getMessage();
    }

    $conexion = null;
```

Recuperant dades amb una matriu com a resultat de la nostra consulta

``` php
<?php
    //  ▒▒▒▒▒▒▒▒ consulta con array asociativo ▒▒▒▒▒▒▒▒

    $sql="SELECT * FROM tienda";

    $sentencia = $conexion -> prepare($sql);
    $sentencia -> setFetchMode(PDO::FETCH_ASSOC);
    $sentencia -> execute();

    $tiendas = $sentencia -> fetchAll();

    foreach($tiendasas$tienda) {
        echo"Codigo:" . $tienda["cod"] . "<br />";
        echo"Nombre:" . $tienda["nombre"] . "<br />";
    }
```
Però si el que volem és llegir dades amb forma d'objecte utilitzant `PDO::FETCH_OBJ`, hem de crear un objecte amb propietats públiques amb el mateix nom que les columnes de la taula que anem a consultar.

``` php
<?php
    //  ▒▒▒▒▒▒▒▒ consulta con formato de objeto ▒▒▒▒▒▒▒▒

    $sql="SELECT * FROM tienda";

    $sentencia = $conexion -> prepare($sql);
    $sentencia -> setFetchMode(PDO::FETCH_OBJ);
    $sentencia -> execute();

    while($t = $sentencia -> fetch()) {
        echo"Codigo:" . $t -> cod . "<br />";
        echo"Nombre:" . $t -> nombre . "<br />";
        echo"Teléfono:" . $t -> tlf . "<br />";
    }
```

### Consultes amb models

Portem temps creant classes en PHP i les consultes també admeten aquest tipus de dades mitjançant l'ús de `PDO::FETCH_CLASS`

Si usem aquest mètode, hem de tindre en compte que els noms dels atributs privats han de coincidir amb els noms de les columnes de la taula que anem a manejar.

Així doncs, si pel que siga canviem l'estructura de la taula <span class="alert">**HEM DE CANVIAR**</span> la nostra classe perquè tot continue funcionant.

``` php
<?php
    //  ▒▒▒▒▒▒▒▒ clase Tienda ▒▒▒▒▒▒▒▒

    classTienda {
        private int $cod;
        private string $nombre;
        private ? string $tlf;
        
        public function getCodigo() : int {
            return $this -> cod;
        }
        
        public function getNombre() : string {
            return $this -> nombre;
        }
        
        public function getTelefono() : ?string {
            return $this -> tlf;
        }
    }
```

``` php
<?php
    //  ▒▒▒▒▒▒▒▒ Consultando a través de la clase Tienda ▒▒▒▒▒▒▒▒

    $sql = "SELECT * FROM tienda";
    $sentencia = $conexion -> prepare($sql);

    // Aquí 'Tienda' es el nombre de nuestra clase
    $sentencia -> setFetchMode(PDO::FETCH_CLASS, Tienda::class);
    $sentencia -> execute();

    while($t = $sentencia -> fetch()) {
        echo "Codigo: " . $t -> getCodigo() . "<br />";
        echo "Nombre: " . $t -> getNombre() . "<br />";
        echo "Teléfono: " . $t -> getTelefono() . "<br />";
        
        var_dump($t);
    }
```

Però què passa si les nostres classes tenen constructor? doncs que hem d'indicar-li, al mètode FECTH, que emplene les propietats després de cridar al constructor i per a això fem ús de `PDO::FETCH_PROPS_LATE`.
``` php
<?php
    //  ▒▒▒▒▒▒▒▒ Consulta para una clase con constructor ▒▒▒▒▒▒▒▒

    $sql = "SELECT * FROM tienda";

    $sentencia = $conexion -> prepare($sql);
    $sentencia -> setFetchMode(PDO::FETCH_CLASS | PDO::FETCH_PROPS_LATE, Tienda::class);
    $sentencia -> execute();

    $tiendas = $sentencia -> fetchAll();
```

### Consultes amb LIKE

Per a utilitzar el comodí *LIKE* o altres comodins, hem d'associar-lo a la dada i MAI en la pròpia consulta.

``` php
<?php
    //  ▒▒▒▒▒▒▒▒ Utilizando comodines :: LIKE ▒▒▒▒▒▒▒▒

    $sql = "SELECT * FROM tienda where nombre like :nombre or tlf like :tlf";

    $sentencia = $conexion -> prepare($sql);
    $sentencia -> setFetchMode(PDO::FETCH_CLASS | PDO::FETCH_PROPS_LATE, Tienda::class);

    $cadBuscar = "%" . $busqueda . "%";

    $sentencia -> execute(["nombre" => $cadBuscar,"tlf" => $cadBuscar]);

    $result = $sentencia -> fetchAll();
```

Teniu una llista d'exemples molt completa en la [documentació oficial](https://phpdelusions.net/pdo/objects).

## 4. Login & Password

<div class="center img-medium">
    <img src="imagenes/06/06-login-password.gif">
</div>

Per a manejar un sistema complet de login i password amb contrasenyes xifrades, necessitem un mètode que xifre aqueixos *strings* que l'usuari introdueix com a contrasenya; tant en el formulari de registre com en el del *login*, ja que en codificar una contrasenya, després hem de descodificar-la per a comprovar que totes dues *contrasenyes (la que introdueix l'usuari en el login i la que tenim en la base de dades) coincidisquen.

Necessitem doncs:

- `password_hash()` per a emmagatzemar la contrasenya en la base de dades a l'hora de fer el *INSERT*
- `PASSWORD_DEFAULT` emmagatzemem la contrasenya usant el mètode d'encriptació bcrypt

- `PASSWORD_BCRYPT` emmagatzemem la contrasenya usant l'algorisme CRYPT_BLOWFISH compatible amb crypt()

- `password_verify()` per a verificar l'usuari i la contrasenya

``` php
<?php
    //  ▒▒▒▒▒▒▒▒ Almacenando usuario y password en BD ▒▒▒▒▒▒▒▒

    $usu = $_POST["usuario"];
    $pas = $_POST["password"];

    $sql = "INSERT INTO usuarios(usuario, password) VALUES (:usuario, :password)";

    $sentencia = $conexion -> prepare($sql);

    $isOk = $sentencia -> execute([
        "usuario" => $usu,
        "password" => password_hash($pas,PASSWORD_DEFAULT)
    ]);
```

Ara que tenim l'usuari codificat i guardat en la base de dades, el recuperarem per a poder loguejar-lo correctament.
``` php
<?php
    //  ▒▒▒▒▒▒▒▒ Recuperando usuario y password en BD ▒▒▒▒▒▒▒▒

    $usu = $_POST["login"] ?? "";

    $sql = "select * from usuarios where usuario = ?";

    $sentencia = $conexion -> prepare($sql);
    $sentencia -> execute([$usu]);

    $usuario = $sentencia -> fetch();

    if($usuario && password_verify($_POST['pass'], $usuario['password'])) {
        echo"OK!";
    } else {
        echo"KO";
    }
```

## 5. QueryBuilder

Un Query Builder (Constructor de Consultes) és una eina o classe que facilita la creació, execució i manipulació de consultes SQL en un programa. L'objectiu principal és proporcionar una interfície més intuïtiva i segura per interactuar amb bases de dades, sense haver d'escriure consultes SQL en brut.

A continuació, detallo algunes de les principals avantatges i característiques d'un Query Builder com el que has compartit anteriorment:

 * 1. Abstracció de la Base de Dades:
 - El Query Builder proporciona una capa d'abstracció que permet interactuar amb diferents tipus de bases de dades (MySQL, PostgreSQL, SQLite, etc.) sense canviar el codi de la teva aplicació. Això facilita la portabilitat i l'escalabilitat del codi.

 * 2. Seguretat:
 - Prevé injeccions SQL: Gràcies a l'ús de sentències preparades i enllaçament de paràmetres, el Query Builder ajuda a prevenir atacs d'injecció SQL, una de les amenaces més comunes en desenvolupament web.

 * 3. Sintaxi Més Neta i Més Fàcil:
 - Els Query Builders solen proporcionar una sintaxi més neta i fàcil d'entendre que les cadenes SQL pures. Això fa que el codi sigui més llegible i fàcil de mantenir.

 * 4. Reutilització de Codi:
 - Les funcions del Query Builder es poden reutilitzar a tot el projecte, reduint la duplicació de codi i facilitant el manteniment.

 * 5. Flexibilitat:
 - Permet realitzar consultes complexes amb una sintaxi simplificada, facilitant l'adaptació del codi a canvis en els requeriments de l'aplicació.

 * 6. Desenvolupament Més Ràpid:
 - Ajuda a accelerar el procés de desenvolupament, ja que els desenvolupadors no necessiten recordar la sintaxi SQL exacta per a cada tipus de base de dades.

 * 7. Fàcil de Depurar:
 - El codi generat pel Query Builder és més fàcil de depurar en comparació amb les llargues cadenes SQL.

 * 8. Suport per a Operacions CRUD:
 - Els Query Builders solen incloure suport integrat per a operacions CRUD (Crear, Llegir, Actualitzar, Esborrar), fent més fàcil la manipulació de dades.

En resum, un Query Builder serveix per simplificar la interacció amb bases de dades, proporcionant una interfície més segura, neta i fàcil d'utilitzar que les cadenes SQL pures. Ajuda a accelerar el desenvolupament, facilita el manteniment i millora la seguretat de l'aplicació.
Ací en tenim un exemple de construcció casera:

```php
<?php

namespace BatBook;

use PDO;

class QueryBuilder
{
    // Aquesta funció serveix per a construir i executar consultes SQL de tipus SELECT.
    // Es pot filtrar per valors, limitar la quantitat de resultats i establir un offset.
    public static function sql($class, $values=null, $limit = null, $offset = null)
    {
        // Obté el nom de la taula a partir de la propietat estàtica $nameTable de la classe passada com argument.
        $table = $class::$nameTable;
        
        // Obté una connexió a la base de dades.
        $conn = Connection::get();
        
        // Construeix la consulta SQL bàsica.
        $sql = "SELECT * FROM $table";
        
        // Afegeix condicions WHERE si es proporcionen valors per a filtrar.
        if ($values) {
            $sql .= " WHERE ";
            foreach (array_keys($values) as $key => $id) {
                if ($key != 0) {
                    $sql .= " AND $id=:$id";
                } else {
                    $sql .= "$id=:$id";
                }
            }
        }
        
        // Afegeix les clàusules LIMIT i OFFSET si són necessàries.
        if (isset($limit) && isset($offset)) {
            $sql .= " LIMIT $limit OFFSET $offset";
        }
        
        // Prepara la sentència SQL.
        $sentence = $conn->prepare($sql);
        
        // Enllaça els valors a la sentència.
        foreach ($values??[] as $key => $value) {
            $sentence->bindValue(":$key", $value);
        }
        
        // Estableix el mode de recuperació a objectes de la classe especificada.
        $sentence -> setFetchMode(PDO::FETCH_CLASS | PDO::FETCH_PROPS_LATE , $class);
        
        // Executa la consulta.
        $sentence -> execute();
        
        // Retorna tots els resultats obtinguts.
        return  $sentence->fetchAll();
    }

    // Aquesta funció serveix per a trobar una fila en una taula basant-se en el seu ID.
    public static function find($class, $id)
    {
        //TODO
    }

    // Aquesta funció serveix per a insertar una fila en una taula.
    public static function insert($class, $values)
    {
        $table = $class::$nameTable;
        $conn = Connection::get();
        $sql = "INSERT INTO $table (";
        foreach (array_keys($values) as $key => $id) {
            if ($key != 0) {
                $sql .= ','.$id;
            } else {
                $sql .= $id;
            }
        }
        $sql .= ") VALUES (";
        foreach (array_keys($values) as $key => $id) {
            if ($key != 0) {
                $sql .= ',:'.$id;
            } else {
                $sql .= ':'.$id;
            }
        }
        $sql .= ")";
        $sentence = $conn->prepare($sql);
        foreach ($values as $key => $value) {
            $sentence->bindValue(":$key", $value);
        }
        $sentence -> execute();
        return $conn->lastInsertId();
    }

    // Aquesta funció serveix per a actualitzar una fila en una taula.
    public static function update($class, $values, $id)
    {
        $table = $class::$nameTable;
        $conn = Connection::get();
        $sql = "UPDATE $table SET ";
        foreach (array_keys($values) as $key => $value) {
            if ($key != 0) {
                $sql .= ','.$value.'=:'.$value;
            } else {
                $sql .= $value.'=:'.$value;
            }
        }
        $sql .= " WHERE id=:id";
        $sentence = $conn->prepare($sql);
        foreach ($values as $key => $value) {
            $sentence->bindValue(":$key", $value);
        }
        $sentence->bindValue(":id", $id);  
        $sentence -> execute();
        return $id;
    }

    // Aquesta funció serveix per a eliminar una fila en una taula basant-se en el seu ID.
    public static function delete($class, $id)
    {
        //TODO
    }
}
```

En resum, aquesta classe proporciona funcions estàtiques per a la construcció i execució de consultes SQL bàsiques com SELECT, INSERT, UPDATE, i DELETE. Utilitza l'extensió PDO per a la connexió a bases de dades i la preparació de sentències SQL, la qual cosa ajuda a prevenir injeccions SQL. També permet la manipulació fàcil de files en bases de dades, tot retornant objectes de la classe especificada.

### Respotes d'error

Quan no trebem un recurs en al nostra web, podem mostrar a l'usuari una pàgina específica d'error utilitzant la funció header. Una típica seria:

```php
<!-- not-found.php -->
<?php http_response_code(404); ?>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>No trobat</title>
</head>
<body>
    <h1>404 - Pàgina no trobada</h1>
    <p>Ho sentim, la pàgina que estàs buscant no s'ha pogut trobar.</p>
    <a href="index.php">Torna a l'inici</a>
</body>
</html>
```

I per a utilitzar-la:

```php
<?php
header("Location: not-found.php");
exit;
?>

```

## 6. Accès a fitxers

Gràcies a la funció fopen() des de PHP podem obrir arxius que es troben en els nostres servidor o una URL.

A aquesta funció cal passar-li 2 paràmetres; el nom de l'arxiu que volem obrir i la manera en què s'obrirà

``` php
$fp = fopen("miarchivo.txt", "r");
```

Moltes vegades no podem obrir l'arxiu perquè aquest no es troba o no tenim accés a ell, per això és recomanable comprovar que podem fer-ho

``` php
if (!$fp = fopen("miarchivo.txt", "r")){
    echo "No se ha podido abrir el archivo";
}
```

### Maneres d'obertura de fitxers

- `r`: Manera lectura. Punter al principi de l'arxiu.
- `r+`: Obertura per a lectura i escriptura. Punter al principi de l'arxiu
- `w`: Obertura per a escriptura. Punter al principi de l'arxiu i el sobreescriu. Si no existeix s'intenta crear.
- `w+`: Obertura per a lectura i escriptura. Punter al principi de l'arxiu i el sobreescriu. Si no existeix s'intenta crear.
- `a`: Obertura per a escriptura. Punter al final de l'arxiu. Si no existeix s'intenta crear.
- `a+`: Obertura per a lectura i escriptura. Punter al final de l'arxiu. Si no existeix s'intenta crear.
- `x`: Creació i obertura per a només escriptura. Punter al principi de l'arxiu. Si l'arxiu ja existeix donarà error E_*WARNING. Si no existeix s'intenta crear.
- `x+`: Creació i obertura per a lectura i escriptura. Mateix comportament que x.
- `c`: Obertura per a escriptura. Si no existeix es crea. Si existeix no se sobreescriu ni dona cap error. Punter al principi de l'arxiu.
- `c+`: Obertura per a lectura i escriptura. Mateix comportament que C.
- `b`: Quan es treballa amb arxius binaris com *jpg, pdf, *png i altres. Se sol col·locar al final de la manera, és a dir *rb, r+b, x+b, *wb...

### Operacions amb arxius

Per a poder **llegir** un arxiu necessitem usar la funció *fread()* de *PHP*

```php
//  ▒▒▒▒▒▒▒▒ Abriendo un archivo y leyendo su contenido ▒▒▒▒▒▒▒▒

$file = "miarchivo.txt";
$fp = fopen($file, "r");

// filesize() nos devuelve el tamaño del archivo en cuestión
$contents = fread($fp, filesize($file));

// Cerramos la conexión con el archivo
fclose();
```

Si el que volem és **escriure** en un arxiu, haurem de fer ús de la funció *fwrite()*

```php
//  ▒▒▒▒▒▒▒▒ Escribiendo en un archivo ▒▒▒▒▒▒▒▒

$file = "miarchivo.txt";
$texto = "Hola que tal";

$fp = fopen($file, "w");

fwrite($fp, $texto);
fclose($fp);
```

### Informació d'un fitxer

Amb PHP i el seu mètode *stat()* podem obtindre informació sobre els arxius que li indiquem. Aquest mètode retorna fins a un total de 12 elements amb *informació* sobre el nostre arxiu.

0	*dev*	 número de dispositiu
1	*ino*	 número d'i-node
2	*mode*	 manera de protecció de l'i-node
3	*nlink*	 nombre d'enllaços
4	*uid*	 ID d'usuari del propietari
5	*gid*	 ID de grup del propietari
6	*rdev*	 tipus de dispositiu, si és un dispositiu i-node
7	*size*	 grandària en bytes
8	*atime*	 moment de l'últim accés (temps Unix)
9	*mtime*	 moment de l'última modificació (temps Unix)
10	*ctime*	 moment de l'última modificació de l'i-node (temps Unix)
11	*blksize*	 grandària del bloc E/S del sistema de fitxers
12	*blocks*	 nombre de blocs de 512 bytes assignats

Uns exemples...

``` php
<?php

//  ▒▒▒▒▒▒▒▒ Información del archivo ▒▒▒▒▒▒▒▒

$file = "miarchivo.txt";
$texto = "Todos somos muy ignorantes, lo que ocurre es que no todos ignoramos las mismas cosas.";

$fp = fopen($file, "w");
fwrite($fp, $texto);

$datos = stat($file);

echo $datos[3] . "<br>"; // Número de enlaces, 1
echo $datos[7] . "<br>"; // Tamaño en bytes, 85
echo $datos[8] . "<br>"; // Momento de último acceso, 1444138104
echo $datos[9] . "<br>"; // Momento de última modificación, 1444138251

?>
```

Dona una ullada a [les funcions de directoris](https://www.php.net/manual/es/book.dir.php) que té **PHP**, és molt interessant.

## 7. Web Scraping 

Consisteix a navegar a una pàgina web i extraure informació automàticament, a partir del codi HTML generat, i organitzar la informació pública disponible en Internet.
Aquesta pràctica requereix l'ús d'una llibreria que facilite la descàrrega de la informació desitjada imitant la interacció d'un navegador web. Aquest "robot" pot accedir a diverses pàgines simultàniament.

!!! question "¿És legal?"
    Si el lloc web indica que té el contingut protegit per drets d'autor o en les normes d'accés via usuari/contrasenya ens avisa de la seua prohibició, estaríem incorrent en un delicte.
    És recomanable estudiar l'arxiu `robots.txt` que es troba en l'arrel de cada lloc web.
    Més informació en l'article [El manual complet per al web scraping legal i ètic en 2021](https://ichi.pro/es/el-manual-completo-para-el-web-scraping-legal-y-etico-en-2021-69178542830388)

### Goutte

[Goutte](https://github.com/FriendsOfPHP/Goutte) és un senzill client HTTP per a PHP creat específicament per a fer web scraping. Ho va desenvolupar el mateix autor del framework *Symfony* i ofereix un API senzilla per a extraure dades de les respostes HTML/XML dels llocs web.

Els components principals que abstrau *Goutte* sobre *Symfony* són:

* `BrowserKit`: simula el comportament d'un navegador web.
* `CssSelector`: tradueix consultes CSS en consultes XPath.
* `DomCrawler`: facilita l'ús del DOM i XPath.

Per a poder utilitzar *Goutte* en el nostre projecte, executarem el següent comando en el terminal:

``` bash
composer require fabpot/goutte
```

### Goutte con selectores CSS

A continuació farem un exemple molt senzill utilitzant els selectors CSS, extraient informació de la web `https://books.toscrape.com/`, la qual és una pàgina per a proves que no rebutjarà les nostres peticions.

Després de crear un client amb *Goutte*, hem de realitzar un petició a una URL. Amb la resposta obtinguda, podem utilitzar el mètode `filter` per a indicar-li la ruta CSS que volem recórrer i iterar sobre els resultats mitjançant una funció anònima. Una vegada estem dins d'un determinat node, el mètode `text()` ens retornarà el contingut del propi node.

En concret, ficarem en un array associatiu el títol i el preu de tots els llibres de la categoria *Classics*.

``` php
<?php
require '../vendor/autoload.php';

$httpClient = new \Goutte\Client();
$response = $httpClient->request('GET', 'https://books.toscrape.com/catalogue/category/books/classics_6/index.html');
// colocamos los precios en un array
$precios = [];
$response->filter('.row li article div.product_price p.price_color')->each(
    // le pasamos $precios por referencia para poder editarla dentro del closure
    function ($node) use (&$precios) {
        $precios[] = $node->text();
    }
);

// colocamos el nombre y el precio en un array asociativo
$contadorPrecios = 0;
$libros = [];
$response->filter('.row li article h3 a')->each(
    function ($node) use ($precios, &$contadorPrecios, &$libros) {
        $libros[$node->text()] = $precios[$contadorPrecios];
        $contadorPrecios++;
    }
);
```

### Crawler

Un cas molt comú és obtindre la informació d'una pàgina que té els resultats paginados, de manera que anem recorrent els enllaços i accedint a cadascun dels resultats.

En aquest cas agafarem tots els preus dels llibres de fantasia, i els sumarem:

``` php
<?php
require '../vendor/autoload.php';

use Goutte\Client;
use Symfony\Component\HttpClient\HttpClient;

$client = new Client(HttpClient::create(['timeout' => 60]));
$crawler = $client->request('GET', 'https://books.toscrape.com/catalogue/category/books/fantasy_19/index.html');

$salir = false;

$precios = [];
while (!$salir) {
    $crawler->filter('.row li article div.product_price p.price_color')->each(
        function ($node) use (&$precios) {
            $texto = $node->text();
            $cantidad = substr($texto, 2); // Le quitamos las libras ¿2 posiciones?
            $precios[] = floatval($cantidad);
        }
    );

    $enlace = $crawler->selectLink('next');
    if ($enlace->count() != 0) {
        // el enlace next existe
        $sigPag = $crawler->selectLink('next')->link();
        $crawler = $client->click($sigPag); // hacemos click
    } else {
        // ya no hay enlace next
        $salir = true;
    }
}

$precioTotal = array_sum($precios);
echo $precioTotal;
```


## 8. Exercisis

### Bateria d'exercicis solucionats 
 
##### Exercici 1. Connexió bàsica

1. Crea un fitxer PHP que faça una connexió a una base de dades MySQL utilitzant PDO.

<details>
<summary>Solució</summary>

``` php
<?php
try {
    $dsn = 'mysql:host=db;dbname=pruebadb';
    $usuari = 'root';
    $contrasenya = '1234';
    $pdo = new PDO($dsn, $usuari, $contrasenya);
    echo "Connexió establerta!";
} catch (PDOException $e) {
    echo "Error de connexió: " . $e->getMessage();
}
 
```
</details>


##### Exercici 2. Inserir un registre

1. Escriu una funció que insereixi un nou usuari a la taula `users` amb el nom i correu electrònic passats per paràmetre.

<details>
<summary>Solució</summary>

``` php
function inserirUsuari($nom, $correu) {
    global $pdo;
    $sql = "INSERT INTO users (nom, correu) VALUES (:nom, :correu)";
    $stmt = $pdo->prepare($sql);
    $stmt->bindParam(':nom', $nom);
    $stmt->bindParam(':correu', $correu);
    $stmt->execute();
    echo "Usuari inserit!";
}
```

</details>

##### Exericici 3. Recuperar dades
 
1. Fes una consulta SQL que mostri tots els usuaris registrats a la taula `users` i mostra'ls en una taula HTML.

<details>
<summary>Solució</summary>

``` php
<?php
function mostrarUsuaris() {
    global $pdo;
    $sql = "SELECT * FROM users";
    $stmt = $pdo->query($sql);
    echo "<table>";
    while ($fila = $stmt->fetch(PDO::FETCH_ASSOC)) {
        echo "<tr><td>{$fila['nom']}</td><td>{$fila['correu']}</td></tr>";
    }
    echo "</table>";
}
```

</details>

##### Exercici 4. Actualitzar dades

1. Escriu una funció que actualitzi el correu electrònic d'un usuari segons el seu identificador (`id`).

<details>
<summary>Solució</summary>

``` php
<?php
function actualitzarCorreu($id, $nouCorreu) {
    global $pdo;
    $sql = "UPDATE users SET correu = :correu WHERE id = :id";
    $stmt = $pdo->prepare($sql);
    $stmt->execute([':correu' => $nouCorreu, ':id' => $id]);
    echo "Correu actualitzat!";
}
```

</details>

##### Exercici 5. Eliminar un registre

1. Implementa un script que esborri un usuari per identificador (`id`).

<details>
<summary>Solució</summary>

``` php
<?php
function eliminarUsuari($id) {
    global $pdo;
    $sql = "DELETE FROM users WHERE id = :id";
    $stmt = $pdo->prepare($sql);
    $stmt->execute([':id' => $id]);
    echo "Usuari eliminat!";
}
```
</details>

 

##### Exercici 6. Tractament d'errors

1. Modifica el codi anterior per gestionar els errors amb `try-catch` i mostrar missatges d'error clars.

<details>
<summary>Solució</summary>

``` php
<?php
 try {
    actualitzarCorreu(5, 'noucorreu@example.com');
} catch (PDOException $e) {
    echo "Error en actualitzar: " . $e->getMessage();
}
```
</details>

##### Exercici 7. Ús de Query Builder

1. Utilitza un Query Builder per fer consultes a la base de dades de manera més fàcil i segura sense escriure SQL explícitament.

<details>
<summary>Solució</summary>

``` php
<?php
#  Ús de Query Builder (amb Laravel com a exemple)
use Illuminate\Support\Facades\DB;

function obtenirUsuaris() {
    $usuaris = DB::table('users')->get();
    foreach ($usuaris as $usuari) {
        echo $usuari->nom . ' - ' . $usuari->correu . "<br>";
    }
}
```
</details>

##### Exercici 8. Tractament de fitxers

1. Crea un script que llegeixi un fitxer CSV i insereixi les dades en una taula de la base de dades.

<details>
<summary>Solució</summary>

``` php
<?php
 
function llegirCSV($fitxerCSV) {
    global $pdo;
    if (($gestor = fopen($fitxerCSV, "r")) !== FALSE) {
        while (($dades = fgetcsv($gestor, 1000, ",")) !== FALSE) {
            $sql = "INSERT INTO users (nom, correu) VALUES (:nom, :correu)";
            $stmt = $pdo->prepare($sql);
            $stmt->execute([':nom' => $dades[0], ':correu' => $dades[1]]);
        }
        fclose($gestor);
        echo "Dades inserides des del CSV!";
    }
}

```
</details>


##### Exercici 9. Web Scraping

1. Utilitza Goutte per a fer web scraping a la pàgina `https://books.toscrape.com/` i extreu el títol i preu de tots els llibres de la categoria `Classics`.
2. Mostra els resultats en una taula HTML.
3. Suma tots els preus i mostra el preu total.
4. Modifica el codi per a recórrer totes les pàgines de resultats.
  
<details>
<summary>Solució</summary>
    
``` php    
<?php
     require '../vendor/autoload.php';
     
     
     use Goutte\Client;
     use Symfony\Component\HttpClient\HttpClient;
     
     $client = new Client(HttpClient::create(['timeout' => 60]));
     $crawler = $client->request('GET', 'https://books.toscrape.com/catalogue/category/books/classics_6/index.html');
     
     $salir = false;
     
     $precios = [];
     while (!$salir) {
         $crawler->filter('.row li article div.product_price p.price_color')->each(
             function ($node) use (&$precios) {
                 $texto = $node->text();
                 $cantidad = substr($texto, 2); // Le quitamos las libras ¿2 posiciones?
                 $precios[] = floatval($cantidad);
             }
         );
     
         $enlace = $crawler->selectLink('next');
         if ($enlace->count() != 0) {
             // el enlace next existe
             $sigPag = $crawler->selectLink('next')->link();
             $crawler = $client->click($sigPag); // hacemos click
         } else {
             // ya no hay enlace next
             $salir = true;
         }
     }    
     
     $precioTotal = array_sum($precios);
     echo $precioTotal;
```

</details>
 
### Exercicis proposats

#### Exercici 1: Creació d'una base de dades

1. **Descripció:**
   Crea una base de dades amb una taula `empleats` que tinga els camps `id`, `nom`, `cognom` i `sou`.

2. **Requisits:**
    - Crear la base de dades i la taula.
    - Definir els tipus de dades adequats per als camps.

#### Exercici 2: Llistat d'empleats

1. **Descripció:**
   Crea un script PHP que mostre tots els empleats de la taula `empleats` en una taula HTML.

2. **Requisits:**
    - Connectar-se a la base de dades.
    - Recuperar els empleats i mostrar-los en una taula HTML.

#### Exercici 3: Formulari per a afegir empleats

1. **Descripció:**
   Afegeix un formulari HTML que permeta afegir nous empleats a la taula `empleats`.

2. **Requisits:**
    - Crear un formulari per a introduir el `nom`, `cognom` i `sou` de l'empleat.
    - Crear un script PHP per a gestionar la inserció de nous empleats en la taula.

#### Exercici 4: Formulari per a actualitzar el sou d'un empleat

1. **Descripció:**
   Afegeix un formulari per a modificar el sou d'un empleat existent.

2. **Requisits:**
    - Crear un formulari per a seleccionar l'empleat i introduir el nou sou.
    - Escriure un script PHP per a actualitzar el sou en la base de dades.

#### Exercici 5: Formulari per a eliminar un empleat

1. **Descripció:**
   Afegeix un formulari per a eliminar un empleat de la taula `empleats`.

2. **Requisits:**
    - Crear un formulari per a seleccionar l'empleat a eliminar.
    - Escriure un script PHP per a eliminar l'empleat de la base de dades.

#### Exercici 6: Creació de la classe `Empleat`

1. **Descripció:**
   Crea una classe `Empleat` en PHP amb els atributs `id`, `nom`, `cognom` i `sou` i utilitza-la per a representar els empleats.

2. **Requisits:**
    - Definir la classe `Empleat` amb els seus atributs.
    - Modificar els exercicis anteriors per a utilitzar aquesta classe en lloc de variables simples.

#### Exercici 7:Completa el Query Builder seleccionat 
1. **Descripció:**
   Completa el QueryBuilder seleccionat.

2. **Requisits:**
   - Implementar el Query Builder en les operacions de consulta,   i eliminació.


#### Exercici 8: Ús d'un Query Builder

1. **Descripció:**
   Modifica els exercicis anteriors per a utilitzar un Query Builder per a fer les consultes a la base de dades.

2. **Requisits:**
    - Implementar el Query Builder en les operacions de consulta, inserció, actualització i eliminació.

#### Exercici 9: Poblar la taula amb dades de webscraping

1. **Descripció:**
   Modifica l'exercici de webscraping per a poblar una taula de la base de dades amb els llibres de la categoria `Classics` de la pàgina `https://books.toscrape.com/`.

2. **Requisits:**
    - Realitzar el webscraping de la pàgina esmentada.
    - Inserir els llibres en una taula de la base de dades.

## 9. Enunciat dels projectes

### Projecte  "4 en Ratlla"

#### 1. Autenticació d'Usuaris i Gestió de Partides Guardades

1. **Registre d'Usuari:**
   - Crea un formulari de login perquè el usuaris s'hagen de validar .
   - Si l'usuari no està registrat es donarà d'alta automàticament i se li permetrà entrar.
   - Després de validar-se o registrar-se es mostrarà la pantalla de triar nom i color.
 
2. **Opcions noves** 

   - **Guardar Partida**: Es guardarà l'estat actual de la partida en la BBDD (només una per usuari, la darrera). Si guardem un altra substituirà a l'anterior. 
   - **Carregar Partida**: Es carregarà l'estat de la partida guardada per a l'usuari.
   - **Tancar sessió**: Afig una opció perquè l’usuari puga tancar sessió i finalitzar la seua sessió activa.
 
#### 3. Consideracions Addicionals

1. **Seguretat:**
   - Utilitza **hashing** de contrasenyes amb `password_hash()` per emmagatzemar-les de forma segura.
    

2. **Millores de la Interfície d'Usuari:**
   - Proporciona missatges clars d'error en cas de contrasenyes incorrectes o usuaris inexistents.
   - Implementa una navegació senzilla per iniciar una nova partida o continuar una partida guardada.

3. **Proves:**
   - Realitza proves per assegurar que l’autenticació d’usuaris funciona correctament.
   - Verifica que les partides es guarden i es recuperen adequadament.

---

### **Exemple d'Estructura de la Base de Dades:**

```sql
CREATE TABLE `partides` (
                           `usuari_id` int NOT NULL,
                           `game` text CHARACTER  
);
 
CREATE TABLE `usuaris` (
                          `id` int NOT NULL,
                          `nom_usuari` varchar(50) NOT NULL,
                          `contrasenya` varchar(255) NOT NULL
);
 
ALTER TABLE `partides`
   ADD PRIMARY KEY (`usuari_id`);
 
ALTER TABLE `usuaris`
   ADD PRIMARY KEY (`id`),
  ADD UNIQUE KEY `nom_usuari` (`nom_usuari`);
 
ALTER TABLE `usuaris`
   MODIFY `id` int NOT NULL AUTO_INCREMENT;
 
ALTER TABLE `partides`
   ADD CONSTRAINT `partides_ibfk_1` FOREIGN KEY (`usuari_id`) REFERENCES `usuaris` (`id`) ON DELETE CASCADE;
COMMIT;

```
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

 
