# Exercicis de recuperació de PHP

## DAMERO

### Part 1. Pintar Tauler

#### Exercici 1.1 Pintar Tauler

Fes un programa que pinte un tauler de damas. El tauler ha de ser de 8x8 i ha de ser de colors. Pots utilitzar la següent taula de colors:

```css
body {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background-color: #f0f0f0;
}

.taula-de-dames {
    display: grid;
    grid-template-columns: repeat(8, 50px);
    grid-template-rows: repeat(8, 50px);
    gap: 2px;
}

.taula-de-dames div {
    width: 50px;
    height: 50px;
    display: flex;
    justify-content: center;
    align-items: center;
}

.negre {
    background-color: #444;
}

.blanc {
    background-color: #fff;
}
```
Guarda el fitxer com a `tauler.view.php` referència-lo des de `index.php`.

#### Exercici 1.2 Classe Tauler

Crea una classe `Tauler` que siga capaç de pintar el tauler de la forma que s'ha indicat en l'exercici anterior. La classe ha de tindre un mètode `__toString` que pinte el tauler.

A més la classe tauler acceptarà el paràmetre `tamany` que per defecte serà 8. La classe anirà dins d'un  directori `classes`.

Utilitza esta classe des de la vista tauler per a pintar el tauler.

### Exercici 1.3 Classe casella

Crea una classe `Casella` que represente una casella del tauler. La classe tindrà un atribut `color` que serà `blanc` o `negre` i un mètode `__toString` que pintarà la casella.
A més tindrà un atribut  `ocupant` que serà `null` si està buida, o `jugador1`, `jugador2`.

### Exercici 1.3 Posició inicial

En la classe `Tauler`, crea un mètode `taulerInicial` per inicialitzar el tauler amb fitxes per als dos jugadors en les posicions correctes. 

Hauras de crear un array en el constructor de la classe `Tauler` per a guardar les caselles.

```php
class Tauler {
    private $tamany; // Tamany del tauler, típicament 8 per a dames
    private $caselles;

    public function __construct($tamany = 8) {
        $this->tamany = $tamany;
        $this->inicialitzarCaselles();
    }
```
Crea un mètode per obtenir les caselles del tauler.

Utilitza aquest .css actualitzat.

```css
body {
display: flex;
justify-content: center;
align-items: center;
height: 100vh;
background-color: #f0f0f0;
}

.taula-de-dames {
display: grid;
grid-template-columns: repeat(8, 60px); /* Ajusta la mida de les caselles */
grid-template-rows: repeat(8, 60px);
gap: 2px;
}

.negre {
background-color: #769656; /* Color verd fosc per a les caselles jugables */
}

.blanc {
background-color: #eeeed2; /* Color clar per a les caselles no jugables */
}

.taula-de-dames div.negre, .taula-de-dames div.blanc {
width: 60px; /* Ajusta la mida de les caselles */
height: 60px;
display: flex;
justify-content: center;
align-items: center;
position: relative; /* Permet posicionament absolut dins */
}

.taula-de-dames div.negre::before, .taula-de-dames div.blanc::before {
content: '';
width: 80%; /* Ajusta la mida del marcador de la fitxa */
height: 80%; /* Ajusta la mida del marcador de la fitxa */
border-radius: 50%;
position: absolute;
}

.taula-de-dames div.negre.fitxa-jugador1::before {
background-color: #fff; /* Color de les fitxes del jugador 1 */
box-shadow: 0 2px 4px rgba(0,0,0,0.3);
}

.taula-de-dames div.negre.fitxa-jugador2::before {
background-color: #000; /* Color de les fitxes del jugador 2 */
box-shadow: 0 2px 4px rgba(255,255,255,0.3);
}
```

### Exercici 1.4 Moviment de fitxes

Crea un mètode `moureFitxa` en la classe `Tauler` que reba la posició inicial i la posició final de la fitxa a moure. El mètode comprovarà si el moviment és vàlid i si ho és, moure la fitxa.
S'ha de comprovar que les coordenades estiguen dins del tauler i que la casella de destí estiga lliure.
Podrem comprovar que funciona modificant el fitxer `index.php` de la següent manera:
    
```php
$tauler = new Tauler();
if ($tauler->moureFitxa(2, 1, 3, 0)) {
    echo "Moviment realitzat amb èxit!";
} else {
    echo "Moviment invàlid.";
}
include_once './views/tauler.view.php';

### 


