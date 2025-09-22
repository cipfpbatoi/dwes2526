# SA2. Programació web amb PHP

??? abstract "Duració i criteris d'avaluació"

Duració estimada: 30 hores

    <hr />

    | Resultat d'aprenentatge | Criteris d'avaluació|
    | -------                 | -------             |
    | 2. Escriu sentències executables per un servidor Web reconeixent i aplicant procediments d'integració del codi en llenguatges de marques. | a) S'han reconegut els mecanismes de generació de pàgines Web a partir de llenguatges de marques amb codi embegut. <br/> b) S'han identificat les principals tecnologies associades.  <br/> c) S'han utilitzat etiquetes per a la inclusió de codi en el llenguatge de marques.  <br/> d) S'ha reconegut la sintaxi del llenguatge de programació que s'ha d'utilitzar.  <br/> e) S'han escrit sentències simples i s'ha comprovat els seus efectes en el document resultant.  <br/> f) S'han utilitzat directives per a modificar el comportament predeterminat.  <br/> g) S'han utilitzat els diferents tipus de variables i operadors disponibles en el llenguatge.  <br/> h) S'han identificat els àmbits d'utilització de les variables.  <br/> |
    | 3. Genera pàgines web de forma dinàmica seguint especificacions rebudes. | a) S'han identificat els mecanismes de separació de la lògica de negoci.<br/>b) S'han utilitzat tecnologies adequades per a la generació dinàmica de pàgines web.<br/>c) S'han utilitzat tècniques d'accés a dades.<br/>d) S'han generat pàgines web dinàmiques que compleixen amb les especificacions rebudes.<br/>e) S'ha comprovat el funcionament de les pàgines web generades.<br/>f) S'han seguit les convencions de format i codificació establertes. |
    | 4. Desenvolupa aplicacions Web embegudes en llenguatges de marques analitzant i incorporant funcionalitats segons especificacions | a) S'han identificat els mecanismes disponibles per al manteniment de la informació que concerneix un client web concret i s'han assenyalat els seus avantatges.<br /> b) S'han utilitzat mecanismes per a mantindre l'estat de les aplicacions web.<br /> c) S'han utilitzat mecanismes per a emmagatzemar informació en el client web i per a recuperar el seu contingut.<br /> d) S'han identificat i caracteritzat els mecanismes disponibles per a l'autenticació d'usuaris.<br /> e) S'han escrit aplicacions que integren mecanismes d'autenticació d'usuaris.<br /> f) S'han utilitzat eines i entorns per a facilitar la programació, prova i depuració del codi. |
 
## SA2.1.Introducció a PHP

#### 🐘 Què és PHP?
**PHP** (Hypertext Preprocessor) és un llenguatge de programació de codi obert, especialment dissenyat per al desenvolupament web del costat del servidor. Es pot incrustar fàcilment en codi HTML, cosa que el fa una opció popular per crear aplicacions web dinàmiques i interactives. PHP s'utilitza per gestionar el contingut dinàmic, les bases de dades, el seguiment de sessions i fins i tot per crear aplicacions completes.

 
#### Importància en el desenvolupament web
PHP és un dels llenguatges més utilitzats en el desenvolupament web per diverses raons:

* **Facilitat d'aprenentatge:** PHP és relativament fàcil d'aprendre per als principiants en programació web. La seva sintaxi és senzilla i similar a altres llenguatges com C i Perl.
* **Gran comunitat i suport:** PHP té una gran comunitat de desenvolupadors que proporcionen suport, biblioteques, extensions i eines. A més, hi ha nombrosos recursos en línia, tutorials i documentació.
* **Integració amb bases de dades:** PHP es pot integrar fàcilment amb una àmplia varietat de bases de dades, cosa que el fa ideal per a aplicacions web basades en dades.
* **Flexibilitat i escalabilitat:** PHP és altament flexible i es pot utilitzar per desenvolupar tant aplicacions petites com projectes grans i complexos. També és escalable, cosa que permet gestionar un gran volum de trànsit.
* **Cost efectiu:** Com que és de codi obert, PHP és gratuït per utilitzar i distribuir. Això redueix els costos de desenvolupament per a les empreses i els desenvolupadors.

 
### 🌐 Llenguatges imbricats en HTML
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

### 🏷️ Etiquetes per a inserció de codi
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

### 🔢 Tipus de dades. Conversions entre tipus de dades
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

### 🛑 Constants
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

### 📦 Variables. Operadors.  Àmbits de les variables

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

- Local: dins d'una funció.
- Global: fora de qualsevol funció.
- Estàtic: persisteixen el seu valor entre crides a la funció.

 
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
 

### 🛠️ Funcions 

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


