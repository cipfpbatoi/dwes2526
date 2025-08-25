# SA4 – Accés segur i estructurat a bases de dades amb Laravel

??? abstract "Duració i criteris d'evaluació"

    Duració estimada: 16 hores

    <hr />

    | Resultat d'aprenentatge  | Criteris d'avaluació  |
    | ------                    | -----                |
    | RA6.-Desenvolupa aplicacions web d'accés a magatzems de dades, aplicant mesures per a mantindre la seguretat i la integritat de la informació. | a) S'han analitzat les tecnologies que permeten l'accés mitjançant programació a la informació disponible en magatzems de dades. b) S'han creat aplicacions que establisquen connexions amb bases de dades. c) S'ha recuperat informació emmagatzemada en bases de dades. d) S'ha publicat en aplicacions web la informació recuperada. e) S'han utilitzat conjunts de dades per a emmagatzemar la informació. f) S'han creat aplicacions web que permeten l'actualització i l'eliminació d'informació disponible en una base de dades. g) S'han provat i documentat les aplicacions web.
 

##  SA4.1  Connexió a la base de dades


### Configuració `.env` i `config/database.php`

- Laravel llegeix la connexió a la BD des del fitxer `.env` i el configura a `config/database.php`. Pots veure tots els paràmetres disponibles i com es gestionen via `env()` :contentReference[oaicite:1]{index=1}.
- Opcionalment, es pot usar una sola cadena URL (`DB_URL`) que defineix host, usuari, contrasenya i base de dades :contentReference[oaicite:2]{index=2}.
- **Ex. connexió MySQL bàsica**:
```dotenv
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=nom_base
DB_USERNAME=usuari
DB_PASSWORD=contrasenya
 ```
- També es pot configurar múltiples connexions dins config/database.php, per exemple per separar connexions de lectura i escriptura.

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
