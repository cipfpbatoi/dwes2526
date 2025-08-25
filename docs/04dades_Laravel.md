# SA4 – Accés segur i estructurat a bases de dades amb Laravel

??? abstract "Duració i criteris d'evaluació"

    Duració estimada: 16 hores

    <hr />

    | Resultat d'aprenentatge  | Criteris d'avaluació  |
    | ------                    | -----                |
    | RA6.-Desenvolupa aplicacions web d'accés a magatzems de dades, aplicant mesures per a mantindre la seguretat i la integritat de la informació. | a) S'han analitzat les tecnologies que permeten l'accés mitjançant programació a la informació disponible en magatzems de dades.<br/> b) S'han creat aplicacions que establisquen connexions amb bases de dades.<br/> c) S'ha recuperat informació emmagatzemada en bases de dades.<br/> d) S'ha publicat en aplicacions web la informació recuperada.<br/> e) S'han utilitzat conjunts de dades per a emmagatzemar la informació.<br/> f) S'han creat aplicacions web que permeten l'actualització i l'eliminació d'informació disponible en una base de dades.<br/> g) S'han provat i documentat les aplicacions web.
 

##  SA4.1  Connexió a la base de dades
 
 
### 🔧 Configuració de la base de dades en Laravel

Per a poder treballar amb bases de dades en Laravel, el primer pas és configurar l’accés al sistema gestor de base de dades (SGBD) que vulguem utilitzar. En aquest cas, farem servir MySQL.

 
#### 📁 1. Fitxer `.env` i separació de configuracions

Laravel utilitza un sistema de variables d'entorn, que permet separar la configuració segons la màquina, l'entorn (desenvolupament, producció...), o l’usuari.

Aquesta configuració s’indica al fitxer `.env` que està a l’arrel del projecte. Allí definirem el tipus de connexió, el servidor, el nom de la base de dades, l’usuari i la contrasenya.
 

#### ⚙️ 2. Fitxer `config/database.php`

Aquest fitxer defineix com Laravel interpreta aquestes variables del `.env`. El valor per defecte sol ser MySQL, però pot canviar-se si cal.

A més, aquest fitxer conté la configuració detallada per a cada tipus de base de dades (MySQL, PostgreSQL, SQLite...). Els valors que trobem estan enllaçats amb les variables del `.env`.
 
#### 🔐 3. Contrasenya i paràmetres necessaris

Perquè Laravel puga connectar-se correctament a la base de dades, és necessari configurar correctament els valors següents en el fitxer `.env`:

- L’adreça del servidor.
- El nom de la base de dades.
- L’usuari.
- La contrasenya d’accés.

En un entorn local, l’adreça del servidor sol ser “localhost”.
 
#### 🧱 4. Crear la base de dades (fora de Laravel)

Laravel pot crear taules, relacions i introduir dades, però la base de dades com a contenidor l’has de crear prèviament de forma manual.

Pots fer-ho mitjançant una eina gràfica com phpMyAdmin o bé per línia de comandes, depenent de les eines disponibles al teu entorn de treball.

 
###  Migracions bàsiques: crear taules i columnes
 
- Models Eloquent: creació i configuració inicial
- Seeders i Factories: generació de dades de prova

### 4.2 Primeres operacions amb Eloquent
- `create`, `update`, `delete`, `all()`, `find()`
- Relacions bàsiques (1:1, 1:N, N:N)
- Eager loading (`with()`)
- Paginació

### 4.3 Arquitectura escalable per a CRUDs (patrons OOP)
- Introducció als principis SOLID
- Patrons Laravel recomanats: Repository, Service, Factory
- Estructura recomanada: `Controller → Service → Repository → Model`
- Exemple complet amb `Producte`

### 4.4 Autenticació, hashing i autorització
- Laravel Breeze: registre, login, logout
- Protecció de rutes amb `auth`
- Hashing automàtic de contrasenyes
- Middleware i polítiques (`Policy`) per a autorització

### 4.5 Formularis amb seguretat i feedback
- Validació amb `FormRequest`
- Ús de `@csrf`, `@method`, `old()`, `@error`
- Missatges flash amb `session()->flash()`
- UX i manteniment d'estat

### 4.6 Exercici integrador: Futbol Femení CRUD
- Migració i model `EquipFutbol`
- Arquitectura amb Service i Repository
- Formularis validats i control d’accés amb auth
- Feedback i proves bàsiques

### 4.7 Extensió opcional: CRUD dinàmic amb Livewire
- Introducció a Livewire
- Creació de component CRUD
- Connexió amb Service i Repository
- Millora UX sense JS explícit
