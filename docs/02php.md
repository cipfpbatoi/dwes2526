# El llenguatge PHP

??? abstract "Duració i criteris d'avaluació"

    Duració estimada: 10 hores

    <hr />

    | Resultat d'aprenentatge | Criteris d'avaluació|
    | -------                 | -------             |
    | 2. Escriu sentències executables per un servidor Web reconeixent i aplicant procediments d'integració del codi en llenguatges de marques. | a) S'han reconegut els mecanismes de generació de pàgines Web a partir de llenguatges de marques amb codi embegut. <br/> b) S'han identificat les principals tecnologies associades.  <br/> c) S'han utilitzat etiquetes per a la inclusió de codi en el llenguatge de marques.  <br/> d) S'ha reconegut la sintaxi del llenguatge de programació que s'ha d'utilitzar.  <br/> e) S'han escrit sentències simples i s'ha comprovat els seus efectes en el document resultant.  <br/> f) S'han utilitzat directives per a modificar el comportament predeterminat.  <br/> g) S'han utilitzat els diferents tipus de variables i operadors disponibles en el llenguatge.  <br/> h) S'han identificat els àmbits d'utilització de les variables.  <br/> |


# Apunts per a la Unitat: Escriu sentències executables per un servidor web reconeixent i aplicant procediments d'integració del codi en llenguatges de marques

## 1. Introducció a PHP

#### Què és PHP?
**PHP** (Hypertext Preprocessor) és un llenguatge de programació de codi obert, especialment dissenyat per al desenvolupament web del costat del servidor. Es pot incrustar fàcilment en codi HTML, cosa que el fa una opció popular per crear aplicacions web dinàmiques i interactives. PHP s'utilitza per gestionar el contingut dinàmic, les bases de dades, el seguiment de sessions i fins i tot per crear aplicacions completes.

#### Història de PHP
PHP va ser creat originalment per Rasmus Lerdorf el **1994**. Inicialment, PHP era una col·lecció d'eines CGI (Common Gateway Interface) escrites en C, utilitzades per rastrejar les visites a la seva pàgina web. Rasmus va anomenar aquestes eines "Personal Home Page Tools" (Eines per a la pàgina personal). Amb el temps, el llenguatge va evolucionar i es va convertir en una eina més robusta i potent per al desenvolupament web. El 1997, dues persones, Zeev Suraski i Andi Gutmans, van redissenyar completament el nucli de PHP, cosa que va donar lloc a **PHP 3**, la primera versió àmpliament utilitzada. Més tard, el 2000, **PHP 4** va ser llançat amb el motor Zend, el qual va millorar significativament el rendiment.

#### Ús de PHP
PHP s'utilitza principalment per a:

* Generació de pàgines web dinàmiques: Permet que el servidor generi contingut HTML dinàmic basat en la lògica programada.
* Interacció amb bases de dades: PHP es pot connectar fàcilment a diverses bases de dades com MySQL, PostgreSQL, SQLite, etc., cosa que facilita la creació d'aplicacions web amb capacitats d'emmagatzematge de dades.
* Gestió de sessions: PHP proporciona una manera senzilla de gestionar sessions d'usuari, cosa que és essencial per a aplicacions que requereixen autenticació i autorització.
* Manipulació de fitxers: PHP permet crear, llegir, escriure, eliminar i gestionar fitxers al servidor.
* Enviament de correus electrònics: Amb PHP, es poden enviar correus electrònics des de l'aplicació web, cosa útil per a notificacions, confirmacions d'inscripció, etc.

#### Importància en el desenvolupament web
PHP és un dels llenguatges més utilitzats en el desenvolupament web per diverses raons:

* Facilitat d'aprenentatge: PHP és relativament fàcil d'aprendre per als principiants en programació web. La seva sintaxi és senzilla i similar a altres llenguatges com C i Perl.
* Gran comunitat i suport: PHP té una gran comunitat de desenvolupadors que proporcionen suport, biblioteques, extensions i eines. A més, hi ha nombrosos recursos en línia, tutorials i documentació.
* Integració amb bases de dades: PHP es pot integrar fàcilment amb una àmplia varietat de bases de dades, cosa que el fa ideal per a aplicacions web basades en dades.
* Flexibilitat i escalabilitat: PHP és altament flexible i es pot utilitzar per desenvolupar tant aplicacions petites com projectes grans i complexos. També és escalable, cosa que permet gestionar un gran volum de trànsit.
* Cost efectiu: Com que és de codi obert, PHP és gratuït per utilitzar i distribuir. Això redueix els costos de desenvolupament per a les empreses i els desenvolupadors.