### ⚙️ Directives per a modificar el comportament predeterminat del codi

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
 
### 🔀 Mecanismes de decisió (if, match)
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

### 🔄 Bucles (for, while, foreach)

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

### 📚 Arrays

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

### 🗂️ Arrays associatius

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

### 📝 Com utilitzar les cometes en PHP

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

### 💬 Comentaris en el codi

Comentaris d'una línia:
```php
// Això és un comentari d'una línia
```
Comentaris de diverses línies:
```php
/* Això és un comentari
   de diverses línies */
```

### 🖥️ Variables de servidor

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

### 📋 Formularis

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


#### Validació

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

#### Parámetre multivalor

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

#### Tornant a emplenar un formulari

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

#### Pujant arxius

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
 
### 📖 Fonaments 

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

 
### 🍪 Cookies  

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

### 🔑 Sessions

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

### 📦➡️📄 Serialització en PHP

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

### 👤✔️ Autenticació d'usuaris

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

### 🐘 Introducció de la POO en php

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

### 📐 Principis de la POO

#### Encapsulació

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

 
### 🗺️ Espai de noms

#### 🧩 Espais de noms (Namespaces)

Els **espais de noms** serveixen per **organitzar les classes** i evitar conflictes. Funcionen com els paquets a Java.

##### Com es declaren

S’escriuen al principi del fitxer:

```php
<?php
namespace Dwes\Exemples;

class Producte {
  public $nom;

  public function mostra() {
    echo "Producte: " . $this->nom;
  }
}
```

##### Com s'utilitzen

Per a usar una classe d’un altre namespace:
 
``` php
require 'Dwes/Exemples/Producte.php';
use Dwes\Exemples\Producte;

$p = new Producte();

```
 
!!! tip "To `use` or not to `use`"
En resum, `use` permet accedir sense qualificar a recursos que estan en un altre *namespace*. Si estem en el mateix espai de nom, no necessitem `use`.

 
#### 📦 Composer i autoload

<figure style="float: right;">
    <img src="imagenes/05/logo-composer.png" width="200">
    <figcaption>Logo Composer</figcaption>
</figure>


Composer és una eina que:

* Instala paquets PHP (llibreries externes).
* Crea un fitxer autoload.php per carregar les classes automàticament.

 
##### Instal·lació

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

##### Actualitzar llibreries

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

##### `autoload.php`

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
### 📅 Gestió de dates i hores amb Carbon

#### Què és Carbon?

**Carbon** és una llibreria PHP que facilita el treball amb dates i hores. Està basada en l’extensió `DateTime` de PHP, però amb una sintaxi molt més senzilla i potent.

Es tracta d’una llibreria molt utilitzada en aplicacions modernes per formatar, manipular i calcular temps.

#### Instal·lació amb Composer

Per a utilitzar Carbon en el nostre projecte, cal primer instal·lar-lo mitjançant Composer:

```bash
composer require nesbot/carbon
```
Una vegada instal·lat, ja la podem carregar automàticament amb l’autoloader de Composer.

#### Exemple bàsic

```php
$data = Carbon::now();

echo $data->format('d/m/Y H:i'); // 05/08/2025 11:45
echo $data->locale('ca')->isoFormat('dddd, D [de] MMMM [de] YYYY'); // dilluns, 5 de agost de 2025
```

#### Operaciò amb dates

```php
$ahir = Carbon::yesterday();
$demà = Carbon::tomorrow();
$unaSetmanaDesprés = Carbon::now()->addWeek();
$fa3Dies = Carbon::now()->subDays(3);

echo "Ahir era: " . $ahir;
echo "Demà serà: " . $demà;
```
#### Comparaciò de dates

```php
$data1 = Carbon::parse('2025-08-05');
$data2 = Carbon::parse('2025-09-01');

if ($data1->lt($data2)) {
echo "$data1 és anterior a $data2";
}
```


### 🚫 Gestió d'Exempcions


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

### 📜 Logger amb Monolog

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

 
!!! tip "Més informació"
Més informació sobre manejadores, formateadores i processadors en <https://github.com/Seldaek/monolog/blob/master/doc/02-handlers-formatters-processors.md>




## 📎 Annex:  Accés a fitxers

### 📄 Funcions bàsiques de PHP per a fitxers

| Funció     | Descripció                                       |
|------------|--------------------------------------------------|
| `fopen()`  | Obri un fitxer.                                 |
| `fread()`  | Llig el contingut d’un fitxer.                  |
| `fwrite()` | Escriu dades en un fitxer.                      |
| `fclose()` | Tanca un fitxer obert.                          |
| `file_exists()` | Comprova si un fitxer existix.            |
| `unlink()` | Elimina un fitxer.                              |

