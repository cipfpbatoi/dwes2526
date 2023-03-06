# Exercicis de recuperació de PHP

## Exercici 1

### Part 1

Crea la següent estructura de fitxers dins de la carpeta /src:

classes/
views/
config/

### Part 2 

Posa els [paràmetres de connexiò a la base de dades](06accesoDatos.md#fitxer-de-configuració-de-la-BD) en un fitxer de configuració que es trobi a la carpeta /config. 

### Part 3

Crea una classe [Connection](03phpoo.md) que es trobi a la carpeta /classes i que continga en el constructor el codi per a fer la connexió a
la base de dades amb el [paràmetres](02php.md#biblioteca-de-funcions) donats en la part2. Utiliza el [composer](05herramientas.md#composer) per a que eixa classe es puga importar amb use 

Crea un mètode insert que reba com a paràmetres el nom de la taula i un array associatiu i que [inserte](06accesoDatos.md#Sentències-preparades) a la base de dades els valors del array

### Part 4

Crea una vista que continga un formulari amb el camps per a inserir un nou usuari a la base de dades.

### Part 5

Crea un fitxer [register.php](04web.md#formularis) que continga el codi per cridar a la vista i per a fer la connexió a la base de dades i que inserte un nou usuari.




