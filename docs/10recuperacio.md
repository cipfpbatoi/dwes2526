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