### 🔓 Modes d'obertura de fitxers

| Mode | Descripció                                                  |
|------|-------------------------------------------------------------|
| `r`  | Llig només. El punter es col·loca al principi del fitxer.   |
| `w`  | Escriure només. Es crea o truncat si ja existix.            |
| `a`  | Afegeix al final del fitxer. El crea si no existix.         |
| `r+` | Llig i escriu. No crea el fitxer si no existix.             |
| `w+` | Llig i escriu. Trunca el fitxer o el crea de nou.           |
| `a+` | Llig i escriu. Afegeix al final si el fitxer existix.       |

#### Exemple bàsic

```php
<?php
$fitxer = fopen("dades.txt", "w");
fwrite($fitxer, "Hola món!");
fclose($fitxer);
?>
```

Aquest codi crea (o substitueix) un fitxer anomenat dades.txt i escriu el text "Hola món!" dins d'ell.

#### Consideracions de seguretat

- Comprova sempre si el fitxer existix abans de llegir o escriure.
- Utilitza rutes relatives i evita permetre a l’usuari introduir noms de fitxer directament.
- Gestiona correctament els errors amb file_exists(), is_readable(), is_writable().

###  📄 Llegir fitxer línia a línia

```php
<?php
$fitxer = fopen("dades.txt", "r");

while (!feof($fitxer)) {
    $linia = fgets($fitxer);
    echo $linia . "<br>";
}

fclose($fitxer);
 
```


La funció fgets() llig una línia de text. La funció feof() comprova si s’ha arribat al final del fitxer.

### ✍️ Escriure múltiples línies

```php
<?php
$fitxer = fopen("registre.log", "a");
$linies = ["Primera línia", "Segona línia", "Tercera línia"];

foreach ($linies as $linia) {
    fwrite($fitxer, $linia . PHP_EOL);
}

fclose($fitxer);
?>
``` 
PHP_EOL assegura que el salt de línia siga compatible amb el sistema operatiu.

### 📁 Gestió de directoris

#### Crear un directori

```php
<?php
if (!is_dir("documents")) {
    mkdir("documents", 0755);
}
?>
``` 

mkdir() crea un directori amb els permisos indicats. is_dir() comprova si ja existix.

#### Llistar el contingut d’un directori

```php
<?php
$directori = opendir("documents");

while (($fitxer = readdir($directori)) !== false) {
    if ($fitxer != "." && $fitxer != "..") {
        echo $fitxer . "<br>";
    }
}

closedir($directori);
 
``` 

#### Eliminar fitxers i directoris

```php
<?php
if (file_exists("documents/antiga.txt")) {
    unlink("documents/antiga.txt");
}

if (is_dir("documents/buid")) {
    rmdir("documents/buid");
}
?>
``` 
 
##  Exercicis 

### 🧩 Bateria d'Exercicis Solucionats per a la Unitat de PHP