#### Exemple de codi PHP simple
Aquí tens un exemple senzill de com funciona PHP:

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

## 4. Etiquetes per a inserció de codi
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

## 5. Tipus de dades. Conversions entre tipus de dades
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

## 6. Variables. Operadors. Àmbits d'utilització
Variables es defineixen amb $, per exemple:
```php
$variable = "valor";
```
Operadors:
- Aritmètics: `+`, `-`, `*`, `/`
- Assignació: `=`, `+=`, `-=`
- Comparació: `==`, `===`, `!=`
- Lògics: `&&`, `||`, `!`

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

## 7. Sintaxi del llenguatge de programació (PHP)
Comentaris:
```php
// Comentari d'una línia
/* Comentari de diverses línies */
```
Estructures de control:
```php
// Condicions
if ($condicio) {
    // Codi si la condició és certa
} elseif ($altra_condicio) {
    // Codi si la segona condició és certa
} else {
    // Codi si cap de les condicions anteriors és certa
}

// Bucles
for ($i = 0; $i < 10; $i++) {
    echo $i;
}

$i = 0;
while ($i < 10) {
    echo $i;
    $i++;
}

$matriu = array(1, 2, 3);
foreach ($matriu as $valor) {
    echo $valor;
}
```
Funcions:
```php
function nom_de_la_funcio($parametre) {
    // Codi
}
```
Exemple:
```php
function saludar($nom) {
    return "Hola, " . $nom;
}
echo saludar("Joan");
```

