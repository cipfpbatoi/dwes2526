# Exercicis de recuperació de PHP

## Exercici 1

### Part 1

Crea la següent estructura de fitxers dins de la carpeta /src:

classes/
views/
config/

### Part 2 

Posa els [paràmetres de connexiò a la base de dades](06accesoDatos.md#fitxer-de-configuracio-de-la-bd) en un fitxer de configuració que es trobi a la carpeta /config. 

### Part 3

Crea una classe [Connection](03phpoo.md) que es trobi a la carpeta /classes i que continga en el constructor el codi per a fer la connexió a
la base de dades amb el [paràmetres](02php.md#biblioteca-de-funcions) donats en la part2. Utiliza el [composer](05herramientas.md#composer) per a que eixa classe es puga importar amb use 

Crea un mètode insert que reba com a paràmetres el nom de la taula i un array associatiu i que [inserte](06accesoDatos.md#sentencies-preparades) a la base de dades els valors del array

### Part 4

Crea una vista que continga un formulari amb el camps per a inserir un nou usuari a la base de dades.

### Part 5

Crea un fitxer [register.php](04web.md#formularis) que continga el codi per cridar a la vista i per a fer la connexió a la base de dades i que inserte un nou usuari.

## Exercici 2

### Part 1

Crea una classe [User](03phpoo.md) que es trobe a la carpeta /classes i que continga els atributs i els mètodes necessaris per a gestionar els usuaris de la base de dades.

### Part 2

Crea un mètode login que reba com a paràmetres el nom d'usuari i la contrasenya i que [consulte](06accesoDatos.md#sentencies-preparades) a la base de dades si existeix un usuari amb aquests valors i que retorni un objecte User si existeix o null si no existeix.

### Part 3

Crea un fitxer [login.php] que mostra la vista de login i s'encarregue de gestionar la petició de l'usuari de la següent [manera](04web.md#autenticaci-dusuaris):
   * Si les credencials d'usuari són correctes que guarde en una variable de [sessió](04web.md#sessio) l'objecte User que retorna el mètode login i vaja a index.php.
   * Si les credencials no són correctes que torne a mostrar el login mantenint el nom possat [inicialment](04web.md#validacio).

### Part 4

Crea un fitxer [index.php] que continga el codi per a mostrar un missatge de benvinguda si l'usuari està loguejat o retorne a la pàgina de login si no ho està.

## Exercici 3

### Part 1

Crea una classe [Product](03phpoo.md) que es trobe a la carpeta /classes i que continga els atributs i els mètodes necessaris per a gestionar els productes de la base de dades.

### Part 2

Crea un mètode getAll que [consulte](06accesoDatos.md#sentencies-preparades) a la base de dades tots els productes i que retorni un array d'objectes Product.

### Part 3

Crea un fitxer [products.php] que continga el codi per a mostrar tots els productes de la base de dades.

### Part 4

Crea un fitxer [product.php] que continga el codi per a mostrar un producte concret de la base de dades.

### Part 5

Crea un fitxer [newProduct.php] que continga el codi per a mostrar un formulari per a inserir un nou producte a la base de dades.

## Exercici 4

### Part 1

Crea un fixert [updateProduct.php] que continga el codi per a mostrar un formulari i per a modificar un producte de la base de dades.

### Part 2

Crea un fitxer [deleteProduct.php] que continga el codi per a eliminar un producte de la base de dades.

### Part 3

Pagina els resultats de la consulta a la base de dades de manera que només es mostren 10 productes per pàgina. Ha d'haver també un enllaç per a anar a la pàgina següent i un altre per a anar a la pàgina anterior.

### Part 4

Crea un fitxer [logout.php] que continga el codi per a esborrar la variable de sessió i que redirigeixi a la pàgina de login.

### Exercici 5

### Part 1

Anem a crear una pagina [api/book.php] que ens retorni un json amb tots els llibres de la base de dades. Pots utilitzar el següent exemple per a fer-ho:

```php
<?php

// Executar consulta SELECT per obtenir totes les dades de la taula "books"
$sql = "SELECT * FROM books";
$result = mysqli_query($conn, $sql);

// Crear un array per a les dades de tots els llibres
$books = array();
while ($row = mysqli_fetch_assoc($result)) {
    $books[] = $row;
}

// Convertir les dades en format JSON i retornar-les com a resposta HTTP
header('Content-Type: application/json');
echo json_encode($books);

?>
```

### Part 2

Anem a afegir a la pàgina [api/book.php] un paràmetre que ens permeti obtenir un llibre concret. Hauràs de comprovar l'existència de la variable per discernir si l'usuari vol obtenir tots els llibres o un llibre concret. 

### Part 3

Anem a afegir a la pàgina [api/book.php] els mètodes POST, PUT i DELETE per a poder afegir, modificar i eliminar llibres de la base de dades. Pots utilitzar el següent exemple per a fer-ho:

```php
<?php

// Comprovar el mètode de petició HTTP
if ($_SERVER['REQUEST_METHOD'] === 'GET') {
    // Executar una consulta SELECT per obtenir les dades de la taula "books"
    // i mostrar-les en una taula HTML
} elseif ($_SERVER['REQUEST_METHOD'] === 'POST') {
    
} elseif ($_SERVER['REQUEST_METHOD'] === 'PUT') {
       
} elseif ($_SERVER['REQUEST_METHOD'] === 'DELETE') {
        // Executar una consulta DELETE per esborrar un registre amb un determinat "id"
}


```

### Part 4

Canvia el que necessites per tal que quan es produïsca una errada es retorni un codi d'estat HTTP adequat.

## Exercici 6

### Part 1

Possa validació als formularis de manera que no es puguin introduir valors no vàlids.

### Part 2

Fes que despres de una validació incorrecta es mostri el formulari amb els valors que ja havia introduït l'usuari.

### Part 3

Fes que despres de una validació incorrecta es mostri un missatge d'error.

## Exercici 7

### Part 1

Crea un classe [Cart](03phpoo.md) que es trobe a la carpeta /classes i que continga els atributs i els mètodes necessaris per a gestionar el carret de la compra.

### Part 2

Crea un fitxer [cart.php] que continga el codi per a mostrar el contingut del carret de la compra de l'usuari validat.

## Exercici 8

### Part 1

Crear els fitxers adients en la carpeta /api per a gestionar les peticions que utilitzes en la part de client.
