## Exercici 1 (1,5p)

Genera una matriu de números aleatoris entre 1 i 500 no repetits de 10x10 i mostra-los en una taula, afegint una fila i una columna on es mostre la suma de cada fila i de cada columna.
Els numeros par estaran en blau i els senars en vermell.

## Exercici 2 (1,5p)

Modifica la capçalera del batoiBook per tal que done la benvinguda a l'usuari de la següent forma:
Si és la primera vegada que entra, li dira 'Benvingut/uda per primera vegada'.
En cas contrari li dira 'Benvingut/uda, la teua darrera visita va ser...', i la data amb format "Y-m-d H:i:s".
No es pot utilitzar la BBDD per guardar la informació.

## Exercici 3 (1p)

Crea la classe `sales` que gestione les transaccions entre usuaris. Aquesta classe tindrà els següents mètodes:

* `__construct($idBook,$idUser)` constructor que rep l'identificador de la transacció.
* `getUser()` retorna l'objecte usuari que ha realitzat la transacció.
* `getBook()` retorna l'objecte llibre que s'ha transaccionat.
* `save()` guarda la transacció a la base de dades.
* `delete()` elimina la transacció de la base de dades.
* `getSales($idUser)` retorna un array amb els llibres venuts per l'usuari passat per paràmetre.

## Exercici 4 (1p)

Crea la pàgina `api/sales.php` que gestione les peticions POST que li arriben y done d'alta la venda en la BBDD.

## Exercici 5 (5p)

Fes un CRUD de la taula cicles (courses), tenint em compte que tots els camps són obligatoris.
Afegix un camp `administrador` (boolean) a la taula users. Fes a un usuari administrador.
Soles l'usuari administrador podrà fer el CRUD de cicles. Implementa'l.