## 8. Mecanismes de generació de pàgines web amb codi embegut
PHP permet generar pàgines dinàmiques incrustant codi PHP en HTML. Exemple:
```php
<!DOCTYPE html>
<html>
<body>
    <h1><?php echo "Hola, món!"; ?></h1>
</body>
</html>
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

## 10. Sentències simples en PHP i els seus efectes
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

## 11. Àmbits de les variables (local, global, estàtic)
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

## 12. Mecanismes de decisió (if, switch)
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

## 13. Bucles (for, while, foreach)
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

## 14. Comentaris en el codi
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

## Exercicis

### PHP bàsic

201. `201.php` (pissarra): Crea un fitxer PHP anomenat "201.php". 
Defineix dues variables per representar l'amplada i l'altura del rectangle i assigna'ls valors 10 i 5.
Defineix una constant anomenada "factor" i assigna-li un valor 2. Aquesta constant s'utilitzarà per calcular l'àrea del rectangle.
Calcula l'àrea del rectangle utilitzant la fórmula:

Àrea = Amplada x Altura x FACTOR

Imprimeix el resultat utilitzant la funció echo i una cadena de text descriptiva.![203](imagenes/02/02p203.png){align=right}

202. `202.php`: Escriu un programa que emmagatzeme en variables el teu nom, primer cognom, segon cognom, email, any de naixement i telèfon. Després mostra'ls per pantalla dins d'una taula.

203. `203.html` i `203.php` (pissarra): És el mateix exercici que l'anterior, però separant la lògica. En el primer arxiu crearem el formulari per a introduir les dades, i després recollim les dades i generem la taula en el segon arxiu.

204. `204.php`: anys - Després de llegir l'edat d'una persona, mostrar l'edat que tindrà dins de 10 anys i fa 10 anys.
     A més, mostra quin any serà en cadascun dels casos.
     Finalment, mostra l'any de jubilació suposant que treballaràs fins als 67 anys.
     En aquest cas, no fa falta que prèviament crees un formulari, pots provar l'exercici via URL: `204.php?edat=33`.

!!! tip "`$anyoActual = date("Y");`"

205. `205.php` (pissarra): dines -A partir d'una quantitat de diners, mostrar la seua descomposició en bitllets (500, 200, 100, 50, 20, 10, 5) i monedes (2, 1), perquè el nombre d'elements siga mínim.
     No s'ha d'utilitzar cap instrucció condicional. Per exemple, en introduir `139` ha de mostrar:

     1 bitllet de 100
    
     0 bitllet de 50
    
     1 bitllet de 20
    
     1 bitllet de 10
    
     1 bitllet de 5 
    
     2 moneda de 2 

    !!! tip "Pots forçar a realitzar la divisió sencera mitjançant la funció `intdiv($dividend, $divisor)` o passar un número flotant a enter pots usar la funció `intval()`"

206. `206.php`: A partir d'un `numero`, mostra per pantalla si el número és `positiu`, `negatiu` o `zero`.

207. `207.php`: Sense fer ús de condicions amb operadors lògics, mostra el major de tres números (`a`, `b` i `c`).

208. `208.php`: A partir d'una `edat` mostra per pantalla:

     * `bebé` si té menys de 3 anys
     * `xiquet` si té entre 3 i 12 anys
     * `adolescent` entre 13 i 17 anys
     * `adult` entre 18 i 66
     * `jubilat` a partir de 67 
     
209. `209.php`: Escriu un programa que funcione similar a un rellotge, de manera que a partir dels valors de `hora`, `minut` i `segon` mostre l'hora dins d'un segon. Després de les `23.59:59` seran les `0:0:0`.

### Bucles

220. Escriu un programa que mostre els nombres parells del 0 al 50 (dins d'una llista desordenada) (pissarra).

221. Escriu un programa que sume els números de l'1 al 10.

222. A partir d'una `base` i `exponent`, mitjançant l'acumulació de productes, calcula la potència utilitzant la instrucció `for` (pissarra).

223. Mostra dins d'una taula HTML la taula de multiplicar del `nombre` que reba com a paràmetre. Utilitza `<thead>` amb els seus respectius `<th>` i `<tbody`> per a dibuixar la taula. Per exemple:

    a | * | b | = | a*b
    -- | -- | -- | -- | --
    7  | * | 1 | = | 7
    7  | * | 2 | = | 14
    ...
    7  | * | 10 | = | 70


224. `224.html`: Crea un formulari que permeta llegir una `quantitat`. (pissarra)
     `224.php`: a partir de la quantitat, prepara un formulari amb tantes caixes de dades com el seu valor.
     Finalment a partir de les dades de totes les caixes de la pàgina anterior, suma'ls i mostra el total.

    !!! tip inline end
        Per a guardar una dada oculta pots utilitzar un camp de formulari de tipus ocult: `<input type="hidden" name="cantidad" value="33" />`

225. `225.html` i `225.php`: Apartir d'un nombre de `files` i `columnes`, crear una taula amb aqueixa grandària.
     Les cel·les han d'estar emplenades amb els valors de les coordenades de cada cel·la.

226. `226.html` i `226.php`: Basant-te en l'exercici anterior, emplena la taula de manera que només les vores de l'esquerra i la de dalt tinguen contingut, quedant-se la resta de cel·les en blanc.
     
227. `227.html` i `227.php`:Basant-te en l'exercici anterior, ara només ha d'aparéixer el contingut dels dues diagonals.


### Arrays

230. `230.php`: Emplena un array amb 50 números aleatoris compresos entre el 0 i el 99, i després mostra-ho en una llista desordenada.
     Per a crear un número aleatori, utilitza la funció `rand(inici, fi)`. (**Pissarra**) Per exemple:

    ``` php
    $num = rand(0, 99)
    ```

231. `231.php`: A partir de l'exercici 230, genera un array aleatori de 33 elements amb números compresos entre el 0 i 100 i calcula:

     * El major
     * El menor
     * La mitjana

232. `232.php`: Emplena un array de 100 elements de manera aleatòria amb valors `M` o `F` (per exemple `["M", "M", "F", "M", ...]`). Una vegada completat, torna a recórrer-ho i calcula quants elements hi ha de cadascun dels valors emmagatzemant el resultat en un array associatiu `['M' => 44, 'F' => 66]` (no utilitzes variables per a comptar les `M` o les `F`).
     Finalment, mostra el resultat per pantalla

233. `233.php`: Torna a realitzar l'exercici 207, el de les monedes (500, 200, 100, 50, 20, 10, 5, 2, 1), però fent ús de arrays i un bucle.
     Emmagatzema el resultat en un array associatiu. (**pissarra**)
     Mostra el resultat en una llista desordenada únicament amb les quantitats que tenen algun valor.

234. `234.php`: Mitjançant un array associatiu, emmagatzema el nom i l'alçada de 5 persones (`nom => alçada`).
     Posteriorment, recorre el array i mostra-ho en una taula HTML.
     Finalment afig una última fila a la taula amb l'altura mitjana.

235. `235.php`: Mitjançant un array bidimensional, emmagatzema el nom, altura i email de 5 persones. Per a això, crea un array de persones, sent cada persona un array associatiu: `[ ['nom'=>'Aitor', 'altura'=>182, 'email'=>'aitor@correo.com'],[…],… ]`
     Posteriorment, recorre el array i mostra-ho en una taula HTML. (**pissarra**)

236. `236.html` i `236.php`: a partir d'un formulari amb un camp de `quantitat` de persones, generar un nou formulari per a llegir el nom, altura i email de `quantitat` persones.

237. `237.php`: A partir de les persones introduïdes, mostrar les seues dades en una taula, i posteriorment, destaca les dades del més alt i el del més baix.

238. `238.php`: Emplena un array bidimensional de 6 files per 9 columnes amb números aleatoris compresos entre 100 i 999 (tots dos inclosos). Tots els números han de ser diferents, és a dir, no es pot repetir cap. 
Mostra a continuació per pantalla el contingut del array de tal forma que:

     * La columna del màxim ha d'aparéixer en blau.
     * La fila del mínim ha d'aparéixer en verd
     * La resta de números han d'aparéixer en negre.

### Funcions

240. `functions.php`: Crea les següents funcions: (**pissarra**)

     * Una funció que esbrine si un número és parell: `esParell(int $num): bool`
     * Una funció que retorne un array de grandària `$tam` amb números aleatoris comprés entre `$min` i `$max` : `arrayAleatori(int $tam, int $min, int $max) : array`
     * Una funció que reba un `$array` per referència i retorne la quantitat de nombres parells que hi ha emmagatzemats: `countParells(array &$array): int`

241. `functions.php`: Crea les següents funcions:

     * Una funció que retorne el major de tots els números rebuts com a paràmetres: `function major(): int`. No pots usar la funció `max()`.
     * Una funció que concatene tots els paràmetres rebuts separant-los amb un espai: `function concatenar(...$paraules) : string`. Utilitza l'operador `...`.

242. `functions.php`: Afig les següents funcions:

     * `digits(int $num): int` → retorna la quantitat de dígits d'un número.
     * `digitsN(int $num, int $post): int` → retorna el dígit que ocupa, començant per l'esquerra, la posició `$post`.
     * `llevaDarrere(int $num, int $cant): int` → li lleva per darrere (dreta) `$cant` dígits.
     * `llevaDavant(int $num, int $cant): int` → li lleva per davant (esquerra) `$cant` dígits.
     
243. `functions.php`: Afig dues funcions:

     * peseta2euros: passa de pessetes a euros
     * euro2pesetes: passa d'euros a pessetes

    Cada funció ha de rebre dos paràmetres:

    * La quantitat a transformar
    * La cotització, amb un paràmetre per defecte amb el factor de transformació.

    `243.php`: utilitza-la per construir un formulari que faça la transformació en ambdos sentits.

244. `244a.php`: A partir d'una quantitat de productes, llegir el nom i cost de la quantitat de productes indicats (similar a l'exercici 237, però aquesta vegada no fa falta crear el formulari amb la quantitat, es rep mitjançant un paràmetre GET via URL). 

     `244b.php`: Després de llegir les dades del tiquet de compra, enumera en una taula els productes, amb el seu preu en euros i pessetes, i finalment, en una última fila, totalitzar en totes dues monedes.

### Plantilles

245. `245a.php`: A partir dels arxius creats en l'exercici anterior, crea una plantilla mitjançant *includes*: *245a.php*: similar a *244a.*php, però separant l'encapçalat (Supermercat Sever en *h1*) i el peu (El teu supermercat de confiança) en fitxers externs i referenciant a ells mitjançant *include*. (**pissarra**)
     `245b.php`: rep les dades de l'anterior, i reutilitza part de *245b.php* canviant la taula per una llista desordenada dels productes al costat del seu preu i utilitzan les plantilles fetes. 

246. Simularem un formulari d'accés:

     * `246.html`: el formulari d'entrada, que sol·licita l'usuari i contrasenya.
     * `246.php`: rep les dades i comprova si són correctes (els usuaris es guarden en un array associatiu en el fitxer `246password.php`.Utilitza  `include`.
     * `246.php`: L'usuari introduït és correcte
     * `246.php`: L'usuari és incorrecte. Informar si tots dos estan mal o només la contrasenya.


### Cadenes i subcadenes

Tots els exercicis s'han de realitzar creant noves funcions per a encapsular el codi.
A més de la pròpia funció, l'exercici ha de contindre codi per a poder provar-lo.

250. `250.php`: A partir d'una frase, retorna una nova amb només els caràcters de les posicions imparelles. (**pissarra**)
251. `251.php`: A partir d'una frase, retorna la quantitat de cadascuna de les vocals, i el total d'elles.
252. `252.php`: A partir d'una frase amb paraules només separades per espais, retornar (**pissarra**)
     * Lletres totals i quantitat de paraules
     * Una línia per cada paraula indicant la seua grandària

253. `253.php`: EsCrIu UnA fUnCiÓ qUe TrAnSfOrMe UnA cAdEnA eN cAnI.
254. `254.php`: Escriu una funció que retorne un booleà indicant si una paraula és palíndroma (es llig igual d'esquerra a dreta que de dreta a esquerra, per exemple, “lligar és ser agil”).
255. `255.php`: Utilitzant les funcions per a treballar amb caràcters, a partir d'una cadena i un desplaçament:
     * Si el desplaçament és 1, substitueix l'A per B, la B per C, etc.
     * El desplaçament no pot ser negatiu
     * Si s'ix de l'abecedari, ha de tornar a començar
     * Cal respectar els espais, punts i comes.
256. `256.html`: Crea un programa que permeta a l'usuari llegir un conjunt de números separats per espais.
     `256.php`: El programa filtrarà els números llegits per a tornar a mostrar únicament els nombres parells i indicarà la quantitat existent.
     ```
     Dona'm números: 1 4 7 9 23 10 8
     Els 3 nombres parells són: 4 10 8
     ```
## Activitats

270. `270.php` : A partir del fitxer de records d'atletisme que se un [suministra](recursos/atletes.php) pinta una taula amb tots els records.
     ![270](imagenes/02/02p270.png){align=right & width=250}. Es valorarà que s'utilitzen comentaris en el resultat d'html per a indicar el codi que s'ocupa de la capçalera de la taula i el del cos de la taula. Tambè que no s'utilitze ninguna instrucció de php per a imprimir la taula(echo, print ...)

    `270a.php`: Extrau el codi que s'utilitza per a pintar la taula al fitxer 207a.php i fes un include del mateix des de 270.php

271. `271.php` : A partir del [formulari](recursos/formRecord.html) per a modificar un record i una vegada que l'usuari introduïsca les dades corresponents:
     * Si no existeix la prova ixirà un missatge comunicant-li a l'usuari que no existeix eixa prova 'La prova ... no existeix en la llista de records oficials de la FEA' 
     * Si existeix es modificaran les dades i mostrarem la taula amb les dades modificades. 

!!! tip  "Hem de fer un include al fitxer 270a.php per mostrar la taula" 

272. `272.php` : Fes una pàgina d'estadistiques i fes una funció per a cada una d'elles
     * El record més vell. La funcio **vell(array):mixed** extrau la key de la més antiga de les dates d'un array en format 'dd.mm.yyyy'  

!!! tip "Crea una funció **fecha_inglesa(string):string**. Funció que donada un data en format 'dd.mm.yyyy' el transforma en format 'yyyy/mm/dd'"

  * El club, el atleta i la ciutat amb més records. La funció **laureado(array):mixed** extrau la key de la que més es repeteix. Si hi ha més d'un extreu un. 
  * L'atleta més jove en conseguir el record. Funció **jove(array,array):mixed** on de l'array de natalici i data extreu el que la diferència siga menor. 

!!! tip "Crea una funció **any(string):string**. Funció que donada un data en format 'dd.mm.yyyy' el transforma en format 'yyyy' "

  * Al final pinta la taula 
  
!!! tip  "La funció [array_column_ext](recursos/functions.php) ens permet extraure una columna d'un array multidimensional respectant la clau del array. La possariem de la següent forma: array_column_ext($records,'data',-1)"

!!! tip "Els [tests](recursos/tests_examen.zip) s'han de possar en la carpeta corresponent. El d'aceptació en accceptance i l'altre en unit"