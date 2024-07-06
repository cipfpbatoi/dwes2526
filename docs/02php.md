# El llenguatge PHP

??? abstract "Duració i criteris d'avaluació"

    Duració estimada: 10 hores

    <hr />

    | Resultat d'aprenentatge | Criteris d'avaluació|
    | -------                 | -------             |
    | 2. Escriu sentències executables per un servidor Web reconeixent i aplicant procediments d'integració del codi en llenguatges de marques. | a) S'han reconegut els mecanismes de generació de pàgines Web a partir de llenguatges de marques amb codi embegut. <br/> b) S'han identificat les principals tecnologies associades.  <br/> c) S'han utilitzat etiquetes per a la inclusió de codi en el llenguatge de marques.  <br/> d) S'ha reconegut la sintaxi del llenguatge de programació que s'ha d'utilitzar.  <br/> e) S'han escrit sentències simples i s'ha comprovat els seus efectes en el document resultant.  <br/> f) S'han utilitzat directives per a modificar el comportament predeterminat.  <br/> g) S'han utilitzat els diferents tipus de variables i operadors disponibles en el llenguatge.  <br/> h) S'han identificat els àmbits d'utilització de les variables.  <br/> |



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

=== "Enunciat"

Crear un fitxer PHP que mostre Hola, món! en un navegador web.

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
=== "Comentari" 

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

## 6. Variables. Operadors. Àmbits d'utilització

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

Àmbits d'utilització:
- **Local:** dins d'una funció.
- **Global:** fora de qualsevol funció.
- **Estàtic:** persisteixen el seu valor entre crides a la funció.
```php
function exemple() {
    global $variable_global;
    static $compte = 0;
    $compte++;
    echo $compte;
}
```

## 7. Directives per a modificar el comportament predeterminat del codi
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

## 8. Sentències simples en PHP i els seus efectes
Eco i print:
```php
echo "Hola, món!";
print "Hola, món!";
```
Variables i operacions:
```php
$a = 5;
$b = 10;
$suma = $a + $b;
echo $suma; // Mostra 15
```
Exemple:
```php
$nom = "Joan";
echo "Benvingut, " . $nom;
```