Hi ha un repositori preparat amb les [solucions](https://github.com/Curs-2025-26/SA2.Exemples).
 
#### Enunciat dels exercicis
 
Escriu els següent programes: 

##### 1. 'Hola món' 
     
* Declare una variable amb el teu nom.
* Mostre en pantalla un missatge com ara:  “Hola, món! , Ignasi” dins d’una etiqueta HTML  utilitzant echo.
   
  Pots combinar text i variables utilitzant el signe de concatenació (.).

##### 2. 'Variables' 

* Declare una variable $a amb el valor numèric 5.
* Declare una altra variable $b amb el valor "10" (cadena).
* Mostre per pantalla el resultat de sumar $a + $b dins d’una frase com: “Suma: 15”, utilitzant echo.

  Observa com PHP converteix automàticament el valor de la cadena "10" a nombre.

##### 3. 'Cometes simples vs dobles'

* Declare una variable $name amb el teu nom.
* Mostre dues frases amb echo:
    * Una utilitzant cometes dobles, on s’imprimisca el contingut de la variable.
    * Una altra utilitzant cometes simples, on s’imprimisca literalment $name.

    Ex.:
    Hola, Ignasi!
    Hola, $name!

##### 4. 'Condicional bàsic'

* Crea una variable `$edat` amb un valor numèric.
* Utilitza una estructura condicional `if` per:
    * Mostrar un missatge si l’edat és negativa: `"Edat invàlida"`.
    * Si és igual o major de 18, mostrar `"Ets major d'edat"`.
    * Si no, mostrar `"Ets menor d'edat"`.


##### 5. 'Arrays i bucles'

* Crea un array anomenat `$fruites` amb tres valors inicials: `"poma"`, `"plàtan"` i `"maduixa"`.
* Mostra per pantalla el primer element de l’array.
* Afegeix un nou element `"taronja"` a l’array.
* Recorre l’array complet amb un bucle `foreach` i mostra cada fruita en una línia separada.


##### 6. 'Estructures `match`'

* Declara una variable `$nota` amb un valor entre 0 i 10.
* Utilitza l’estructura `match (true)` per assignar un resultat segons el valor:
    * `10` → `"Excel·lent"`
    * Entre `8` i `9` → `"Molt bé"`
    * Entre `5` i `7` → `"Bé"`
    * Per defecte → `"Insuficient"`
* Mostra el resultat per pantalla.

* Declara una variable `$producte` amb algun dels següents valors: `"pa"`, `"llet"`, `"formatge"`.
* Usa un altre `match` per assignar un preu a cada producte.
* Mostra per pantalla el missatge: `"El preu de formatge és 2.5 euros."`

##### 7. 'Informació del servidor amb `$_SERVER`'

* Crea una pàgina HTML amb títol "Informació del Servidor".
* Mostra diferents dades utilitzant l’array especial `$_SERVER`:
    * Nom del servidor (`SERVER_NAME`)
    * Adreça IP del servidor (`SERVER_ADDR`)
    * Software del servidor (`SERVER_SOFTWARE`)
    * Agent d'usuari del client (`HTTP_USER_AGENT`)
    * Mètode de la sol·licitud (`REQUEST_METHOD`)
    * URL de la sol·licitud (`REQUEST_URI`)
    * Referent de la pàgina (`HTTP_REFERER`)
    * Protocol utilitzat (`SERVER_PROTOCOL`)
    * Port utilitzat (`SERVER_PORT`)
* Assegura't de controlar si alguna clau no està disponible, com per exemple el `HTTP_REFERER`.


##### 8. 'Formulari de contacte amb validació'

* Crea una pàgina HTML amb un formulari que demane:
    * Una adreça de correu electrònic (`email`)
    * Un missatge (`textarea`)
* El formulari s’ha d’enviar mitjançant el mètode POST i validar:
    * Que el camp `email` conté una adreça vàlida (`FILTER_VALIDATE_EMAIL`)
    * Que els camps no estiguen buits (usa `required` en HTML i valida amb PHP)
* Mostra un missatge de confirmació si tot és correcte, o d’error si el correu no és vàlid.
* Assegura’t de protegir el contingut rebut amb `htmlspecialchars()` per evitar problemes de seguretat.

##### 9. 'Formulari amb validació i missatges d’error'

* Crea un formulari que demane:
    * El nom de l’usuari (`input text`)
    * El correu electrònic (`input text`)
* Afegeix validació en PHP perquè:
    * Cap dels camps estiga buit
    * El correu siga vàlid (`FILTER_VALIDATE_EMAIL`)
* Mostra missatges d’error en cas de validació incorrecta (en color roig).
* Si les dades són correctes, mostra-les en pantalla.
* Assegura’t de:
    * Utilitzar `htmlspecialchars()` i `trim()` per netejar les entrades
    * Mantenir les dades escrites en el formulari si hi ha errors (**sticky form**)
##### 10. 'Pujar fitxer i seleccionar opció'

* Crea un formulari que permeta:
    * Pujar un fitxer (input `file`)
    * Seleccionar una opció d’entre diverses (checkbox)
* El formulari ha de validar:
    * Que el fitxer ha estat pujat correctament
    * Que almenys una opció ha estat seleccionada
* Mostra per pantalla:
    * Nom, tipus, mida i ubicació del fitxer
    * L’opció seleccionada pel usuari
* El fitxer pujat s’ha de moure a una carpeta anomenada `uploads/` dins del projecte.
* Utilitza `move_uploaded_file()` per traslladar-lo de la ubicació temporal a la definitiva.

##### 11. 'Comptador de visites amb sessió'

* Crea un script que utilitze sessions per comptar quantes vegades un usuari ha visitat la pàgina.
    * Si és la primera vegada, mostra `"Has visitat esta pàgina 1 vegada."`
    * Si ja ha visitat abans, incrementa el comptador i mostra el nombre de visites.
* Afegeix un botó que permeta **reiniciar** el comptador. En fer clic:
    * S’ha de destruir la sessió
    * Redirigir a la mateixa pàgina per tornar a començar

##### 12. 'Cistella de la compra (I): Afegir productes'

* Crea una pàgina amb un formulari on es puga introduir el nom d’un producte.
* Quan s’envia el formulari:
    * Guarda el producte dins d’una variable de sessió anomenada `$_SESSION["cistella"]`
    * Redirigeix l’usuari a una pàgina anomenada `02_cistella_veure.php`
* Inclou un enllaç que permeta accedir a la pàgina de visualització de la cistella.

##### 13. 'Cistella de la compra (II): Veure i buidar'

* Crea una pàgina que mostre els productes emmagatzemats en la variable de sessió `$_SESSION["cistella"]`.
    * Si no hi ha cap producte, mostra un missatge indicant-ho.
    * Si n’hi ha, mostra’ls en una llista.
* Inclou un botó per buidar la cistella:
    * Si es prem, elimina `$_SESSION["cistella"]`
    * Redirigeix a la mateixa pàgina per actualitzar el contingut

##### 14. 'Sistema bàsic d’autenticació amb sessió'

* Crea un formulari de login amb els camps:
    * Usuari (`usuari`)
    * Contrasenya (`clau`)
* Valida els camps amb valors fixos, per exemple:
    * Usuari: `admin`
    * Clau: `1234`
* Si les dades són correctes:
    * Guarda l’estat de login a la sessió (`$_SESSION["login"]`)
    * Guarda també el nom de l’usuari
    * Redirigeix a la mateixa pàgina
* Si són incorrectes, mostra un missatge d’error.
* Si l’usuari està identificat:
    * Mostra un missatge de benvinguda amb el nom d’usuari
    * Mostra un enllaç per a tancar sessió, que destruïsca la sessió i redirigisca

##### 15. 'Recordar nom amb cookies'

* Crea una pàgina amb un formulari que demane el nom de l’usuari.
* Quan s’envie el formulari:
    * Guarda el nom en una cookie amb duració d’1 hora.
    * Redirigeix a la mateixa pàgina.
* Quan es carregue la pàgina:
    * Si existeix la cookie, mostra un missatge de benvinguda amb el nom.
    * Mostra el valor de la cookie com a valor per defecte en l’input (`sticky form`).

##### 16. 'Preferència de tema amb cookies'

* Crea una pàgina que permeta a l’usuari seleccionar entre dos temes: `"clar"` i `"fosc"`.
* Quan l’usuari selecciona un tema, guarda la selecció en una cookie amb duració d’1 dia.
* Aplica l’estil CSS corresponent segons el valor de la cookie:
    * Tema `"clar"`: fons blanc, text negre.
    * Tema `"fosc"`: fons fosc, text clar.
* Redirigeix automàticament després de canviar el tema per aplicar-lo.

##### 17. 'Gestió de productes amb fitxer CSV'

* Crea un formulari que permeta afegir productes amb:
    * Nom del producte (`text`)
    * Preu (`number`)
* Quan s’envie el formulari:
    * Guarda les dades en un fitxer `productes.csv` en format CSV.
    * Mostra un missatge si s’ha afegit correctament o si falta algun camp.
* Mostra una taula amb tots els productes emmagatzemats al fitxer:
    * Llig el fitxer `productes.csv`
    * Mostra una taula amb les columnes: `Nom` i `Preu (€)`

##### 18. 'Classe `Usuari` i mètodes'

* Crea una classe anomenada `Usuari` amb atributs privats:
    * `$nom`, `$email`  
* Afegeix un constructor que inicialitze `$nom`, `$email` .
* Afegeix els mètodes públics següents:
    * `saluda()`: retorna un missatge com: `"Hola, sóc Ignasi i el meu email és ignasi@example.com"`
    
* Prova la classe creant una instància i cridant als mètodes `saluda()` i `validar()`.

##### 19. 'Instanciació i ús d’una classe'

* Inclou el fitxer `Usuari.php` on es defineix la classe `Usuari`.
* Crea una instància de la classe amb nom `"Pau"` i email `"pau@example.com"`.
* Mostra el resultat del mètode `saluda()` per pantalla.
* Assegura’t que has utilitzat `require_once` per incloure la definició de la classe.

##### 20. 'Classe `Producte` amb constructor i mètode'

* Crea una classe anomenada `Producte` amb dos atributs públics:
    * `$nom` i `$preu`
* Afegeix un constructor per inicialitzar els atributs.
* Afegeix un mètode públic `mostrar()` que retorne una cadena amb el format:
    * `"Nom - Preu€"` (per exemple: `"Formatge - 2.5€"`)
* Crea una instància de `Producte` i mostra el resultat del mètode `mostrar()`.

##### 21. 'Ús d’una classe amb `try-catch`'

* Inclou el fitxer `Producte.php` on es defineix la classe `Producte`.
* Crea una instància amb els valors `"Portàtil"` i `799.99`.
* Mostra el resultat del mètode `mostrar()` per pantalla.
* Encapsula la creació i ús de l’objecte dins d’un bloc `try-catch`.
    * En cas d’error, mostra el missatge capturat amb `getMessage()`.

##### 22. 'Login amb sessió i classe `Usuari`'

* Afegeix a la classe `Usuari` la propietat $clau (modifica el constructor) i els mètodes:
    * `validar($usuari, $clau)`
    * `getNom()`
* Crea un script de login que:
    * Cree un objecte `Usuari` amb valors fixos (p. ex. `"admin"`, `"1234"`)
    * Valide les dades del formulari POST utilitzant el mètode `validar()`
    * Si les dades són correctes, guarde l’estat en `$_SESSION` i redirigisca
    * Si no, mostre un error
* Mostra un formulari si l’usuari no està loguejat i un missatge de benvinguda si ho està.
* Afig un enllaç per tancar sessió que:
    * Elimine la sessió
    * Redirigisca a la mateixa pàgina

##### 23. 'Classe amb namespace personalitzat'

* Crea una classe anomenada `Salutador` dins del namespace `App`.
* Afegeix un mètode públic `diu($nom)` que retorne `"Hola, $nom!"`
* Desa la classe dins d’un fitxer adequat, seguint l’estructura de carpetes segons PSR-4.
* Prova la classe des d’un fitxer a part utilitzant:
    * `require 'vendor/autoload.php';`
    * `use App\Salutador;`

##### 24. 'Ús de classe amb autoload i `use`'

* Crea un fitxer `index.php` dins d’una carpeta `public/`.
* Assegura’t que utilitza l’autoload generat per Composer:
    * `require __DIR__ . '/../vendor/autoload.php';`
* Importa la classe `Salutador` mitjançant `use App\Salutador`.
* Crea una instància i crida al mètode `diu("Anna")` per mostrar el missatge.
 

### 🎯 Projecte "El penjat"
 
#### Repositori

[Grup A](https://classroom.github.com/a/DtM86hTQ)

#### Entrega 1 

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


| Criteri                                    | Puntuació Total | Complet(2)                          | Incomplet(1)                  | Insuficient(0)                     |
|--------------------------------------------|-----------------|-------------------------------------|-------------------------------|------------------------------------|
| **Inicialització de les variables** (2.dg) | 2               | Paraula i Array creat correctament  | Creats però amb errors        | No s'ha creat l'array              |
| **Funció per a Comprovar Intents** (2.fe)  | 3               | Funció creada i funcional           | Funció creada però amb errors | No s'ha creat la funció            |
| **Comprovació d'Intents**   (2.eh)         | 3               | Comprovació realitzada correctament | Comprovació amb errors        | No s'ha realitzat la comprovació   |
| **Estil CSS**               (2c)           | 1               | CSS aplicat correctament            | CSS aplicat però amb errors   | No s'ha aplicat el CSS             |
| **Comentaris i Claredat del Codi**  (2ah)  | 1               | Codi ben comentat i clar            | Codi amb alguns comentaris    | Codi sense comentaris o desordenat |


#### Entrega 2  

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


| Criteri                            | Puntuació Total | Complet (2)                                                | Incomplet (1)                                           | Insuficient (0)                                   |
|------------------------------------|-----------------|------------------------------------------------------------|---------------------------------------------------------|---------------------------------------------------|
| **Funcionalitat del Joc** (4f)     | 2               | El joc està completament funcional i sense errors.         | El joc és funcional, però conté errors significatius.   | El joc no és funcional o està incomplet.          |
| **Ús de Sessions**         (4b)    | 1               | Sessions ben implementades per a mantenir l'estat del joc. | Sessions utilitzades, però amb deficiències importants. | No s'han utilitzat sessions o són incorrectes.    |
| **Ús de Cookies**       (4c)       | 1               | Cookies ben utilitzades per a recordar els jugadors.       | Cookies utilitzades amb limitacions evidents.           | No s'han utilitzat cookies o són incorrectes.     |
| **Autenticació d'Usuaris**   (4de) | 3               | Autenticació segura i efectiva implementada.               | Autenticació present però amb deficiències notables.    | No s'ha implementat autenticació o és incorrecta. |
| **Interfície d'Usuari** (3f)       | 1               | Interfície atractiva i fàcil d'utilitzar.                  | Interfície funcional però poc intuïtiva.                | Interfície confusa i difícil d'utilitzar.         |
| **Punts addicionals**    (4ef)     | 2               | 1 punt per cadascúna aconseguida.                          | 

#### Entrega 3 

1. **Desenvolupar una versió modular i escalable del joc "L'Ofegat" emprant programació orientada a objectes (POO) i gestió de dependències amb Composer**
    -Organitza el projecte de manera clara utilitzant namespaces i Composer (autoload PSR-4):

    
    ofegat-poo/
    ├── composer.json
    ├── vendor/
    ├── app/
    │ ├── Joc.php
    │ ├── Jugador.php
    │ └── GestorPartida.php
    ├── public/
    │ ├── index.php
    │ ├── login.php
    │ ├── logout.php
    │ └── reiniciar.php
    ├── config/
    │ └── paraules.php
    ├── templates/
    │ ├── capçalera.php
    │ ├── peu.php
    │ └── joc.php
    ├── style.css

2. **Classes**

- **Joc**
    - Emmagatzema la paraula a endevinar, intents restants i lletres encertades/error.
    - Mètodes per comprovar lletres, mostrar estat del joc i saber si ha acabat.

- **Jugador**
    - Gestió del nom d’usuari (amb cookie si s'ha marcat "recordar").
    - Control de sessió.

- **GestorPartida**
    - Inicia, reinicia i manté l'estat del joc en sessió.
    - Crida els mètodes corresponents de `Joc` i `Jugador`.

3. **Altres** 
  
- Ús de Composer per a autoload.
  - `index.php` mostrarà el joc actual.
  - `login.php` per accedir amb nom d’usuari.
  - `reiniciar.php` per reiniciar la partida.
  - `logout.php` per tancar sessió i esborrar cookies.

- Crea un fitxer de paraules i utilitza'l per fer que cada vegada s'haja d'endivinar una

4. **Extres**

- Afegir dibuix d'ofegat (ASCII o imatge) segons el nombre d'errades.
- Multijugador amb base de dades.
- Guardar puntuacions.

 
| **Criteri**                             | **Punts** | **Complet (2)**                                                                    | **Incomplet (1)**                                                     | **Insuficient (0)**                                       |
|-----------------------------------------|-----------|------------------------------------------------------------------------------------|-----------------------------------------------------------------------|-----------------------------------------------------------|
| **Funcionament correcte del joc** (3de) | 2         | El joc és completament funcional i sense errors.                                   | El joc és funcional però amb errors o limitacions notables.           | El joc no funciona o està incomplet.                      |
| **Ús correcte de POO**    (3af)         | 2         | Classes ben estructurades, encapsulament correcte, ús de mètodes i atributs clars. | S’usen classes però amb estructura poc clara o pràctiques deficients. | No s’aplica orientació a objectes o de manera incorrecta. |
| **Autoload amb Composer**      (3b)     | 1         | Composer ben configurat i autoload funcional amb PSR-4.                            | Composer usat però amb problemes o mala configuració.                 | No s’ha utilitzat Composer o l’autoload no funciona.      |
| **Utilització del fitxer**      (4f)    | 2         | Lectura del fitxer i random de paraules amb funcions o poo                         | Lectura del fitxer poc funcional o escalable                          | No s’han implementat o no funciona correctament.          |
| **Extres**                      (4f)    | 2         | Tots els extres implementats                                                       | Algun extra implementat                                               | No s'han implementat                                      |
| **Bon ús del codi i organització** (3f) | 1         | Codi ben estructurat, clar i fàcil de seguir.                                      | Codi funcional però desorganitzat o poc llegible.                     | Codi desordenat i difícil de mantenir.                    |

**Puntuació màxima total: 10 punts**
 
### 📝 Exercicis proposats

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

#### Exercici 10: Sistema de Carret de Compres sense Base de Dades

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


#### Exercici 11: Autenticació Bàsica d'Usuaris amb Sessions

1. **Descripció:**

   Crea una aplicació PHP que permeta als usuaris iniciar sessió mitjançant un formulari. Utilitza sessions per a mantindre l'estat d'autenticació de l'usuari i mostrar missatges personalitzats basats en aquest estat.

2. **Requisits:**
    - Crear un formulari d'inici de sessió que sol·licite el nom d'usuari i la contrasenya.
    - Emmagatzemar l'estat d'autenticació en una sessió després de verificar les credencials.
    - Mostrar una pàgina de benvinguda personalitzada per a l'usuari autenticat.
    - Proporcionar un enllaç per a tancar sessió i destruir la sessió.

#### Exercici 12: Recordatori d'Usuari amb Cookies

1. **Descripció:**

   Afig una funcionalitat de "recordar-me" a l'exercici anterior que emmagatzeme el nom d'usuari en una cookie i permeta a l'usuari ser recordat en futures visites al lloc web.

2. **Requisits:**
    - Afig una opció de "recordar-me" al formulari d'inici de sessió.
    - Emmagatzemar el nom d'usuari en una cookie quan l'opció és seleccionada.
    - Comprovar la cookie en futures visites i iniciar sessió automàticament si la cookie existeix.
    - Assegurar que les cookies es configuren amb atributs de seguretat adequats (`HttpOnly`, `Secure`, `SameSite`).

#### Exercici 13: Formulari de Contacte amb Protecció CSRF

1. **Descripció:**

   Desenvolupa un formulari de contacte que permeta als usuaris enviar missatges i implementa protecció CSRF per a assegurar que les sol·licituds siguen legítimes.

2. **Requisits:**
    - Crear un formulari de contacte amb camps per al nom, correu electrònic i missatge.
    - Generar i emmagatzemar un token CSRF en una sessió quan es carrega el formulari.
    - Incloure el token CSRF com a camp ocult en el formulari.
    - Verificar el token CSRF quan s'envia el formulari i mostrar un missatge de confirmació si és vàlid.
    - Mostrar un missatge d'error si el token CSRF no és vàlid o no existeix.

#### Exercici 14: Seguiment d'Activitat de l'Usuari amb Sessions

1. **Descripció:**

   Crea un sistema que registre les pàgines visitades per l'usuari durant una sessió i mostre aquesta informació quan l'usuari visita una pàgina d'activitat.

2. **Requisits:**
    - Emmagatzemar una llista de pàgines visitades per l'usuari en una sessió.
    - Actualitzar la llista de pàgines cada vegada que l'usuari visite una nova pàgina.
    - Crear una pàgina que mostre l'historial de pàgines visitades durant la sessió actual.
    - Assegurar que l'historial es restableix quan l'usuari tanca la sessió.

#### Exercici 15. Creació de la Classe Bàsica i Gestió de Propietats

* Crea una classe `Persona` amb les propietats privades `nom`, `cognoms`, i `edat`. Encapsula aquestes propietats mitjançant getters i setters. Afig els següents mètodes:

      - `getNomComplet(): string` – Retorna el nom complet de la persona.
      - `estaJubilat(): bool` – Retorna `true` si l'edat és major o igual a 65, `false` en cas contrari.

* Modifica la classe `Persona` afegint un constructor que assigna nom i cognoms. Si es proporciona un tercer paràmetre, assigna l'edat; en cas contrari, assigna una edat per defecte de 25 anys.

* Modifica la classe `Persona` per utilitzar una constant `LIMITE_EDAT` amb el valor de 66 anys i utilitza-la en el mètode `estaJubilat`.

#### Exercici 16. Herència i Polimorfisme

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

#### Exercici 17. Integració d'Espais de Noms, Autoloading, i Composer

* Crea una classe `Empresa` que incloga una propietat amb un array de `Empleados` . Implementa:

    - `public function addWorker(Empleado $t)`
    - `public function listWorkersHtml(): string` – Genera la llista de treballadors en format HTML.
    - `public function getCosteNominas(): float` – Calcula el cost total de les nòmines.

* Configura el projecte PHP amb Composer que utilitze l'autoloading PSR-4.

#### Exercici 18. Logger  

* Utilitza la llibreria `Monolog` per configurar un logger que escriga missatges a un fitxer `app.log`. Afig funcionalitat perquè el logger registre missatges d'informació i d'error en diferents arxius segons la gravetat.

* Configura un logger que escriga missatges de registre tant a un fitxer com a la consola. Prova el logger registrant missatges d'error i advertència.

 
#### Exercici 19. Generació de PDFs amb DomPDF

* Instal·la la llibreria `dompdf/dompdf` amb Composer. Crea un script PHP que genere un PDF senzill amb un títol i un paràgraf de text.

* Crea un PDF utilitzant DomPDF que incloga una taula amb dades i una imatge. Assegura't que el PDF es renderitze correctament i que la imatge s'incloga en el document.

* Utilitzant la classe `Empresa` i `Empleado`, genera un informe en PDF amb la llista de treballadors i el seu sou. Utilitza DomPDF per generar aquest informe.

#### [Solucions](10solucions.html )

### ✅ Autoavaluació 

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

#### Exercici 8: Funcions de les Cookies

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

#### Exercici 9: Seguretat de les Cookies

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

#### Exercici 10: Creació de Sessions en PHP

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

#### Exercici 11: Manteniment d'Informació en Sessions

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

#### Exercici 12: Funcions de PHP per a Sessions

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

#### Exercici 13: Avantatges de les Sessions

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

#### Exercici 14: Autenticació d'Usuaris

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

#### Exercici 15: Constructors en PHP

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

#### Exercici 16: Herència en PHP

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

#### Exercici 17: Polimorfisme

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

#### Exercici 18: Espais de Noms

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

 

#### Exercici 19: Excepcions en PHP

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

#### Exercici 20: Autoloading en PHP

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

