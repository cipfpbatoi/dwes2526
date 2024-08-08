# PHP Orientant a Objectes

??? abstract "Duració i criteris d'avaluació"

    Duració estimada: 20 hores

    <hr />

    | Resultat d'aprenentatge | Criteris d'avaluació |
    | --------                | --------             |
    | 5. Desenvolupa aplicacions Web identificant i aplicant mecanismes per a separar el codi de presentació de la lògica de negoci.| a) S'han identificat els avantatges de separar la lògica de negoci dels aspectes de presentació de l'aplicació. <br/> b) S'han analitzat tecnologies i mecanismes que permeten realitzar aquesta separació i les seues característiques principals. <br/> c) S'han utilitzat objectes i controls en el servidor per a generar l'aspecte visual de l'aplicació Web en el client. <br/> d) S’han utilitzat formularis generats de forma dinàmica per a respondre als esdeveniments de l'aplicació Web. <br/> e) S'han identificat i aplicat els paràmetres relatius a la configuració de l'aplicació Web. <br/> f) S'han escrit aplicacions Web amb manteniment d'estat i separació de la lògica de negoci. <br/> g) S'han aplicat els principis de la programació orientada a objectes. <br/> g) S'ha provat i documentat el codi. |


## Classes i Objectes

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

## Encapsulació

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

### Rebent i enviant objectes

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

## Constructor

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

### Constructors en PHP 8

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

## Classes estàtiques

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

## Introspecció

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

## Herència

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

### Sobreescriure mètodes

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

### Constructor en fills

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

## Classes abstractes

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

## Classes finals

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

## Interfícies

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

## Mètodes encadenats

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

## Mètodes màgics

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

## Espai de noms

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

### Accés

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

### Accés

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

### Organització

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

### Autoload

No és tediós haver de fer el `include` de les classes? El autoload ve al rescat.

Així doncs, permet carregar les classes (no les constants ni les funcions) que s'utilitzaran i evitar haver de fer el `include_once` de cadascuna d'elles. Per a això, s'utilitza la funció `spl_autoload_register`

``` php
<?php
spl_autoload_register( function( $nombreClase ) {
    include_once $nombreClase.'.php';
} );
?>
```

!!! question "Per què es diuen autoload?"
    Perquè abans es realitzava mitjançant el mètode màgic `__autoload()`, el qual està *deprecated* des de PHP 7.2

I com organitzem ara el nostre codi aprofitant el autoload?

<figure style="float: right;">
    <img src="imagenes/03/03autoload.png" width="600">
    <figcaption>Organització amb autoload</figcaption>
</figure>

Per a facilitar la cerca dels recursos a incloure, és recomanable col·locar totes les classes dins d'una mateixa carpeta. Nosaltres la col·locarem dins de `app` (més endavant, quan estudiem *Laravel* veurem el motiu d'aquesta decisió). Altres carpetes que podem crear són `test` per a col·locar les proves *PhpUnit* que després realitzarem, o la carpeta `vendor` on s'emmagatzemaran les llibreries del projecte (aquesta carpeta és un estándard dins de PHP, ja que *Composer* la crea automàticament).

Com hem col·locat tots els nostres recursos dins de `app`, ara nostre `autoload.php` (el qual col·loquem en la carpeta arrel) només buscarà dins d'aqueixa carpeta:

``` php
<?php
spl_autoload_register( function( $nombreClase ) {
    include_once "app/".$nombreClase.'.php';
} );

```