## 9. Àmbits de les variables (local, global, estàtic)
Local: dins d'una funció.
Global: fora de qualsevol funció.
Estàtic: persisteixen el seu valor entre crides a la funció.
```php
function exemple() {
    static $compte = 0;
    $compte++;
    echo $compte;
}
```
Exemple:
```php
function contar() {
    static $vegades = 0;
    $vegades++;
    echo $vegades;
}
contar(); // Mostra 1
contar(); // Mostra 2
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

** Diferències amb switch**
1. **Comparació estricta**: `match` utilitza comparació estricta (===) per comparar els valors.
2. **Retorna un valor**: `match` és una expressió, la qual cosa significa que retorna un valor.
3. **No necessita break**: A diferència de `switch`, no es necessita l'ús de `break` per evitar la caiguda (fall-through).
4. **Més concís**: Permet una sintaxi més neta i concisa.

Exemple:
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


## Referències

* [Manual de PHP](https://www.php.net/manual/es/index.php)
* [PHP en 2020](https://www.jesusamieiro.com/wp-content/uploads/2020/10/20201024-hacktoberday-PHP-en-2020.pdf), por Jesús Amieiro
* [Apunts de PHP](https://www.mclibre.org/consultar/php/) de Bartolomé Sintes, profesor del IES Abastos de Valencia
* [Guía de Estilo - PSR](http://coppeldev.github.io/php/standards/coppel.html)
* [PHP - La manera correcta](http://phpdevenezuela.github.io/php-the-right-way/)

## Exercicis Solucionats

### Bateria d'Exercicis per a la Unitat de PHP

#### Exercici 1: Introducció a PHP
1. Crea un fitxer `hola.php` que imprimeixi "Hola, món!" a la pantalla.
2. Modifica el fitxer `hola.php` per tal que imprimeixi el teu nom utilitzant una variable.

#### Exercici 2: Ús de cometes
1. Crea un fitxer `cometes.php` que defineixi una variable `$nom` amb el teu nom i imprimeixi la frase "Hola, [nom]!" utilitzant cometes dobles.
2. Modifica el fitxer `cometes.php` per utilitzar cometes simples i compara els resultats.

#### Exercici 3: Funcions bàsiques
1. Crea una funció `suma` que sumi dos números i retorni el resultat. Invoca la funció amb els números 5 i 3 i imprimeix el resultat.
2. Crea una funció `multiplicacio` que multipliqui dos números i retorni el resultat. Invoca la funció amb els números 4 i 7 i imprimeix el resultat.

#### Exercici 4: Control de flux - Condicionals
1. Crea un fitxer `edat.php` que defineixi una variable `$edat`. Si `$edat` és major o igual a 18, imprimeix "Ets major d'edat"; en cas contrari, imprimeix "Ets menor d'edat".
2. Modifica el fitxer `edat.php` per tal que imprimeixi "Edat invàlida" si `$edat` és un número negatiu.

#### Exercici 5: Control de flux - Bucles
1. Crea un fitxer `bucles.php` que utilitzi un bucle `for` per imprimir els números del 0 al 9.
2. Modifica el fitxer `bucles.php` per utilitzar un bucle `while` que faci el mateix.

#### Exercici 6: Treballar amb arrays
1. Crea un fitxer `arrays.php` que defineixi un array `$fruites` amb tres elements: "poma", "plàtan" i "maduixa". Imprimeix el primer element de l'array.
2. Afegeix un quart element "taronja" a l'array i imprimeix tots els elements utilitzant un bucle `foreach`.

#### Exercici 7: Cometes dobles i variables
1. Crea un fitxer `cometes_dobles.php` que defineixi una variable `$color` amb el valor "blau". Utilitza cometes dobles per imprimir "El meu color preferit és [color]."
2. Modifica el fitxer per imprimir "El meu color preferit és blau." utilitzant cometes simples i concatenació.

#### Exercici 8: Combinació de funcions i arrays
1. Crea una funció `afegir_element` que prengui un array i un element com a arguments, afegeixi l'element a l'array i retorni l'array modificat.
2. Crea un fitxer `exercici8.php` on defineixis un array `$animals` amb els elements "gat" i "gos". Utilitza la funció `afegir_element` per afegir "conill" a l'array i imprimeix tots els elements.

#### Exercici 9: Utilitzant `match` per a categoritzar

=== "Enunciat"

Crea un fitxer `categoritzar.php` que utilitzi la instrucció `match` per categoritzar una variable `$nota` segons el següent criteri:
     - Si la nota és 10, imprimir "Excel·lent".
     - Si la nota és 8 o 9, imprimir "Molt bé".
     - Si la nota és 5, 6 o 7, imprimir "Bé".
     - Per qualsevol altra nota, imprimir "Insuficient".

=== "Solució"

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

#### Exercici 10: Llista de preus amb `match`

=== "Enunciat"

Crea un fitxer `preus.php` que utilitzi la instrucció `match` per assignar un preu a una variable `$producte`. Els productes i preus són:
     - "pa" => 1.00
     - "llet" => 0.80
     - "formatge" => 2.50
     - Qualsevol altre producte => 0.00

=== "Solució"

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

#### Exercici 11: Calculadora simple amb `match`

Crea un fitxer `calculadora.php` que utilitzi la instrucció `match` per fer operacions matemàtiques bàsiques (`+`, `-`, `*`, `/`). La variable `$operacio` ha de determinar l'operació a realitzar i les variables `$a` i `$b` seran els operands.

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

#### Exercici 12: Validació de formulari amb `match`

1. Crea un fitxer `formulari.php` que utilitzi la instrucció `match` per validar un formulari amb camps per a nom, correu electrònic i edat. Si algun camp està buit, ha de retornar un missatge d'error corresponent.

<details>
<summary>

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
</summary>
</details>
