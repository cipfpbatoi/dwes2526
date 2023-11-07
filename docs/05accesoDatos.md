<style>
    img { margin: 20px 0; border-radius: 8px; }

    .alert { color: #BD1550; }
    .warning { color: #E97F02; }
    .success { color: #8A9B0F; }

    .center { text-align: center; }
    .right { text-align: right; }

    .img-small { max-width: 200px; margin: auto; }
    .img-medium { max-width: 400px; margin: auto; }
    .img-large { max-width: 800px; margin: auto; }

    .leyenda {
        font-size: small;
        margin: 10px 0;
    }
</style>

# Accès a dades
<!-- 
> Duració estimada: 14 hores
 -->
En aquesta unitat aprendrem a accedir a dades que es troben en un servidor; recuperant, editant i creant aquestes dades a través d'una base de dades.

A través de les diferents capes o nivells, de les quals 2 d'elles ja coneixem (*Nginx*, *PHP*) i *MySQL* la que estudiarem en aquest tema.

<div class="center img-large">
    <img src="imagenes/06/06-bbdd-arquitectura-3-niveles.png">
</div>

## Instal·lació
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

## Estructura d'una base de dades

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

## SQL

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

## phpMyAdmin

<div class="center img-medium">
    <img src="imagenes/06/06-bbdd-phpMyAdmin-logo.png">
</div>

Aquest programari funciona sota Ngingx i PHP i és més que res una interfície web per a gestionar les bases de dades que tinguem disponibles en el nostre servidor local. Molts **hostings* ofereixen aquesta eina per defecte per a poder gestionar les BBDD que tinguem configurades sota el nostre compte.

### Creant una base de dades dins de phpMyAdmin

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

### Opcions en phpMyAdmin

Quan seleccionem una base de dades de la llista, el sistema ens mostra diverses pestanyes amb les quals interactuar amb la base de dades en qüestió:

- `Estructura`: Podem veure les diferents taules que consoliden la nostra base de dades

- `SQL`: Per si volem injectar codi SQL perquè el sistema l'interprete

- `Buscar`: Serveix per a buscar per termes, en la nostra base de dades, aplicant diferents filtres de cerca

- `Generar consulta`: semblança a SQL però d'una manera més gràfica, sense haver de saber res del llenguatge

- `Exportar i importar`: Com el seu nom indica, per a fer qualsevol de les 2 operacions sobre la base de dades

- `Operacions`: Diferents opcions avançades per a realitzar en la nostra base de dades, de la qual destacarem l'opció *Cotejamiento* on podrem canviar el *cotejamiento* de la nostra taula però <span class="alert">*ULL AMB ACÔ* perquè podem eliminar dades sense voler, ja que en canviar el *cotejamiento* podem suprimir caràcters no suportats pel nou *cotejamiento*</span>

No aprofundirem en la resta d'opcions però, en la pestanya **Més** existeix l'opció **Dissenyador** per a poder editar les relacions entre taules d'una manera gràfica (punxant i arrossegant) que veurem més endavant.

## PHP Data Objects :: PDO

*PHP Data Objects* (o *PDO*) és un *driver* de *PHP* que s'utilitza per a treballar sota una interfície d'objectes amb la base de dades. Hui dia és el que més s'utilitza per a manejar informació des d'una base de dades, ja siga relacional o no relacional.

Per establir la connexió en la bbdd utilitzarem:

``` php
<?php
    $conexion = new PDO('mysql:host=localhost; dbname=dwes', 'dwes', 'abc123');
```

A més, amb *PDO* podem usar les excepcions amb *try catch* per a gestionar els errors que es produïsquen en la nostra aplicació, per a això, com féiem abans, hem d'encapsular el codi entre blocs *try / catch*.

``` php
<?php

    $dsn = 'mysql:dbname=prueba;host=127.0.0.1';
    $usuario = 'usuario';
    $contraseña = 'contraseña';

    try {
        $mbd = new PDO($dsn, $usuario, $contraseña);
        $mbd->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
    } catch (PDOException $e) {
        echo 'Falló la conexión: ' . $e->getMessage();
    }
```
En primer lloc, creem la connexió amb la base de dades a través del constructor *PDO* passant-li la informació de la base de dades.

En segon lloc, establim els paràmetres per a manejar les exempcions, en aquest cas hem utilitzat:

- `PDO::ATTR_ERRMODE` indicant-li a PHP que volem un reporte d'errors.
- `PDO::ERRMODE_EXCEPTION` amb aquest atribut obliguem al fet que llance exempcions, a més de ser l'opció més humana i llegible que hi ha a l'hora de controlar errors.

Qualsevol error que es llance a través de **PDO**, el sistema llançarà una <span class="alert">**PDOException**</span>.

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
    //  ▒▒▒▒▒▒▒▒ Borrando con parámetros ▒▒▒▒▒▒▒▒

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
    $sentencia -> setFetchMode(PDO::FETCH_CLASS, "Tienda");
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

## Login & Password

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

## QueryBuilder

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


## Accès a fitxers

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


## Exercisis

### PDO

601. Crea una nova base de dades amb el nom `batoiBook` i cotejamiento de dades `utf8mb4_unicode_ci`. Importa el fitxer [`batoiBook.sql`](recursos/batoiBook.sql) que trobaràs en la carpeta `sql` d'aquesta unitat.
602. Crea una carpeta config i dins d'ella un fitxer `database.inc.php` on establisques les constants de connexió amb la base de dades.
603. Crea una classe Connection com a model de connexió amb la base de dades. Aquesta classe tindrà un mètode `__construct()` que inicialitzarà la connexió amb la base de dades i un mètode `getConection()` que retornà la connexió.

``` php
<?php
namespace batBook;

use PDO;
use PDOException;

include_once($_SERVER['DOCUMENT_ROOT']."/config/database.inc.php");

class Connection
{

    private $connection;

    ...

```

604. Anem a canviar la classe Module per a que carregue les dades des de la BD i no des de l'array:

    * Eliminarem el constructor de la classe Module
    * Afegim el mètode static `getModulesInArray()` que retornarà un array associatiu d'objectes del la classe Modules, amb clau de l'array el camp Code de la tupla de la taula Modules.
           
        * Haurem de crear un objecte de la classe Connection.
        * Utilitzarem sentencies preparades
        * Utilitzarem  $sentence -> setFetchMode(PDO::FETCH_CLASS  , Module::class); per tal de retornar objectes de la classe Module.

    * Modificarem el fitxer load per a llevar tota referència a la variable $modules. 
    * Substituirem la crida a la funció `getModulesInArray()` per a que carregue les dades des de la BD en els llocs que abans utitlizaba la variable $modules.

605. Anem a afegir un metode nou a la classe Book per tal de guardar les dades del llibre en la BD. Aquest metode tindrà el nom de `save()` i serà el responsable de guardar les dades del llibre en la BD. Per a això haurem de:

    * Crear un objecte de la classe Connection.
    * Utilitzar sentencies preparades.
    * Utilitzar el metode `lastInsertId()` per a recuperar el codi del llibre que s'ha insertat.
    * Utilitzar el metode `execute()` per a executar la sentencia preparada.

606. Transforma el registre.php per a guardar les dades d'usuari en la BD.
607. Transforma el login.php per a comprovar les dades d'usuari en la BD.
608. Crea la classe QueryBuilder i copia-la dels apunts. Modifica els exercicis anterior per tal d'utilitzar el QueryBuilder.


## Activitats

### BatoiBook

610. Anem a crear la pàgina `myBooks.php` on es mostren els llibres que ha donat d'alta cada usuari. Per a aixó:
       
    * Crea la pàgina `myBooks.php` que mostrarà els llibres que ha donat d'alta l'usuari, en format taula.
    * Fes que es mostre el nom del mòdul i no el codi.
    * El darrer element de cada fila seràn els botons per a vore, modificar i eliminar el llibre.
    * Crea un enllaç en la capçalera per anar a myBooks.php sempre que l'usuari estiga autenticat.
    * Protegueix la pàgina per a que sols es puga accedir si l'usuari està autenticat.

611. Completa en el  `QueryBuilder.php` els mètodes que falten. Modificar els exercisis anteriors per utilitzar el QueryBuilder.
612. Crea la pàgina `showBook.php?id=` per a mostrar les dades d'un llibre. 
     
    * Crea el mètode static `find($id)` en la classe Book
    * Crea la vista `views/book/show.view.php` que mostre el llibre, amb capçalera.
     
613. Crea la pàgina `editBook.php?id=` per a modificar les dades d'un llibre. Després redirigirà a myBooks.php.

    * Modifica el mètode save() per a que actualitze les dades del llibre, si el llibre ja existeix
    * Fes la vista `views/book/edit.view.php` que mostre el formulari amb les dades del llibre a modificar.
    * Fes que el formulari redirisca a `updateBook.php` on s'actualitzen les dades del llibre. Si no es carrega foto quedarà la que hi ha.
    * El id del llibre no es pot modificar (utilitza un camp ocult per passar-lo).

614. Crea la pàgina `deleteBook.php?id=` per a eliminar un llibre. Després redirigirà a myBooks.php.
615. Crea el directori errors i dins la pàgina `not-found.php`. Fes que quan no es trobe un llibre en les pàgines anteriors es redirisca a la pàgina `not-found.php`.