!!! tip "autoload i rutes errònies"
    En *Ubuntu* en fer el *include* de la classe que rep com a paràmetre, les barres dels namespace (`\`) són diferents a les de les rutes (`/`). Per això, és millor que utilitzem el fitxer autoload:
    ``` php
    <?php
    spl_autoload_register( function( $nombreClase ) {
        $ruta = "app\\".$nombreClase.'.php';
        $ruta = str_replace("\\", "/", $ruta); // Sustituimos las barras
        include_once $_SERVER['DOCUMENT_ROOT'].'/'.$ruta;
    } );
    
    ```

## Separar la lògica de negoci dels aspectes de presentació de l'aplicació

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

#### Exemple MVC

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


## Gestió d'Errors

PHP classifica els errors que ocorren en diferents nivells. Cada nivell s'identifica amb una constant. Per exemple:

* `E_ERROR`: errors fatals, no recuperables. S'interromp el script.
* `E_WARNING`: advertiments en temps d'execució. El script no s'interromp.
* `E_NOTICE`: avisos en temps d'execució.

Podeu comprovar el llistat complet de constants de <https://www.php.net/manual/es/errorfunc.constants.php>

Per a la configuració dels errors podem fer-ho de dues formes:

* A nivell de `php.ini`:
  * `error_reporting`: indica els nivells d'errors a notificar
    * `error_reporting = E_ALL & ~E_NOTICE` -> Tots els errors menys els avisos en temps d'execució.
  * `display_errors`: indica si mostrar o no els errors per pantalla. En entorns de producció és comuna posar-ho a `off`
  * mitjançant codi amb les següents funcions:
    * `error_reporting(codigo)` -> Controla quins errors notificar
    * `set_error_handler(nombreManejador)` -> Indica que funció s'invocarà cada vegada que es trobe un error. El manejador rep com a paràmetres el nivell de l'error i el missatge

A continuació tenim un exemple mitjançant codi:

=== "Funcions per a la gestió d'errors"

    ``` php
    <?php
    error_reporting(E_ALL & ~E_NOTICE & ~E_WARNING);
    $resultado = $dividendo / $divisor;

    error_reporting(E_ALL & ~E_NOTICE);
    set_error_handler("miManejadorErrores");
    $resultado = $dividendo / $divisor;
    restore_error_handler(); // vuelve al anterior

    function miManejadorErrores($nivel, $mensaje) {
        switch($nivel) {
            case E_WARNING:
                echo "<strong>Warning</strong>: $mensaje.<br/>";
                break;
            default:
                echo "Error de tipo no especificado: $mensaje.<br/>";
        }
    }
    ```

=== "Consola"

    ```
    Error de tipo no especificado: Undefined variable: dividendo.
    Error de tipo no especificado: Undefined variable: divisor.
    Error de tipo Warning: Division by zero.
    ```

## Excepcions

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

### Creant excepcions

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

### Excepcions múltiples

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

### Rellançar excepcions

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

## SPL

*Standard PHP Library* és el conjunt de funcions i utilitats que ofereix PHP, com:

* Estructures de dades
* Pila, cua, cua de prioritat, llista doblement enllaçada, etc...
* Conjunt de iteradores dissenyats per a recórrer estructures agregades
* arrays, resultats de bases de dades, arbres XML, llistats de directoris, etc.

Podeu consultar la documentació en <https://www.php.net/manual/es/book.spl.php> o veure alguns exemples en <https://diego.com.es/tutorial-de-la-libreria-spl-de-php>

També defineix un conjunt d'excepcions que podem utilitzar perquè les llancen les nostres aplicacions:

* `LogicException` (`extends Exception`)
    * `BadFunctionCallException`
    * `BadMethodCallException`
    * `DomainException`
    * `InvalidArgumentException`
    * `LengthException`
    * `OutOfRangeException`
* `RuntimeException` (`extends Exception`)
    * `OutOfBoundsException`
    * `OverflowException`
    * `RangeException`
    * `UnderflowException`
    * `UnexpectedValueException`

També podeu consultar la documentació d'aquestes excepcions en <https://www.php.net/manual/es/spl.exceptions.php>.


## Composer

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

## Arxius PDF


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

## Monolog

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

Per exemple, en l'arxiu `pruebaLog.php` que col·locaríem en l'arrel, primer incloem el *autoload*, importem els classes a utilitzar per a finalment usar els mètodes de *Monolog*:

``` php
<?php
include __DIR__ ."/vendor/autoload.php";

use Monolog\Logger;
use Monolog\Handler\StreamHandler;

$log = new Logger("MiLogger");
$log->pushHandler(new StreamHandler("logs/milog.log", Logger::DEBUG));

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

Cada instància `Logger` té un nom de canal i una pila de manejadores (*handler*).
Cada missatge que manem al log travessa la pila de manejadores, i cadascun decideix si ha de registrar la informació, i si es dona el cas, finalitzar la propagació.
Per exemple, un `StreamHandler` en el fons de la pila que ho escriga tot en disc, i en el topall afig un `MailHandler` que envie un mail només quan hi haja un error.

### Manejadors

Cada manejador tambien té un formatejador (`Formatter`). Si no s'indica cap, se li assigna un per defecte. L'últim manejador inserit serà el primer a executar-se.
Després es van executant conforme a la pila.

Els manejadores més utilitzats són:

* `StreamHandler(ruta, nivel)`
* `RotatingFileHandler(ruta, maxFiles, nivel)`
* `NativeMailerHandler(para, asunto, desde, nivel)`
* `FirePHPHandler(nivel)`

Si volem que els missatges de l'aplicació isquen pel log del servidor,
en el nostre cas l'arxiu `error.log` de Apatxe* utilitzarem com a ruta l'eixida d'error:

``` php
<?php
// error.log
$log->pushHandler(new StreamHandler("php://stderr", Logger::DEBUG));
```

!!! tip "FirePHP"
Per exemple, mitjançant `FirePHPHandler`, podem utilitzar `FirePHP`, la qual és una eina per a fer debug en la consola de Firefox*.
Després d'instal·lar l'extensió en Firefox, habilitar les opcions i configurar el *Handler*, podem veure els missatges acolorits amb les seues dades:

    ``` php
    <?php
    $log = new Logger("MiFirePHPLogger");
    $log->pushHandler(new FirePHPHandler(Logger::INFO));

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

### Canals

Se'ls assigna en crear el `Logger`. En grans aplicacions, es crea un canal per cada subsistema: vendes, comptabilitat, magatzem.
No és una bona pràctica usar el nom de la classe com a canal, això es fa amb un processador.

Per al seu ús, és recomane assignar el log a una propietat privada a Logger, i posteriorment, en el constructor de la classe, assignar el canal, manejadors i format.

``` php
<?php
$this->log = new Logger("MiApp");
$this->log->pushHandler(new StreamHandler("logs/milog.log", Logger::DEBUG));
$this->log->pushHandler(new FirePHPHandler(Logger::DEBUG));
```

I dins dels mètodes per a escriure en el log:

``` php
<?php
$this->log->warning("Producto no encontrado", [$producto]);
```

### Processadors

Els processadors permeten afegir informació als missatges.
Per a això, s'apilen després de cada manejador mitjançant el mètode `pushProcessor($processador)`.

Alguns processadors coneguts són `IntrospectionProcessor` (mostren la línia, fitxer, classe i metodo des del qual s'invoca el log), `WebProcessor` (afig la URI, mètode i IP) o `GitProcessor` (afig la branca i el commit).

=== "PHP"

    ``` php
    <?php
    $log = new Logger("MiLogger");
    $log->pushHandler(new RotatingFileHandler("logs/milog.log", 0, Logger::DEBUG));
    $log->pushProcessor(new IntrospectionProcessor());
    $log->pushHandler(new StreamHandler("php://stderr", Logger::WARNING));
    // no usa Introspection pq lo hemos apilado después, le asigno otro
    $log->pushProcessor(new WebProcessor());
    ```

=== "Consola en format text"

    ``` log
    [2020-11-26T13:35:31.076138+01:00] MiLogger.DEBUG: Esto es un mensaje de DEBUG [] {"file":"C:\\xampp\\htdocs\\log\\procesador.php","line":12,"class":null,"function":null}
    [2020-11-26T13:35:31.078344+01:00] MiLogger.INFO: Esto es un mensaje de INFO [] {"file":"C:\\xampp\\htdocs\\log\\procesador.php","line":13,"class":null,"function":null}
    ```

### Formateadores

S'associen als manejadores amb `setFormatter`. Els formateadores més utilitzats són `LineFormatter`, `HtmlFormatter` o `JsonFormatter`.

=== "PHP"

    ``` php
    <?php
    $log = new Logger("MiLogger");
    $rfh = new RotatingFileHandler("logs/milog.log", Logger::DEBUG);
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

### Ús de Factories

En comptes de instanciar un log en cada classe, és convenient crear una factoria (per exemple, seguint la idea del patró de disseny [*Factory Method*](https://refactoring.guru/és/design-patterns/factory-method)).

Per al següent exemple, suposarem que creguem la factoria en el *namespace* `Dwes\Exemples\Util`.

``` php
<?php
namespace Dwes\Ejemplos\Util

use Monolog\Logger;
use Monolog\Handler\StreamHandler;

class LogFactory {

    public static function getLogger(string $canal = "miApp") : Logger {
        $log = new Logger($canal);
        $log->pushHandler(new StreamHandler("logs/miApp.log", Logger::DEBUG));

        return $log;
    }
}
```

Si en comptes de retornar un `Monolog\Logger` utilitzem la interfície de PSR, si en el futur canviem la implementació del log, no haurem de modificar nostre codi. Així doncs, la factoria ara retornarà `Psr\Log\LoggerInterface`:

``` php
<?php
namespace Dwes\Ejemplos\Util

use Monolog\Handler\StreamHandler;
use Monolog\Logger;
use Psr\Log\LoggerInterface;

class LogFactory {

    public static function getLogger(string $canal = "miApp") : LoggerInterface {
        $log = new Logger($canal);
        $log->pushHandler(new StreamHandler("log/miApp.log", Logger::DEBUG));

        return $log;
    }
}
```

Finalment, per a utilitzar la factoria, només canviem el codi que teníem en el constructor de les classes que usen el log, quedant alguna cosa asi:

``` php
<?php

namespace Dwes\Ejemplos\Model;

use Dwes\Ejemplos\Util\LogFactory;
use Monolog\Logger;

class Cliente {

    private $codigo; 

    private Logger $log;

    function __construct($codigo){ 
        $this->codigo=$codigo; 

        $this->log = LogFactory::getLogger();
    }

    /// ... resto del código
}
```

## Documentación con *phpDocumentor*



[phpDocumentor](https://www.phpdoc.org/) és l'eina per a documentar el codi PHP. És similar en propòsit i funcionament a *Javadoc*.

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
docker run --rm -v $(pwd):/data phpdoc/phpdoc:latest run -d /data/src -t /data/docs
```
Aquesta comanda fa el següent:

--rm: Això elimina el contenidor després d'executar-lo, així no es queden contenidors inactius.
-v $(pwd):/data: Munta el directori actual del teu sistema ($(pwd)) al directori /data dins del contenidor. Hauràs de reemplaçar $(pwd) amb el camí on està el teu codi font si no estàs executant aquesta comanda des del directori del teu projecte.
-d /data/src: Especifica el directori dins del contenidor on es troba el teu codi font. Reemplaça /data/src amb el camí corresponent dins del contenidor si és diferent.
-t /data/docs: Especifica on vols que es generi la documentació dins del contenidor. En aquest cas, es generarà dins de /data/docs.

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

## *Web Scraping*

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

## Proves amb Codeception

El curs passat, dins del mòdul de Entorns de Desenvolupament*, estudiarieu la importància de la realització de proves, així com les proves unitàries mitjançant [JUnit](https://junit.org/junit5/).

<figure style="float: right;">
    <img src="imagenes/05/tdd.png" width="300">
    <figcaption>Test Driven Development</figcaption>
</figure>

Hui dia és de gran importància seguir una bona metodologia de proves, sent el desenvolupament dirigit per les proves (Test Driven Development / TDD) un dels enfocaments més emprats, el qual consisteix en:

1. Escriure el test, i com no hi ha codi implementat, la prova falle (roig).
2. Escriure el codi d'aplicació perquè la prova funcione (verda).
3. refactoritzar el codi de l'aplicació amb l'ajuda de la prova per a comprovar que no trenquem res (refactor).

En el cas de PHP, l'eina que s'utilitza és *PHPUnit* (<https://phpunit.de/>), que com el seu nom indica, està basada en JUnit. La versió actual és la 9.0.
També podem utilitzar *Codeception* (<https://codeception.com/>) que inclou *PHPUnit*.

### Introducció a Codeception
Codeception és una eina de proves per a PHP que inclou suport per a proves unitàries, funcionals, d'acceptació i API. Per més informació, pots consultar la seua documentació oficial a Codeception.

#### Instal·lació i Configuració
Per començar amb Codeception, afegeix-lo com a dependència de desenvolupament en el teu composer.json:

``` json
"require-dev": {
"codeception/codeception": "^4.0"
},
"scripts": {
"test": "codecept run --colors"
}
```

També pots instal·lar-lo directament des del terminal:

``` bash
composer require --dev codeception/codeception ^4.0
```

!!! tip "Llibreries de desenvolupament"
Les llibreries que es col·loquen en `require-dev` són les de desenvolupament i *testing*, de manera que no s'instal·laran en un entorn de producció.


Una vegada instal·lat, executa vendor/bin/codecept bootstrap per inicialitzar la configuració bàsica.

##### Estructura de Carpetes
Codeception organitza les proves en diverses carpetes segons el tipus de prova:
tests/unit, tests/functional, tests/acceptance.

##### Exemple de Prova Unitària
A continuació, un exemple de com escriure una prova unitària en Codeception:

``` php
<?php
namespace tests\unit;

class PilaTest extends \Codeception\Test\Unit
{
    public function testPushAndPop()
    {
        $pila = [];
        $this->assertSame(0, count($pila));

        array_push($pila, 'batman');
        $this->assertSame('batman', $pila[count($pila)-1]);
        $this->assertSame(1, count($pila));

        $this->assertSame('batman', array_pop($pila));
        $this->assertSame(0, count($pila));
    }
}
```

##### Execució de Proves
Per executar les proves, pots utilitzar les comandes següents:

vendor/bin/codecept run (executa totes les proves)
vendor/bin/codecept run unit (executa només proves unitàries)
vendor/bin/codecept run --testdox --colors (mostra els resultats en format més llegible)

### Dissenyant proves

Tal com hem vist en l'exemple, la classe de prova ha d'heretar de `\Codeception\Test\Unit`, i el nom de la classe ha d'acabar en `Test`, d'aquí ve que hàgem anomenat la classe de prova com `PilaTest`.
Una prova implica un mètode de prova (públic) per cada funcionalitat a provar. Cada un dels mètodes se'ls associa un cas de prova.
Els mètodes han de nomenar-se amb el prefix `test`, per exemple, `testPushAndPop`. És molt important que el nom siga molt clar i descriptiu del propòsit de la prova. (*camelCase*).
En els casos de prova prepararem diverses assercions per a tota la casuística: rangs de valors, tipus de dades, excepcions, etc...

### Assercions

Les assercions permeten comprovar el resultat dels mètodes que volem provar. Les assercions esperen que el predicat sempre siga vertader.

PHPUnit ofereix les següent assercions:

* `assertTrue` / `assertFalse`: Comprova que la condició donada siga avaluada com true / false
* `assertEquals` / `assertSame`: Comprova que dues variables siguen iguals
* `assertNotEquals` / `assertNotSame`: Comprova que dues variables NO siguen iguals
* `Same` → comprova els tipus. Si no coincideixen els tipus i els valors, l'asserció fallarà
* `Equals` → sense comprovació estricta
* `assertArrayHasKey` / `assertArrayNotHasKey`: Comprova que un array posseïsca un *key* determinat / o NO ho posseïsca
* `assertArraySubset`: Comprova que un array posseïsca un altre array com subset del mateix
* `assertAttributeContains` / `assertAttributeNotContains`: Comprova que un atribut d'una classe continga una variable determinada / o NO continga una variable determinada
* `assertAttributeEquals`: Comprova que un atribut d'una classe siga igual a una variable determinada.

### Comparant l'eixida

Si els mètodes a provar generen contingut mitjançant `echo` o una instrucció similar, disposem de les següent expectatives:

* `expectOutputString(salidaEsperada)`
* `expectOutputRegex(expresionRegularEsperada)`

Les expectatives difereixen de les assercions que informen del resultat que s'espera abans d'invocar al mètode. Després de definir l'expectativa, s'invoca al mètode que realitza el `echo`/`print`.

``` php
<?php
namespace Dwes\Videoclub\Model;

use PHPUnit\Framework\TestCase;
use Dwes\Videoclub\Model\CintaVideo;

class CintaVideoTest extends TestCase {
    public function testConstructor()
    {
        $cinta = new CintaVideo("Los cazafantasmas", 23, 3.5, 107); 
        $this->assertSame( $cinta->getNumero(), 23);
    }

    public function testMuestraResumen()
    {
        $cinta = new CintaVideo("Los cazafantasmas", 23, 3.5, 107);
        $resultado = "<br>Película en VHS:";
        $resultado .= "<br>Los cazafantasmas<br>3.5 (IVA no incluido)";
        $resultado .= "<br>Duración: 107 minutos";
        // definimos la expectativa
        $this->expectOutputString($resultado);
        // invocamos al método que hará echo
        $cinta->muestraResumen();
    }
}
```

##### Proveïdors de Dades

Els providers en Codeception s'utilitzen principalment per a provar amb diferents conjunts de dades utilitzant el mateix test. Aquí tens una guia bàsica de com utilitzar-los:

Definir el Provider: Primer, has de definir una funció que retorni un array de dades. Aquesta funció és el teu provider. Per exemple:

```php
function myDataProvider() {
return [
['data1', 'result1'],
['data2', 'result2']
];
}
```

Utilitzar el Provider en un Test: Després, pots utilitzar aquest provider en un mètode de prova, passant el nom de la funció provider com a anotació. Per exemple:

```php
/**
* @dataProvider myDataProvider
  */
  public function testMyFunction($input, $expected) {
  $result = myFunction($input);
  $this->assertEquals($expected, $result);
  }
```

En aquest exemple, testMyFunction s'executarà múltiples vegades amb cada conjunt de dades proporcionat per myDataProvider. Això és especialment útil quan vols provar una funció o mètode amb diferents valors d'entrada i verificar si el resultat és el que esperes en cada cas.

### Provant excepcions

Les proves a més de comprovar que les classes funcionen com s'espera, han de cobrir tots els casos possibles. Així doncs, hem de poder fer proves que esperen que es llance una excepció (i que el missatge continga una certa informació):

Per a això, s'utilitzen les següent expectatives:

* `expectException(Excepcion::class)`
* `expectExceptionCode(codigoExcepcion)`
* `expectExceptionMessage(missatge)`

De la mateixa manera que abans, primer es posa l'expectativa, i després es provoca que es llance l'excepció:

``` php
<?php
public function testAlquilarCupoLleno() {
    $soporte1 = new CintaVideo("Los cazafantasmas", 23, 3.5, 107); 
    $soporte2 = new Juego("The Last of Us Part II", 26, 49.99, "PS4", 1, 1);
    $soporte3 = new Dvd("Origen", 24, 15, "es,en,fr", "16:9"); 
    $soporte4 = new Dvd("El Imperio Contraataca", 4, 3, "es,en","16:9"); 

    $cliente1 = new Cliente("Bruce Wayne", 23); 
    $cliente1->alquilar($soporte1); 
    $cliente1->alquilar($soporte2); 
    $cliente1->alquilar($soporte3); 

    $this->expectException(CupoSuperadoException::class);
    $cliente1->alquilar($soporte4); 
}
```


## Referències

* [Manual de PHP](https://www.php.net/manual/es/index.php)
* [Manual de OO en PHP - www.desarrolloweb.com](https://desarrolloweb.com/manuales/manual-php.html#manual68)

## Exercicis

### Objectes

301. `Persona.php`: Crea una classe `Persona` amb el seu nom, cognoms i edat.
     Encapsula les propietats mitjançant *getters/setters* i afig mètodes per a: (**Pissarra**)
     * Obtindre el seu nom complet → `getNombreCompleto(): string`
     * Saver si està jubilat o no → `estaJubilado(): bool`
302. `Persona7.php`: Còpia la classe persona i modifica-la. Afig el constructor de manera que assignem nom i cognoms mitjançant el constructor (utilitza la sintaxi de PHP7).
     Si el constructor rep un tercer paràmetre, serà l'edat de la `Persona`. Si no, se li assignarà 25 anys com a edat. 
303. `Persona8.php`: Copia la classe persona i modifica la classe per a utilitzar la sintaxi de PHP 8 de promoció de les propietats del constructor. 
304. `Persona8.php`: Modifica la classe de l'exercici anterior per afegir una constant `LIMITE_EDAT` amb el valor de la edat jubilació, i modifica el codi per a utilitzar la constant. Posa la constant en 66.
305. `Persona8.php`: Modifica la classe de l'exercici anterior, canviant la constant per una variable estàtica `limite_edat`, de manera que mitjançant la funció estatica *modificaLimite()* pugues modificar el seu valor. Per defecte se li assignarà la constant `LIMITE_EDAT`
306. `Empleado.php`: Crea un classe que herete de l'anterior i afig una propietat privada que emmagatzeme el sou i un array de nombres de telèfons.
          Afig els següents mètodes:
    * `public function anyadirTelefono(int $telefono) : void` → Afig un telèfon al array (**pissarra**)
    * `public function listarTelefonos(): string` → Mostra els telèfons separats per comes
    * `public function vaciarTelefonos(): void` → Elimina tots els telèfons
    * `public debePagarImpuestos(): bool`Que retorne un booleà indicant si deu o no pagar impostos (es paguen quan el sou és superior a 3333€)
307. `Empleado.php`: Completa-la el següent mètode amb una cadena HTML que mostre el nom complet d'un empleat dins d'un paràgraf i tots els telèfons mitjançant una llista ordenada (per a això, hauràs de crear un *getter* per als telèfons):
     * `public static function toHtml(Empleado $emp): string`
 <figure style="float: right;">
     <img src="imagenes/03/03p307.png">
     <figcaption>Ejercicio 307</figcaption>
 </figure>

308. `Persona8.php`: Crea en `Persona` el mètode estàtic `toHtml(Persona $p)` que mostrarà el nom complet de la persona dins d'un paragraf, i modifica en `Empleado` el mateix mètode `toHtml(Persona $p)`, però canvia la signatura perquè reba una `Persona` com a paràmetre.
     Per a accedir a les propietats de l'empleat amb la persona que rebem com a paràmetre, comprovarem el seu tipus:

    ``` php
    <?php
    class EmpleadoTelefono extends Empleado {
        /// resto del código


        public static function toHtml(Persona $p): string {
            if ($p instanceof Empleado) {
                // Aqui ya podemos acceder a las propiedades y métodos de Empleado
            }
        }
    }
    ```

309. `Persona8.php i Empleado.php`: 
     Afig nous mètodes que facen una representació de totes les propietats de les classes `Persona` i `Empleado`, de manera similar als realitzats en HTML, però sense que siguen estàtics, de manera que  obtinga les dades mitjançant `$this`.
     * `function public __toString(): string`

!!! tip "*Magic methods*"
    El mètode `__toString()` és un mètode màgic que s'invoca automàticament quan volem obtindre la representació en cadena d'un objecte.

310.`Worker.php`: Copia classes i canvia el nom(Person,Worker,Employee,Manager).

* Transforma `Person` a una classe abstracta on el seu mètode estàtic `toHtml(Persona $p)` haja de ser redefinit en tots els seus fills.
  * Canvia l'estructura de classes conforme al gràfic respectant tots els mètodes que ja estan fets
  * `Worker` és una classe abstracta que ara emmagatzema els `telefonos` i on `calcularSueldo` és un mètode abstracte de manera que:
    * El sou d'un `Empleat` es calcula a partir de les hores treballades i el que cobra per hora.
    * Per als `Gerents`, el seu sou s'incrementa percentualment sobre la base de la seua edat: `salari + salari*edat/100`

<figure>
   <img src="imagenes/03/03p312.png">
   <figcaption>Ejercicio 312</figcaption>
</figure>

311.`Enterprise.php`: Utilitzant les classes dels exercicis anteriors.

* Crea una classe `Enterprise` que a més del nom i la direcció, continga una propietat amb un array de `Workers`, ja siguen Employees o Managers. 
  * Afig *getters/setters* per al nom i direcció.
  * Afig mètodes per a afegir i llistar els treballadors.
     * `public function addWorker(Worker $t)`
     * `public function listWorkersHtml() : string` -> utilitza `Worker::toHtml(Person $p)`
  * Afig un mètode per a obtindre el cost total en nòmines.
     * `public function getCosteNominas(): float` -> recorre els treballadors i invoca al mètode `calcularSueldo()`.

312.`JSerializable.php`: Crea una interfície JSerializable, de manera que oferisca els mètodes:
       
* `toJSON(): string` → utilitza la funció [`json_encode(mixed)`](https://www.php.net/manual/es/function.json-encode.php). Tingues en compte que com tenim les propietats dels objectes privats, has de recórrer les propietats i col·locar-les en un mapa. Per exemple:        

``` php
   <?php
       public function toJSON(): string {
            $mapa = array()
           foreach ($this as $clave => $valor) {
               $mapa[$clave] = $valor;
           }
           return json_encode($mapa);
       }
    ?>
```

  * `toSerialize(): string` → utilitza la funció [`serialize(mixed)`](https://www.php.net/manual/es/function.serialize.php)
  * Modifica totes les classes perquè implementen la interfície creada.


## Activitat

En la següent activitat simularem una web d'intercanvi de llibres entre els usuaris de Batoi, el qual realitzarem mitjançant un desenvolupament incremental.
Utilitzarem el repositori que trobareu a l'aules per a treballar. 

!!! warning "Projecte no real"
    El següent projecte està pensat des d'un punt de vista formatiu. Algunes de les decisions que es prenen no s'han d'usar (com fer `echo` dins de les classes) o provar el codi comparant el resultat en el navegador.

Cada classe ha d'anar en un arxiu php separat. Els arxius que no contenen classes, com `index.php` han d'anar en l'arrel del projecte.

320. Crea una classe per als llibres (`Book.php`).
    
     * Afig els atributs `idUser`, `idModule` , `publisher`, `price`,`pages`,`status`,`photo`,`comments`,`soldDate`.
     * Crea el constructor que inicialitze les seues propietats. 
     * Crea el setters i els getters.
     * Crea un mètode per __toString() que mostre les dades del llibre dins d'un <div> amb la classe `book`.
     * Crea un mètode __toJson() que retorne un objecte JSON amb les dades del llibre.
     * Crea un mètode per a marcar el llibre com a venut.

321. Crea un classe per als usuaris (`User.php`).
    
     * Afig els atributs  `email`, `password`, `nick`.
     * Crea el constructor que inicialitze les seues propietats. 
     * Crea el setters i els getters.
     * Crea un mètode per __toString() que mostre les dades de l'usuari dins d'un <div> amb la classe `user`.
     * Crea un mètode per a gestionar la complexitat de la contrasenya. La contrasenya ha de tindre almenys 8 caràcters, una lletra majúscula, una minúscula i un número. Si no compleix aquestes condicions, llança una excepció `WeekPasswordException`.

323. Crea un classe per als cicles (`Course.php`).
     * Afig els atributs `cycle`,`idFamily`,`vliteral`,`cliteral`
     * Crea el constructor que inicialitze les seues propietats. 
     * Crea el setters i els getters.
     * Crea un mètode per __toString() que mostre les dades del cicle dins d'un <div> amb la classe `cycle`.
     * Crea un mètode per __toJson() que retorne un objecte JSON amb les dades del cicle.
     
324. Crea un classe per al Modul (`Module.php`).
    
     * Afig els atributs `code`,`cliteral`,`vliteral`,`idCycle`
     * Crea el constructor que inicialitze les seues propietats. 
     * Crea el setters i els getters.
     * Crea un mètode per __toString() que mostre les dades del mòdul dins d'un <div> amb la classe `module`.
     * Crea un mètode per __toJson() que retorne un objecte JSON amb les dades del mòdul.

325. Importa les classes anteriors en `index.php` i crea un array associatiu per a totes les clases, on l'index de l'array serà l'equivalent a la key una taula.
326. Importa dels fitxers [`modulesBook`](recursos/modulesbook.csv) i [`coursesBook`](recursos/coursesbook.csv) (pots mirar [ací](https://cipfpbatoi.github.io/dwes2324/05accesoDatos.html#acces-a-fitxers) com fer-ho, i ompli els arrays corresponents, savent que el primer camp de cada entrada és la key de l'array. Si es produix una errada es llança una exempció `InvalidFormatException` per a mostrar un missatge però s'ha de continuar intentant important la resta.
326. Crea un usuari i un llibre d'eixe usuari. Mostra per pantalla el llibre i l'usuari.
327. Crea un directori api i afegix un fitxer `book.php` que acepte un paràmetre `id` i mostre el llibre o usuari corresponent en format JSON. Si no existeix, llança una exempció `NotFoundException`.

328. Anem a utilitzar el autoload de les classes. 

        * Canvia de branca `Second-Deliver`. 
        * Posa tots els arxius de classes en una carpeta `app` i les exempcions dins d'una carpeta `Exempcions` dins de `app`.
        * Crea el fixer `autoload.php` per a que busque en eixa carpeta. 
        * Posa un namesapce `BatBook` a totes les classes. 
        * Utilitza `use` per a importar les classes en `index.php` i `book.php`. 

``` php
<?php
spl_autoload_register( function( $nombreClase ) {
    $ruta = $nombreClase.'.php';
    $ruta = str_replace("BatBook", "app", $ruta); // Sustituimos las barras
    $ruta = str_replace("\\", "/", $ruta); // Sustituimos las barras
    include_once $ruta;
} );
```