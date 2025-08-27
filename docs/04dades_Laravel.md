# SA4 – Accés segur i estructurat a bases de dades amb Laravel

??? abstract "Duració i criteris d'evaluació"

    Duració estimada: 16 hores

    ---

    | Resultat d'aprenentatge  | Criteris d'avaluació  |
    | ------                    | -----                |
    | RA6.-Desenvolupa aplicacions web d'accés a magatzems de dades, aplicant mesures per a mantindre la seguretat i la integritat de la informació. | a) S'han analitzat les tecnologies que permeten l'accés mitjançant programació a la informació disponible en magatzems de dades.<br/> b) S'han creat aplicacions que establisquen connexions amb bases de dades.<br/> c) S'ha recuperat informació emmagatzemada en bases de dades.<br/> d) S'ha publicat en aplicacions web la informació recuperada.<br/> e) S'han utilitzat conjunts de dades per a emmagatzemar la informació.<br/> f) S'han creat aplicacions web que permeten l'actualització i l'eliminació d'informació disponible en una base de dades.<br/> g) S'han provat i documentat les aplicacions web.
 
## SA 4.1 Connexió a la base de dades

### 🔧 Configuració de la base de dades en Laravel

Per a poder treballar amb bases de dades en Laravel, el primer pas és configurar l’accés al sistema gestor de base de dades (SGBD) que vulguem utilitzar. En aquest cas, farem servir MySQL.
 
#### 📁 1. Fitxer `.env` i separació de configuracions

```env
DB_CONNECTION=mysql
DB_HOST=localhost
DB_PORT=3306
DB_DATABASE=nom_base_de_dades
DB_USERNAME=usuari
DB_PASSWORD=contrasenya
```
 