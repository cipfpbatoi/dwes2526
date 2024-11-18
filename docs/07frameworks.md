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

# Frameworks PHP. Laravel

> Duració estimada: 16hores

## INTRODUCCIÓ ALS FRAMEWORKS PHP I LARAVEL

### Frameworks

Un **framework** és una eina que proporciona una estructura base per al desenvolupament d'aplicacions, permetent estandarditzar el codi i agilitzar processos comuns com la connexió a bases de dades, l'organització del codi i la gestió de rutes. En el cas dels **frameworks PHP**, la majoria segueixen el patró **MVC** (Model-Vista-Controlador) i ofereixen eines per a simplificar tasques complexes, com la validació de dades o la creació de serveis web.

Els frameworks moderns com **Laravel**, **Symfony** i **Slim** ofereixen avantatges significatius, com la modularitat, la seguretat integrada i una comunitat activa. Utilitzar un framework pot ajudar a:
- **Accelerar el desenvolupament.**
- **Estandarditzar el codi i bones pràctiques.**
- **Facilitar el manteniment i l'escalabilitat.**

#### Exemples de frameworks PHP actuals

A continuació, es presenten els frameworks PHP més rellevants avui dia:

- **Laravel** (2011): És el framework més popular per la seva sintaxi clara, funcionalitats modernes i una comunitat vibrant. Ideal per a projectes de qualsevol mida, gràcies a característiques com el sistema de rutes, Eloquent ORM, i eines com Sail i Vite.

- **Symfony** (2005): És un framework molt robust i altament modular. Es recomana per a aplicacions empresarials d'alta complexitat. És la base de molts components utilitzats en altres frameworks, inclòs Laravel.

- **Slim** (2010): És un microframework lleuger, ideal per a aplicacions petites o APIs RESTful. Ofereix una gran flexibilitat amb mínim consum de recursos.

- **Phalcon** (2012): Escrit en C, ofereix un rendiment excel·lent. Tot i no ser tan popular com Laravel o Symfony, és conegut pel seu baix consum de memòria.

#### Com triar un framework

No hi ha un framework perfecte; l'elecció depèn de les necessitats del projecte:
- **Laravel:** Si busques rapidesa, facilitat d'ús i suport ampli, Laravel és l'elecció ideal.
- **Symfony:** Si el projecte requereix alta personalització i escalabilitat, Symfony és una millor opció.
- **Slim o Phalcon:** Si només necessites un backend lleuger, opta per Slim o Phalcon.

### Per què Laravel és una bona opció?

Laravel destaca per:
- Una sintaxi neta i expressiva.
- L'ús del patró **MVC**, que facilita la separació de la lògica i la presentació.
- Un ecosistema extens, incloent eines com **Artisan CLI**, **Eloquent ORM** i **Blade**.
- Solucions modernes per a autenticació (**Sanctum**, **Passport**).
- Suport natiu per APIs RESTful.
- Gran documentació i tutorials (ex. Laracasts).

En projectes moderns, Laravel és la primera opció gràcies a la seva constant evolució i la seva capacitat d'adaptar-se a les necessitats dels desenvolupadors.
 
### Característiques Laravel

**Laravel** és un framework de codi obert per al desenvolupament d'aplicacions web en PHP que posseeix una sintaxi simple, expressiva i elegant. Va ser creat en 2011 per Taylor Otwell, inspirant-se en **Ruby on Rails i Symfony**, dels quals ha adoptat els seus principals avantatges.

Laravel facilita el desenvolupament simplificant el treball amb tasques comunes com l'autenticació, el enrutamiendo, gestió sessions, l'emmagatzematge en caché, etc. Algunes de les principals característiques i avantatges de Laravel són:

* Esta dissenyat per a desenvolupar sota el patró **MVC** (model - vista - controlador), centrant-se en la correcta separació i modularització del codi. El que facilita el treball en equip, així com la claredat, el manteniment i la reutilització del codi.
* Eloquent, el ORM de Laravel, fa que treballar amb bases de dades sigui més senzill i intuïtiu, especialment en la gestió de relacions complexes.
* Permet la gestió de **bases de dades** i la manipulació de taules des de codi, mantenint un control de versions de les mateixes mitjançant el seu sistema de **Migracions**.
* Utilitza un **sistema de plantilles** per a les vistes anomenat **Blade**, el qual fa ús de la cache per a donar-li major velocitat. Blade facilita la
  creació de **vistes** mitjançant l'ús de layouts, herència i seccions.
* Facilita l'extensió de funcionalitat mitjançant paquets o **llibreries externes**. D'aquesta forma és molt senzill afegir paquets que ens
  faciliten el desenvolupament d'una aplicació i ens estalvien molt temps de programació.
* Incorpora un **intèrpret de línia de comandos** anomenat **Artisan** que ens ajudarà amb un munt de tasques rutinàries com la creació de
  diferents components de codi, treball amb la base de dades i migracions, gestió de rutes, cachés, cues, tasques programades, etc.
* Laravel Jetstream ofereix una implementació robusta per a l'autenticació i la gestió de sessions. Laravel Sanctum es utilitza per a APIs tokenitzades, proporcionant una solució elegant per a la autenticació d'APIs.
* Laravel inclou proteccions de seguretat com la protecció CSRF, xifrat segur de contrasenyes i defenses contra injeccions SQL, garantint un entorn segur per al desenvolupament d'aplicacions web.
* Amb Laravel, és possible construir arquitectures de microserveis eficaces, utilitzant Laravel Lumen o integrant-se amb altres serveis i APIs.
* Laravel facilita la creació d'APIs RESTful amb característiques com les API Resources i la integració amb Laravel Passport per l'autenticació OAuth.
* La comunitat de Laravel és una de les més actives i de suport en el món PHP, amb recursos com Laracasts, paquets de tercers, i fòrums extensos.



### Instal·lació de Laravel
 
#### Instal·lacio amb docker (laravel sail)

Si ja esteu desenvolupant Linux i Docker Compose està instal·lat, podeu utilitzar una senzilla ordre de terminal per a crear un nou projecte Laravel. Per exemple, per a crear una nova aplicació Laravel en un directori anomenat "exemple-app", podeu executar l'ordre següent al terminal:

curl -s https://laravel.build/example-app | bash

Per descomptat, podeu canviar "exemple-app" en aquest URL a qualsevol cosa que vulgueu - només assegureu-vos que el nom de l'aplicació només conté caràcters alfanumèrics, guions i guions baixos. El directori de l'aplicació Laravel es crearà dins del directori des del qual executeu l'ordre.

La instal·lació del **Sail** pot trigar diversos minuts mentre els contenidors de l'aplicació del **sail** es construeixen a la vostra màquina local.

Després de crear el projecte, 

Seria bó comprovar que el .env inclou la següent configuració:

```php
WWWUSER = 1000
WWWGROUP = 1000
```

Ara podeu navegar al directori de l'aplicació i iniciar Laravel Sail. Laravel Sail proporciona una interfície senzilla de línia d'ordres per a interactuar amb la configuració predeterminada de l'acoblador Laravel:
```php
cd exemple-app && ./vendor/bin/sail up &
```

Un cop iniciats els contenidors Docker de l'aplicació, podeu accedir a l'aplicació al vostre navegador web a: http://localhost.

Per a executar una terminal en el contenidor haurem d'executar:

```php
./vendor/bin/sail bash
```

I per a inicialitzar la base de dades des de dins del contenidor:

```php
php artisan migrate
```

##### phpmyadmin

Si volem que funcione el phpmyadmin haurien d'afegir un altre contenidor docker, o farem incluint el següent codi en el docker-compose.yml

```php
myadmin:
    image: 'phpmyadmin:latest'
    ports:
      - 8080:80
    environment:
      MYSQL_ROOT_PASSWORD: '${DB_PASSWORD}'
    links:
      - "mysql:db"
    depends_on:
      - mysql
    networks:
      - sail
```

#### Instal·lació des de repositori github

Seguiu aquests passos per a un repositori de Laravel amb Sail després de clonar des de Github. Aquest és un exemple

1. **Clona el repositori, exemple:**

    $ git clone https://github.com/example/laravel-backend-api.git

2. **Canvia el directori a l'aplicació/projecte de nova creació.**
   
    $ cd laravel-backend-api

3. **Copia el fitxer .env**
   
    $ cp .env.example .env

4. **Obre .env per a coincidir la configuració amb les línies següents:**

   ```php
   DB_CONNECTION=mysql
   DB_HOST=mysql
   DB_PORT=3306
   DB_DATABASE=batoiBook
   DB_USERNAME=root
   DB_PASSWORD=1234
   
5. ** Afegix el phpmyadmin a docker-compose.yml**
   
   ```php
   myadmin:
       image: 'phpmyadmin:latest'
       ports:
         - 8080:80
       environment:
         MYSQL_ROOT_PASSWORD: '${DB_PASSWORD}'
       links:
         - "mysql:db"
       depends_on:
         - mysql
       networks:
         - sail
    ```

5. **Instal·la totes les dependències requerides**
   
    $ docker run --rm -v $(pwd):/opt -w /opt laravelsail/php83-composer:latest composer install
   
    NOTA: Això pot trigar una estona si aquesta és la primera vegada que s'instal·la com a contenidor.

6. **Executa els servidors amb Sail**
   
    $ vendor/bin/sail up -d

7. **Entra en el phpmyadmin (localhost:8080) i crea la base de dades batoiBook.**

8. **Inicia el terminal del contenidor**
   
    $ vendor/bin/sail bash

9. **Genera la clau APP.KEY.**
   
    $ php artisan key:generate

10. **Construeix la llavor.**
    
    $ php artisan migrate:fresh --seed

11. **Genera els node_modules**
    
    $ npm install

    $ npm run build

Ara podeu obrir la vostra aplicació amb el vostre navegador: http://localhost

Ara que ja tenim tot el sistema preparat per a desenvolupar projectes Laravel, vegem els primers passos que hem de donar per a crear aquests projectes.

### Configuració de Laravel

La configuració en Laravel està centralitzada i organitzada en fitxers dins del directori **config/**. Aquests fitxers permeten ajustar el comportament de diferents aspectes de l'aplicació.

#### Fitxer .env

Laravel utilitza el fitxer `.env` per gestionar configuracions específiques de l'entorn. Aquest fitxer permet canviar paràmetres sense modificar el codi base.

##### Exemple de `.env`:
```env
APP_NAME="LaravelApp"
APP_ENV=local
APP_KEY=base64:...
APP_DEBUG=true
APP_URL=http://localhost

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=root
DB_PASSWORD=
```
### Configuració predeterminada

Els fitxers de configuració es troben al directori `config/`. A continuació es descriuen alguns dels més importants:

#### **1. config/app.php**
Conté configuracions globals de l'aplicació.

- **`name`**: Nom de l'aplicació.
- **`env`**: Entorn d'execució (`local`, `production`, `testing`).
- **`debug`**: Habilita o deshabilita el mode depuració (`true` o `false`).
- **`timezone`**: Zona horària de l'aplicació (per defecte `UTC`).
- **`locale`**: Idioma predeterminat.
- **`providers`**: Llista de proveïdors de serveis.
- **`aliases`**: Aliases per a facades.

#### **2. config/database.php**
Configura les bases de dades de l'aplicació.

- **`default`**: Connexió predeterminada (`mysql`, `sqlite`, `pgsql`, etc.).
- **Configuracions per a cada connexió**:
    - **`mysql`**: Exemple:
      ```php
      'mysql' => [
          'driver' => 'mysql',
          'host' => env('DB_HOST', '127.0.0.1'),
          'port' => env('DB_PORT', '3306'),
          'database' => env('DB_DATABASE', 'laravel'),
          'username' => env('DB_USERNAME', 'root'),
          'password' => env('DB_PASSWORD', ''),
      ],
      ```

#### **3. config/mail.php**
Configura el sistema d'enviament de correus electrònics.

- **`default`**: Transport predeterminat (`smtp`, `mailgun`, `sendmail`, etc.).
- **Configuracions SMTP**:
  ```php
  'mailers' => [
      'smtp' => [
          'transport' => 'smtp',
          'host' => env('MAIL_HOST', 'smtp.mailtrap.io'),
          'port' => env('MAIL_PORT', 2525),
          'username' => env('MAIL_USERNAME'),
          'password' => env('MAIL_PASSWORD'),
          'encryption' => env('MAIL_ENCRYPTION', 'tls'),
      ],
  ],
    ```
#### **4. config/filesystems.php**
Gestiona els sistemes d'arxius.

- **`default`**: Sistema predeterminat (local, s3, etc.).
- **Configuració de discos**:
```php
  'disks' => [
  'local' => [
  'driver' => 'local',
  'root' => storage_path('app'),
  ],
  's3' => [
  'driver' => 's3',
  'key' => env('AWS_ACCESS_KEY_ID'),
  'secret' => env('AWS_SECRET_ACCESS_KEY'),
  'region' => env('AWS_DEFAULT_REGION'),
  'bucket' => env('AWS_BUCKET'),
  ],
  ],
```

###  Funcions d'ajuda

Laravel proporciona **helpers** per treballar amb configuracions de manera senzilla i dinàmica.

#### **Accedir a configuracions**

Utilitza la funció `config()` per obtenir valors de configuració des de qualsevol lloc de l'aplicació:

```php
config('app.name'); // Retorna el nom de l'aplicació
```
#### Canviar configuracions en temps d'execució

Pots modificar configuracions de forma temporal durant l'execució de l'aplicació:

```php
config(['app.debug' => false]); // Desactiva el mode depuració
``` 

#### Establir valors predeterminats

Si el valor no existeix, pots establir un valor predeterminat:

```php
$value = config('app.missing_key', 'valor per defecte');
```
Aquestes funcions són útils per ajustar l'aplicació a les necessitats de l'entorn o per gestionar configuracions específiques durant l'execució.

### El comanament Artisan

Laravel inclou un interfície de línia de comandos (CLI, Command line interface) anomenat **Artisan**. Aquesta utilitat ens va a permetre realitzar múltiples tasques necessàries durant el procés de desenvolupament o desplegament a producció d'una aplicació, per la qual cosa ens facilitarà i accelerarà el treball.
Per a veure una llista de totes les opcions que inclou Artisan podem executar el següent comando en un consola o terminal del sistema en la carpeta arrel del nostre projecte:

    php artisan list

Si volem obtenir una ajuda més detallada sobre alguna de les opcions de Artisan simplement hem d'escriure la paraula **help** davant del comando en qüestió, per exemple:

    php artisan help migrate

A poc a poc anirem veient més opcions de Artisan, de moment anem a comentar solament dues opcions importants: el llistat de rutes i la generació de codi.

Per a veure un llistat amb totes les rutes que hem definit en el fitxer routes.php podem executar el comando:

    php artisan route:list

Açò ens mostrarà una taula amb el mètode, l'adreça, l'acció i els filtres definits per a totes les rutes. D'aquesta forma podem comprovar totes les rutes de la nostra aplicació i assegurar-nos que estiga tot correcte.


### Estructura d'un projecte Laravel

 
Laravel segueix una estructura modular basada en el patró **MVC (Model-Vista-Controlador)**. Aquesta organització facilita la separació de responsabilitats, manteniment i escalabilitat. A continuació, es descriuen les carpetes més importants.

#### Carpetes principals

##### **1. app/**
Conté la lògica principal de l'aplicació.
- **Models/**: Classes que representen les taules de la base de dades. Gestionen les relacions i la lògica de negoci.
- **Http/Controllers/**: Controladors que processen les peticions i retornen respostes.
- **Http/Middleware/**: Classes per filtrar i processar les peticions abans d'arribar als controladors.
- **Observers/**: Classes per observar i respondre a esdeveniments dels models.
- **Policies/**: Gestionen l'autenticació basada en permisos.

##### **2. bootstrap/**
Conté el fitxer `app.php`, que inicialitza el framework i carrega configuracions bàsiques. També inclou la **caché de rutes i serveis** per millorar el rendiment.

##### **3. config/**
Fitxers de configuració global de l'aplicació (base de dades, mail, cues, etc.). És recomanable revisar aquests fitxers per personalitzar-los segons les necessitats del projecte.

##### **4. database/**
Gestió de bases de dades.
- **Migrations/**: Fitxers per definir l'estructura de les taules de manera programàtica.
- **Factories/**: Generació de dades de prova per als models.
- **Seeders/**: Inserció de dades inicials per a la base de dades.

##### **5. public/**
Punt d'entrada de l'aplicació. Conté:
- Fitxer `index.php`, que gestiona totes les peticions.
- Recursos públics com **CSS, JavaScript, imatges**.

##### **6. resources/**
Carpeta de recursos per a la interfície d'usuari.
- **views/**: Conté les vistes Blade.
- **lang/**: Fitxers de traducció per a aplicacions multilingües.
- **css/** i **js/**: Recursos d'estil i funcionalitat del client.

##### **7. routes/**
Defineix totes les rutes de l'aplicació.
- **web.php**: Rutes per a l'aplicació web.
- **api.php**: Rutes per a APIs RESTful.
- **console.php**: Comandes Artisan personalitzades.
- **channels.php**: Rutes per a canals de difusió.

##### **8. storage/**
Emmagatzematge d'arxius generats per l'aplicació.
- **app/**: Conté arxius d'usuari o aplicació.
- **framework/**: Caché, sessions, i altres fitxers temporals.
- **logs/**: Registres d'errors i activitat.

##### **9. tests/**
Inclou proves automatitzades per garantir el bon funcionament de l'aplicació.
- **Feature/**: Proves completes que cobreixen múltiples components.
- **Unit/**: Proves individuals per a components o mètodes específics.

##### **10. vendor/**
Carpeta gestionada per Composer. Conté totes les dependències i paquets de tercers utilitzats pel projecte. **No s'ha de modificar manualment.**


### Desenvolupament del Frontend

Laravel ofereix diverses opcions per al desenvolupament del frontend, depenent de si prefereixes utilitzar PHP o frameworks JavaScript com Vue o React.

#### Utilitzant PHP

##### Blade
Blade és el motor de plantilles lleuger de Laravel que permet crear vistes amb una sintaxi senzilla per mostrar dades i iterar sobre elles.

##### Livewire
Livewire és un framework que facilita la construcció d'interfícies dinàmiques utilitzant PHP, sense necessitat de JavaScript addicional.

####  Utilitzant Vue o React

##### Inertia
Inertia actua com a pont entre Laravel i frameworks com Vue o React, permetent construir aplicacions modernes sense gestionar rutes o autenticació al costat del client.

#### Kits d'Inici
Laravel proporciona kits com Breeze i Jetstream que ofereixen scaffolding per a l'autenticació i altres funcionalitats, utilitzant Blade, Livewire, Vue o React.

#### Agrupació d'Actius
Laravel utilitza **Vite** per compilar i agrupar els actius del frontend, oferint temps de compilació ràpids i reemplaçament de mòduls en calent durant el desenvolupament.

 
### Laravel : Kits d'Inici

Laravel ofereix diversos kits d'inici per agilitzar el desenvolupament d'aplicacions, proporcionant scaffolding per a l'autenticació i altres funcionalitats essencials.

#### Laravel Breeze

Breeze és un kit d'inici minimalista que implementa les funcionalitats bàsiques d'autenticació, incloent:

- Inici de sessió
- Registre
- Restabliment de contrasenya
- Verificació de correu electrònic
- Confirmació de contrasenya

Per defecte, Breeze utilitza plantilles Blade estilitzades amb Tailwind CSS. També ofereix opcions de scaffolding basades en Livewire o Inertia, amb la possibilitat d'utilitzar Vue o React.

#### Laravel Jetstream

Jetstream és un kit d'inici més robust que amplia les funcionalitats de Breeze, afegint:

- Autenticació de dos factors
- Gestió de sessions
- Suport per a API mitjançant Laravel Sanctum
- Opcionalment, gestió d'equips

Jetstream està dissenyat amb Tailwind CSS i ofereix la possibilitat d'utilitzar Livewire o Inertia per al frontend.

##### Instal·lació

Per instal·lar Laravel Breeze en una aplicació Laravel existent:

```bash
composer require laravel/breeze --dev
php artisan breeze:install
php artisan migrate
npm install
npm run dev
``` 
Per instal·lar Laravel Jetstream:

```bash 
composer require laravel/jetstream
php artisan jetstream:install livewire
php artisan migrate
npm install
npm run dev
```
Nota: Substitueix livewire per inertia si prefereixes utilitzar Inertia.


### Arquitectura d'un projecte Laravel


#### Cicle de Vida d'una Sol·licitud en Laravel

Quan una sol·licitud HTTP arriba a una aplicació Laravel, aquesta segueix una sèrie de passos abans de retornar una resposta al client. A continuació, es detallen les etapes principals d'aquest procés:

##### 1. Creació de la Instància de l'Aplicació

Laravel inicia creant una instància de l'aplicació, que serveix com a contenidor de serveis per a la gestió de dependències.

##### 2. Selecció del Nucli (Kernel)

Segons el tipus de sol·licitud (HTTP o consola), Laravel dirigeix la sol·licitud al nucli corresponent:

- **HTTP Kernel**: Gestiona sol·licituds web.
- **Console Kernel**: Gestiona comandes de consola.

##### 3. Carregant els Bootstrapers

Abans de processar la sol·licitud, Laravel executa una sèrie de bootstrapers que configuren aspectes com la gestió d'errors, el registre de logs i la detecció de l'entorn de l'aplicació.

##### 4. Registre dels Proveïdors de Serveis

Els proveïdors de serveis són responsables de carregar i configurar els diversos components de Laravel, com la base de dades, la cua de treballs, la validació i el sistema de rutes.

##### 5. Execució del Middleware

Laravel passa la sol·licitud a través d'una cadena de middleware, que poden realitzar tasques com la verificació d'autenticació, la protecció CSRF i la gestió de sessions.

##### 6. Despatx de la Sol·licitud

Després de passar pel middleware, la sol·licitud és dirigida al controlador o ruta corresponent, on es processa la lògica de l'aplicació.

##### 7. Retorn de la Resposta

Un cop processada la sol·licitud, es genera una resposta que és retornada al client.


### Els Proveïdors de Serveis (Service Providers)

Els **proveïdors de serveis** són responsables de l'arrencada o "bootstrapping" de qualsevol projecte Laravel. La seva funció principal és registrar els components, dependències externes, classes i mètodes que hem definit, fent-los accessibles a tota l'aplicació.

Al fitxer **config/app.php** del projecte, trobaràs una secció anomenada **providers**. Aquest array conté tots els proveïdors de serveis que Laravel carrega quan l'aplicació s'inicia. Alguns exemples són:

- **DatabaseServiceProvider**: Gestiona l'accés a bases de dades.
- **AuthServiceProvider**: Configura el sistema d'autenticació d'usuaris.

Un proveïdor de serveis pot contenir dos mètodes principals:
- **register**: Defineix els serveis i els vincula al contenidor de Laravel.
- **boot**: S'executa després de carregar tots els serveis, ideal per inicialitzar funcionalitats.

---

### Les Classes del Nucli de Laravel

Laravel proporciona una infraestructura robusta de classes que faciliten el desenvolupament. Algunes d'aquestes classes són:

- **Route**: Permet definir i gestionar rutes.
- **Model**: Proporciona funcionalitats per a treballar amb la base de dades mitjançant Eloquent ORM.

Aquestes classes estan organitzades dins de l'espai de noms **Illuminate**, per la qual cosa sovint veurem imports com:

```php
use Illuminate\Database\Eloquent\Model;
```
 
###  Altres elements

A més dels dos pilars anteriors sobre els quals se sustenta fonamentalment el desenvolupament de projectes en Laravel, podem parlar d'altres elements que ens poden resultar d'utilitat en el desenvolupament, com són els facades i els contracts.

Les facades proporcionen una interfície estàtica als elements de l'aplicació, de manera que faciliten l'accésa uns certs mètodes o utilitats. Per exemple, la facade	**cache** permet accedir de manera senzilla amb el seu mètode **get**a unes certes propietats cachejades prèviament.

```php
return Cache::get('key');
```

Els **contracts** són un conjunt d'interfícies que proporcionen el nucli de serveis oferits per Laravel. Per exemple, mètodes per a enviar e-mails, o encolar tasques en una cola de prioritat, etc.


### MVC: Model - Vista - Controlador

El model–vista–controlador (MVC) és un patró d'arquitectura de programari que separa les dades i la lògica de negoci d'una aplicació de la interfície d'usuari i el mòdul encarregat de gestionar els esdeveniments i les comunicacions. Per a açò MVC proposa la construcció de tres components diferents que són el model, la vista i el controlador, és a dir, d'una banda defineix components per a la representació de la informació, i d'altra banda per a la interacció de l'usuari. Aquest patró d'arquitectura de programari es basa en les idees de **reutilització de codi** i la **separació de conceptes**, característiques que cerquen facilitar la tasca de desenvolupament d'aplicacions i el seu posterior manteniment.
De manera genèrica, els components de MVC es podrien definir com segueix:

* El **Model**: És la **representació de la informació** amb la qual el sistema opera, per tant gestiona tots els accessos a aquesta informació, tant consultes com a actualitzacions. Les peticions d'accés o manipulació d'informació arriben al 'model' a través del 'controlador'.
* El **Controlador**: **Respon a esdeveniments** (usualment accions de l'usuari) i **invoca peticions al 'model'** quan es fa alguna sol·licitud d'informació (per exemple, editar un document o un registre en una base de dades). Per tant es podria dir que el 'controlador' fa d'intermediari entre la 'vista' i el 'model'.
* La **Vista**: **Presenta el 'model'** i les dades preparades pel controlador a l'usuari de **forma visual**. L'usuari podrà interactuar amb la vista i realitzar altres peticions que s'enviaran al controlador.

![Modelo Vista Controlador](imagenes/07/mvc.png)

#### Funcionament bàsic

El funcionament bàsic que segueix Laravel després d'una petició web a una URL del nostre lloc és el següent:

* Totes les peticions entren a través del fitxer **public/index.php**, el qual en primer lloc comprovarà en el fitxer de rutes (**routes/web.php**) si la URL és vàlida i en cas de ser-ho al fet que controlador ha de fer la petició.

* A continuació cridarà al mètode del controlador assignat per a aquesta ruta. Com hem vist, el controlador és el punt d'entrada de les peticions de l'usuari, el qual, depenent de la petició:
    * Accedirà a la base de dades (si fóra necessari) a través dels "models" per a obtenir dades (o per a afegir, modificar o eliminar).
    * Després d'obtenir les dades necessàries els prepararà per a passar-li'ls a la vista.

* En el tercer pas el controlador cridarà a una vista amb una sèrie de dades associades, la qual es prepararà per a
  mostrar-se correctament a partir de les dades d'entrada i finalment es mostrarà a l'usuari.
  A continuació s'inclou un xicotet esquema d'aquest funcionament:

<figure>
  <img src="imagenes/07/l101.png" />
  <figcaption>Funcionament Bàsic Laravel</figcaption>
</figure>

## Rutes
[![](../img/ull.png)Video](https://youtu.be/oHJokaq0yeY)

Podríem dir que existeixen dos tipus principals de rutes:

* Les rutes **web** (emmagatzemades a l'arxiu **web.php** de l'aplicació), que ens permetran carregar diferents vistes en funció de la URL que indique el client.

* Les rutes **API** (emmagatzemades en l'arxiu **api.php**), a través de les quals deﬁnirem
  diferents serveis **REST**, com veurem també més endavant.

Ens centrarem durant aquesta tema en el primer grup, per la qual cosa editarem el contingut de l'arxiu **routes/web.php**. Vegem quins tipus de rutes podem *deﬁnir, i quines característiques tenen.

Este és el punt centralitzat per a la definició de rutes i qualsevol ruta no definida en aquest fitxer no serà vàlida, generat una excepció (el que retornarà un error 404).
Les rutes, en la seua forma més senzilla, poden retornar directament un valor des del propi fitxer de rutes, però també podran generar la trucada a una vista o a un controlador.

#### Rutes simples

Les rutes simples tenen un nom de ruta fix, i una funció que respon a aquest nom emetent una resposta.
Les rutes, a més de definir la URL de la petició, també indiquen el mètode amb el qual s'ha de fer aquesta petició. Els dos mètodes més utilitzats i que començarem veient són les peticions tipus GET i tipus POST. Per exemple, per a definir una petició tipus GET hauríem d'afegir el següent codi al nostre fitxer routes.php:

```php  
	Route::get('salut', function()
	{ 
		return 'Hola món!'; 
	});
```

Aquest codi es llançaria quan es realitze una petició tipus GET a la ruta arrel de la nostra aplicació. Si estem treballant en local aquesta ruta seria http://localhost (en el notre cas **intranet.my**) però quan la web estiga en producció es referiria al domini principal, per exemple: http://www.dirección-de-tu-web.com.


#### Afegir paràmetres a les rutes

Si volem afegir paràmetres a una ruta simplement els hem d'indicar entre claus {} a continuació de la ruta, de la forma:

```php    
    Route::get('salut/{nom}', function($nom)
    {
	return 'Bon dia, '.$nom; });
```    

En aquest cas estem definint la ruta /salut/{nom}, on **nom** és requerit i pot ser qualsevol valor. En cas de no especificar cap **nom** ens redigirirà a una pàgina d'error 404. El paràmetre se li passarà a la funció, el qual es podrà utilitzar (com veurem més endavant) para per exemple obtenir dades de la base de dades, emmagatzemar valors, etc.

També podem indicar que un paràmetre és opcional simplement afegint el símbol ? al final (i en aquest cas no donaria error si no es realitza la petició amb aquest paràmetre):

```php     
    Route::get('salut/{nom?}', function($nom = 'convidat')
    {
    	return 'Bon dia, '.$nom; 
	});
```   
#### Validació de paràmetres

Alguns paràmetres caldrà que seguisquen un determinat patró. Per exemple, un identificador numèric
només contindrà dígits. Per a assegurar-nos d'això, podem emprar el mètode *where en definir la ruta. A aquest mètode li passem dos paràmetres: el nom del paràmetre a validar, i l'expressió regular que
ha de complir. En el cas del nom anterior, si volem que només continga lletres (majúscules o minúscules), podem fer una cosa així:

```php 
Route::get('salut/{nom?}', function($nom = "Convidat") {
return "Hola, " . $nom;
})->where('nom', "[A-Za-z]+");
```
En cas que la ruta no complisca el patró, s'obtindrà una pàgina d'error. Més endavant s'explicarà
com podem personalitzar aquestes pàgines d'error.

#### Named routes

A vegades pot ser convenient associar un nom a una ruta. Especialment, quan aqueixa ruta formarà part d'un enllaç en alguna pàgina del nostre lloc, ja que en un futur la ruta podria canviar, i d'aquesta manera evitem haver d'actualitzar els enllaços al nou nom.
Per a això, en definir la ruta, li associem amb la funció **name** el nom que vulguem. Per exemple:

```php 
Route::get('contacte', function() {
return "Pàgina de contacte";
})->name('ruta_contacte');
```
Ara, si volem definir un enllaç a aquesta ruta en qualsevol part, n'hi ha prou amb emprar la funció **route** de Laravel, indicant el nom que li hem assignat a aquesta ruta. Per tant, en lloc de posar això:

```php 
echo '<a href="/contacte">Contacte</a>';
```
Podem fer alguna cosa com això un altre, tal com veurem a continuació quan usem el motor de plantilles **Blade**:

```php 
<a href="{{ "{{ route('ruta_contacte') " }}}}">Contacte</a>
```
D'aquesta manera, davant futurs canvis en les rutes, només haurem de canviar la URL en **Route::get**

#### Combinació d'elements en rutes

Podem combinar diverses clàusules **where** en una ruta per a validar diferents paràmetres que puga
tindre, i també enllaçar aquestes crides amb una a la funció **name** per a nomenar la ruta. Per exemple, la
següent ruta espera rebre un nom amb caràcters, i un id numèric, tots dos amb valors per defecte:

```php
Route::get('salut/{nom?}/{id?}',
function($nom="Convidat", $id=0)
{
return "Hola $nom, el teu codi és el $id";
})->where('nom', "[A-Za-z]+")
->where('id', "[0-9]+")
->name('salut');
```

Si accedim a cadascuna de les següents URLs, obtindrem cadascuna de les respostes indicades:

|URL|Respuesta|
|--|--|
|/salut| Hola Convidat, el teu codi és el 0|
|/salut/Ignasi| Hola Ignasi, el teu codi és el 0|
|/salut/Ignasi/3| Hola Ignasi, el teu codi és el 3|
|/salut/3| Error 404 (URL incorrecta)|

Notar que l'últim cas és incorrecte. No podem especificar un id sense haver especificat un nom
davant, perquè incompleix el patró de la URL. Es pot deixar un paràmetre omés, sempre que els
posteriors també ho estiguen.


## Vistes

[![](../img/ull.png)Video](https://youtu.be/D3uLYwkQ3C0)

Les vistes són la forma de presentar el resultat (una pantalla del nostre lloc web) de forma visual a l'usuari, el qual podrà interactuar amb ell i tornar a realitzar una petició. Les vistes a més ens permeten separar tota la part de presentació de resultats de la lògica (controladors) i de la base de dades (models).

Per tant no hauran de realitzar cap tipus de consulta ni processament de dades, simplement rebran dades i els prepararan per a mostrar-los com HTML.

Fins ara les rutes que hem definit retornen un text simple, excepte la qual ja estava creada per defecte
en el projecte, que apuntava a la pàgina d'inici. Si volguérem retornar contingut HTML, una
opció (costosa) seria retornar aquest contingut generat des del propi mètode de la ruta, a través de la
instrucció **return** , però en lloc de fer això des de dins de la pròpia funció de resposta, el més
habitual (i recomanable) és generar una vista amb el contingut HTML que es vol enviar al client.

La forma general de mostrar vistes en **Laravel** és fer que les rutes retornen (return) una determinada vista. Per a això, es pot emprar la funció **view** de Laravel, indicant el nom de la vista a generar o mostrar.
Per defecte, en la carpeta **resources/views** tenim disponible una vista d'exemple anomenada **welcome.blade.php** . És la que s'utilitza com a pàgina d'inici en la ruta arrel en **routes/web.php** :

```php
Route::get('/', function() {
return view('welcome');
});
```
Notar que no és necessari indicar el path o ruta cap a l'arxiu de la vista, ni tampoc l'extensió, ja que
Laravel assumeix que per defecte les vistes es troben en la carpeta **resources/views** , amb l'extensió
**.blade.php** (que fa referència al motor de plantilles **Blade** que veurem a continuació), o
simplement amb extensió **.php** (en el cas de vistes simples que no utilitzen Blade).
Podem, per exemple, crear una vista senzilla dins d'aquesta carpeta de vistes (anomenem-la
**inici.blade.php** ), amb un contingut HTML bàsic:

```html
<html>
	<head>
		<title>Inici</title>
	</head>
	<body>
		<h1>Pàgina d'inici</h1>
	</body>
</html>
```
I podem utilitzar esta vista com a pàgina d'inici:

```php
Route::get('/', function() {
return view('inicio');
});
```

Les vistes contenen el codi HTML del nostre lloc web, barrejat amb els **assets** (CSS, imatges, Javascripts, etc. que estaran emmagatzemats en la carpeta public) i una **mica de codi PHP (o codi Blade de plantilles, com veurem més endavant)** per a presentar les dades d'entrada com un resultat HTML.

##### Pasar valor a les vistes

És molt habitual passar una certa informació a unes certes vistes, com per exemple, llistats de dades a mostrar, o dades d'un element en concret. Per exemple, si volem donar un missatge de benvinguda a un nom
(suposadament variable), hem d'emmagatzemar el nom en una variable en la ruta, i passar-s'ho a la vista en carregar-la. Això pot fer-se, per exemple, amb el mètode **with** després de generar la vista, indicant el nomamb què l'associarem a la vista, i el valor (variable) associat a aquest nom. En el nostre cas quedaria així:

```php
Route::get('/', function() {
$nombre = "Nacho";
return view('inicio')->with('nombre', $nombre);
});
```

Posteriorment, en la vista, haurem de mostrar el valor d'aquesta variable en algun lloc del codi HTML.
Podem emprar PHP tradicional per a recollir aquesta variable:

```html
<html>
	<head>
		<title>Inicio</title>
	</head>
	<body>
		<h1>Página de inicio</h1>
		<p>Bienvenido/a <?php echo $nombre; ?></p>
	</body>
</html>
```

Però és més habitual i net emprar una sintaxi específica de Blade, com veurem a continuació.
Com a alternatives a l'ús de with comentat abans, també podem utilitzar un array associatiu (assignant així diversos noms a diversos valors):

```php
return view('inicio')->with(['nombre' => $nombre, ...]);
```

Així mateix, podem utilitzar aquest mateix array com segon paràmetre de la funció view , i prescindir
així de with :

```php
return view('inicio', ['nombre' => $nombre, ...]);
```

I també podem utilitzar una funció anomenada compact com segon paràmetre de view . A aquesta funció li passem únicament el nom de la variable i, sempre que la variable associada es cride igual, estableix l'associació per nosaltres:

```php
return view('inicio', compact('nombre'));
```

La funció **compact** admet tants paràmetres com dades vulguem enviar a la vista per separat, cadascun amb el seu nom associat. Si simplement retornarem una vista amb poca informació associada, o poca lògica interna, també podem abreujar el codi anterior cridant directament a view , en lloc de route primer, en
l'arxiu **routes/web.php** , i li passem així la informació associada a la vista:

```php
Route::view('/', 'inicio', ['nombre' => 'Nacho']);
```

## [Plantilles mitjançant Blade](https://laravel.com/docs/8.x/blade)

Laravel utilitza Blade per a la definició de plantilles en les vistes. Aquesta llibreria permet realitzar tot tipus d'operacions amb les dades, a més de la substitució de seccions de les plantilles per un altre contingut, herència entre plantilles, definició de layouts o plantilles base, etc.

Els fitxers de vistes que utilitzen el sistema de plantilles Blade han de tenir l'extensió **.blade.php**. Aquesta extensió tampoc s'haurà d'incloure a l'hora de referenciar una vista des del fitxer de rutes o des d'un controlador. És a dir, utilitzarem view('home') tant si el fitxer es diu home.php com home.blade.php.

En general el codi que inclou Blade en una vista començarà pels símbols **@** o **{{ "{{**, el qual posteriorment serà processat i preparat per a mostrar-se per pantalla. Blade no afig sobrecàrrega de processament, ja que totes les vistes són preprocesadas i cachejades, per contra ens brinda utilitats que ens ajudaran en el disseny i modularització de les vistes.

#### Mostrar dades
El mètode més bàsic que tenim en Blade és el de mostrar dades, per a açò utilitzarem les claus dobles (**{{ "{{ " }}}}**) i dins d'elles escriurem la variable o funció amb el contingut a mostrar:

```   
    Hola {{  $name }}.
```

Cada vegada que es renderitza una vista en Laravel, s'emmagatzema el contingut PHP generat en
**storage/framework/views** , i només es torna a re-generar davant un canvi en la vista, amb el que
tornar a cridar a una vista ja renderitzada no afecta al rendiment de l'aplicació. Si donem una ullada
a la vista generada amb PHP pla i amb Blade, veurem que hi ha una subtil diferència entre
ambdues, i és que amb Blade, en lloc de fer un simple echo per a mostrar el valor de la variable, s'utilitza
una funció intermèdia anomenada e , que evita atacs **XSS (Cross Site Scripting)**, és a dir, que
s'injecten scripts de Javascript amb la variable a mostrar. En altres paraules, el codi no s'interpreta,
i es mostra tal qual. En alguns casos (especialment quan generem contingut HTML des de dins de l'expressió Blade) ens pot interessar que no protegisca contra aquestes injeccions de codi.
En aqueix cas, se substitueix la segona clau per una doble exclamació:

```   
    Hola {!! $name !!}.
```

En general sempre haurem d'usar les claus dobles, especialment si anem a mostrar dades que són proporcionats pels usuaris de l'aplicació. Per tant, aquest últim mètode solament hem d'utilitzar-ho si estem segurs que no volem que s'escape el contingut.

##### Mostrar una dada sola si existeix
Per a comprovar que una variable existeix o té un determinat valor podem utilitzar l'operador ternari de la forma:

```php    
    {{  isset($name) ? $name : 'Valor per defecte' }}
```

O simplement usar la notació que inclou Blade per a aquesta fi:

```  
    {{  $name or 'Valor per defecte' }}
```

#### Comentaris
Per a escriure comentaris en Blade s'utilitzen els símbols **{{ "{{-- i --" }}}}**

#### Estructures de control

Per a iterar sobre un conjunt de dades (array), podem emprar la directiva @foreach , amb una sintaxi similar al foreach de PHP, però sense necessitat de claus. N'hi ha prou amb finalitzar el bucle amb la directiva
@endforeach , d'aquesta manera:

```html
<ul>
	@foreach($elementos as $elemento)
		<li>{{  $elemento}}</li>
	@endforeach
</ul>
```

En el cas de voler realitzar alguna comprovació (per exemple, si el array anterior està buit, per a mostrar
un missatge pertinent), usem la directiva @if , tancada pel seu corresponent parella @endif .
Opcionalment, es pot intercalar una directiva @else per al camí alternatiu, o també @elseif per a indicar una altra condició. L'exemple anterior podria quedar així:

```
<ul>
	@if($elementos)
		@foreach($elementos as $elemento)
			<li>{{  $elemento }}</li>
		@endforeach
	@else
			<li>No hay elementos que mostrar</li>
	@endif
</ul>
```

També podem comprovar si una variable està definida. En aquest cas, reemplacem la directiva @if per @isset, amb el seu corresponent tancament @endisset.

```html
<ul>
	@isset($elementos)
		@foreach($elementos as $elemento)
			<li>{{ $elemento }}</li>
		@endforeach
	@else
		<li>No hay elementos que mostrar</li>
	@endisset
</ul>
```

No obstant això, amb qualsevol d'aquestes opcions tenim un problema: en el primer cas, si la variable **\$elements** no està definida, mostrarà un error de PHP. En el segon cas, si la variable sí que està definida però no conté elements, no es mostrarà res per pantalla. Una tercera estructura alternativa que agrupa aquests dos casos (controlar alhora que la variable estiga definida i tinga elements) és emprar la directiva @forelse en lloc de @foreach . Aquesta directiva permet una clàusula addicional @empty per a indicar què fer si la col·lecció no té elements o està sense definir. L'exemple anterior quedaria ara així d'abreujat:

```
<ul>
	@forelse($elementos as $elemento)
		<li>{{  $elemento }}</li>
	@empty
		<li>No hay elementos que mostrar</li>
	@endforelse
</ul>
```


En aquesta mena de iteradors ( @foreach o @forelse ), tenim disponible un objecte anomenat \$loop ,
amb una sèrie de propietats sobre el bucle que estem iterant, com per exemple index (posició
dins del array per la qual anem), o count (total d'elements), o first i last (booleans que
determinen si és el primer o últim element, respectivament), entre altres. Podem veure totes les
propietats disponibles en aquest objecte cridant a var_dump :

```html
<ul>
	@forelse($elementos as $elemento)
		<li>{{  $elemento }} {{  var_dump($loop) }} </li>
	@empty
		<li>No hay elementos que mostrar</li>
	@endforelse
</ul>
```

Si, per exemple, volem determinar si és l'últim element de la llista, i mostrar un missatge o estil especial, podem fer alguna cosa com això:

```html
<ul>
	@forelse($elementos as $elemento)
		<li>{{  $elemento }}
			{{  $loop->last ? "Ultimo elemento" : "" }}
		</li>
	@empty
		<li>No hay elementos que mostrar</li>
	@endforelse
</ul> 
```   

Aquesta són les estructures de control més utilitzades. Ademas d'aquestes Blade defineix algunes més que podem veure directament en la seua [documentació](https://laravel.com/docs/8.x/blade#control-structures)


##### Sobre els enllaços a altres rutes

Hem comentat breument en punts anteriors que, gràcies a Blade i als noms en les rutes,podem enllaçar una vista amb una altra de dues formes: de manera tradicional...

```php
echo '<a href="/contacto">Contacte</a>';
```
... o bé emprant la funció route seguida del nom que li hem donat a la ruta:

```php
<a href="{{  route('ruta_contacto') }}">Contacte</a>
```

A més, mitjançant Blade existeix una tercera manera d'enllaçar, emprant la funció url , que genera una
URL completa fins a la ruta que indiquem:

```php
<a href="{{  url('/contacto') " }}">Contacte</a>
```

### Definir Plantilles comunes

A l'hora de donar homogeneïtat a una web, és habitual que la capçalera, el menú de navegació o el peu de pàgina formen part d'una plantilla que es repeteix en totes les pàgines del lloc, de manera que evitem
haver d'actualitzar totes les pàgines davant qualsevol possible canvi en aquests elements.
Per a crear una plantilla en Blade, creem un arxiu normal i corrent (per exemple,
**plantilla.blade.php** ), en la carpeta de vistes, amb el contingut general de la plantilla. En aquelles zones del document on permetrem contingut variable depenent de la vista en si, afegim
una secció anomenada **@yield** , amb un nom associat. La nostra plantilla podria ser aquesta (notar que es permeten varies **@yield** amb diferents noms):

```html
<html>
	<head>
		<title>
			@yield('titulo')
		</title>
	</head>
	<body>
		<nav>
			<!-- ... Menú de navegación -->
		</nav>
		@yield('contenido')
	</body>
</html>
```
Després, en cada vista en què vulguem utilitzar aquesta plantilla, afegim la directiva @*extends de Blade,
indicant el nom de plantilla que utilitzarem. Amb la directiva @section , seguida del nom de la
secció, definim el contingut per a cadascun dels @yield que s'hagen indicat en la plantilla.
Finalitzarem cada secció amb la directiva @endsection . Així, per a la nostra pàgina inicial
( inici.blade.php ), el contingut pot ser ara aquest:

```html
@extends('plantilla')
@section('titulo', 'Inicio')
@section('contenido')
	<h1>Página de inicio</h1>
	Bienvenido/a {{ $nombre }}
@endsection
```
Notar, a més, que a la directiva @section se li pot passar un segon paràmetre amb el contingut
d'aqueixa secció, i en aquest cas no és necessari tancar-la amb @endsection . Aquesta opció és útil per a continguts on no interessen caràcters en blanc o salts de línia innecessaris al principi o al final,
com ocorre en l'exemple anterior amb el títol (title) de la pàgina.
De la mateixa manera, la nostra vista per al llistat de llibres quedaria d'aquesta manera:

```html
@extends('plantilla')
@section('titulo', 'Listado de libros')
@section('contenido')
	<h1>Listado de libros</h1>
		<ul>
		@forelse ($libros as $libro)
			<li>{{  $libro["titulo"] }}({{  $libro["autor"] }})</li>
		@empty
			<li>No se encontraron libros</li>
		@endforelse
		</ul>
@endsection
```
##### Incloure vistes dins daltres

També sol ser habitual definir continguts parcials (se solen definir en una subcarpeta **partials**
dins de resources/views ), i incloure'ls en les vistes. Per a això, utilitzarem la directiva **@include**
de Blade.
Per exemple, definirem un menú de navegació. Suposem que aquest menú està en l'arxiu
**resources/views/partials/nav.blade.php**.

```html
<nav>
	<a href="{{  route('inici') }}">Inici</a>
	<a href="{{  route('libres_llistat') }}">Llistat de llibres</a>
</nav>
```

Per a incloure el menú en la plantilla anterior, podem fer això (i eliminaríem el menú <nav> de la
plantilla):

```html
<html>
	<head>
		<title>
			@yield('titulo')
		</title>
	</head>
	<body>
		@include('partials.nav')
		@yield('contenido')
	</body>
</html>
```

##### Estructuras vistes en carpetes

Quan l'aplicació és una mica complexa, poden ser necessàries diverses vistes, i tindre-les totes en una mateixa carpeta pot ser una cosa difícil de gestionar. És habitual, com anirem veient en sessions posteriors,
estructurar les vistes de la carpeta **resources/views** en **subcarpetas**, de manera que, per exemple, cada carpeta es referisca a les vistes d'una entitat o model de l'aplicació, o a un controlador específic. Per renderitzar una vista que està dins d'una carpeta,  haurem d'indicar també el nom de la subcarpeta:

```php
Route::get('llistat', function() {
	...
	return view('llibres.llistat', compact('llibres'));
});
```

Ací tindrem una vista llistat dins d'una carpeta llibres.


##### Vistes per a pàgines d'error

Quan programem, algunes accions que fem provocaran pàgines d'error amb determinats
codis, com per exemple 404 per a pàgines no trobades. Si volem definir l'aspecte i estructura d'aquestes
pàgines, n'hi ha prou amb crear la vista corresponent en la carpeta **resources/views/errors** , per exemple
, **resources/views/errors/404.blade.php** per a l'error 404 (anteposem el codi d'error
al sufix de la vista).

```php
@extends('plantilla')
@section('titulo', 'Error 404')
@section('contenido')
	<h1>Error</h1>
	Documento no encontrado
@endsection
```

## Ús de Components Blade en Laravel

Els components Blade són una funció poderosa en Laravel que permet als desenvolupadors crear elements d'interfície d'usuari reutilitzables. Aquests components poden ser personalitzats i inclosos en diverses vistes, oferint una manera eficient de gestionar elements comuns com formularis, botons, o panells d'informació.

### Creació d'un Component Blade
Per crear un component Blade, podeu utilitzar el comandament Artisan:

```php
php artisan make:component NomDelComponent
```
Això crearà una nova classe de component en app/View/Components i una vista associada en resources/views/components.

### Definició del Component
Dins de la classe del component, podeu definir propietats i mètodes que el component utilitzarà. Per exemple:

```php
namespace App\View\Components;

use Illuminate\View\Component;

class Alert extends Component
{
    public $type;

    public function __construct($type)
    {
        $this->type = $type;
    }

    public function render()
    {
        return view('components.alert');
    }
}
```

### Utilització del Component en Vistes
Per utilitzar el component, simplement afegiu-lo a la vostra vista Blade com si fos una etiqueta HTML:

```php
<x-alert type="danger">
    Aquest és un missatge d'alerta!
</x-alert>
```

Aquest enfocament manté el codi organitzat i promou la reutilització del codi, facilitant el manteniment i la lectura dels teus projectes Laravel.

## Enllaçant amb CSS i Javascript en el client

Ara que ja tenim una visió bastant completa del que el motor de plantilles Blade pot oferir-nos, arriba el moment d'acabar de perfilar les nostres vistes. Fins ara no hem parlat res d'estils CSS, i això és una cosa que tota vista que es pree ha d'incloure. A més, també pot ser necessari en alguns casos incloure alguna llibreria Javascript en el costat del client per a uns certs processaments.
Veurem com gestiona Laravel aquests recursos.  Per a poder afegir estils CSS o arxius Javascript al nostre projecte Laravel, el framework proporciona
ja uns arxius on centralitzar aquestes opcions.

### Vite

Vite és una eina de construcció de frontend moderna que proporciona un entorn de desenvolupament extremadament ràpid i empaqueta el vostre codi per a la producció. En construir aplicacions amb Laravel, normalment utilitzareu Vite per empaquetar els fitxers CSS i JavaScript de la vostra aplicació en actius preparats per a la producció.
Laravel s'integra perfectament amb Vite proporcionant una directiva oficial de connectors i de Blade per carregar els vostres actius per al desenvolupament i la producció.

#### Instal·lació del connector Vite i Laravel

En una instal·lació nova del Laravel, trobareu un fitxer package.json a l'arrel de l'estructura de directoris de la vostra aplicació. El fitxer predeterminat package.json ja inclou tot el que necessiteu per començar utilitzant el connector Vite i Laravel. Podeu instal·lar les dependències del frontal de l'aplicació mitjançant NPM:

```
npm install
```

##### Configuració de Vite

Vite està configurat a través d'un fitxer vite.config.js a l'arrel del projecte. Podeu personalitzar aquest fitxer segons les vostres necessitats, i també podeu instal·lar altres connectors que requereixi la vostra aplicació, com ara .vitejs/plugin-vue o .vitejs/plugin-react.

El connector Laravel Vite requereix que especifiqueu els punts d'entrada per a la vostra aplicació. Aquests poden ser fitxers JavaScript o CSS, i inclouen llenguatges preprocessats com TypeScript, JSX, TSX, i Sass.

```
import { defineConfig } from 'vite';
import laravel from 'laravel-vite-plugin';

export default defineConfig({
   plugins: [
      laravel([
         'resources/css/app.css',
         'resources/js/app.js',
     ]),
   ],
});
```

##### Carregar els vostres scripts i estils
Amb els punts d'entrada de Vite configurats, només els necessiteu referències en una directiva .vite() Blade que afegiu a la <head> de la plantilla arrel de la vostra aplicació:.

```
<!doctype html>
<head>
    {{-- ... --}}
 
    @vite(['resources/css/app.css', 'resources/js/app.js'])
</head>
```

La directiva @vite detectarà automàticament el servidor de desenvolupament de Vite i injectarà el client de Vite per habilitar la substitució del mòdul Hot. En el mode de construcció, la directiva carregarà els vostres actius compilats i versionats, incloent-hi qualsevol CSS importat.

##### Executar Vite
Hi ha dues maneres d'executar Vite. Podeu executar el servidor de desenvolupament mitjançant l'ordre dev, la qual és útil mentre es desenvolupa localment. El servidor de desenvolupament detectarà automàticament els canvis als vostres fitxers i els reflectirà instantàniament en qualsevol finestra del navegador oberta.

O, executar l'ordre de construcció versionarà i empaquetarà els actius de la vostra aplicació i els prepararà per a desplegar-los en producció:

##### Run the Vite development server...
npm run dev

##### Build and version the assets for production...
npm run build

### Instal·lar tailwind CSS amb Laravel

Tailwind CSS és un framework CSS d'utilitat-primera per a la construcció ràpida d'interfícies d'usuari personalitzades. A diferència d'altres frameworks CSS com Bootstrap o Foundation, que ofereixen components pre-dissenyats, Tailwind proporciona classes d'utilitat a baix nivell que es poden compondre per crear dissenys únics i personalitzats.

Cada classe en Tailwind té un propòsit específic (com ara marge, relleno, tipus de lletra, alineació, etc.), permetent als desenvolupadors construir ràpidament dissenys complexes sense escriure CSS des de zero. A més, Tailwind facilita la personalització i l'adaptació als requeriments específics del disseny, fent-lo una eina molt flexible per als desenvolupadors front-end.

[Instal·lacio](https://tailwindcss.com/docs/guides/laravel)

## Proves amb laravel
En les primeres rutes de la nostra aplicació, utilitzem el navegador per a provar aquestes rutes i URLs. El problema d'aquestes proves en el navegador és que no perduren en el temps ni poden executar-se de forma ràpida / automàtica. Així que avui veurem com podem provar el codi que desenvolupem de forma més intel·ligent, utilitzant el component de proves automatitzades que ve inclòs amb Laravel.

##### Directori de proves
Laravel inclou en el directori principal del teu projecte un directori anomenat /tests. En aquest directori anem a escriure codi que es va a encarregar de provar el codi de la resta de l'aplicació. Aquest directori està separat en dos subdirectoris:

* El directori Feature on escrivim proves que emulen peticions HTTP al servidor.
* El directori Unit on escrivim proves que s'encarreguen de provar parts individuals de l'aplicació (com a classes i mètodes).

##### Escrivint una prova
El comanament per a generar noves proves és **php artisan make:test NombreDeLaPruebaTest**
En la prova simularem una petició HTTP GET a la URL del mòdul d'usuaris. Amb **assertStatus** comprovem que la URL carrega de forma correcta verificant que el status HTTP siga 200. Amb el mètode **assertSee**  comprovem que podem veure el text “Usuaris”:

```php    
    / @test /
    function it_loads_the_users_lists_page(){
    	$this->get(‘usuaris)->assertStatus(200)->assertSee(‘Usuaris’);
    	}
```    

Perquè PHPUnit execute el mètode com una prova, has de col·locar l'anotació / @test / abans de la declaració
del mètode o col·locar el prefix test_ en el nom del mètode com a tal:


```php   
	function test_it_loads_the_users_lists_page(
		{	
		$this->get(‘usuaris)->assertStatus(200)->assertSee(‘Usuaris’);
		}
```    

En cas contrari el mètode NO serà executat com una prova, la qual cosa és útil perquè ens permet agregar mètodes helpers dins de la nostra classe de proves.

##### Notes

* Pots executar les proves amb vendor/bin/phpunit o crear un àlies per a la consola (àlies t=vendor/bin/phpunit).
* Pots llegir sobre els mètodes d'assercions disponibles en la documentació de Laravel.


#### Exercicis

En el repositori nou anem a crear un Blog:

701. Edita el fitxer routes/web.php i afig una nova [ruta](#rutes-simples) a la URL posts. En accedir a aquesta ruta (http://localhost/posts), haurem de veure un missatge amb el text “Llistat de posts”.

702. Afig una nova [ruta parametritzada](#afegir-paràmetres-a-les-rutes) a **posts/{id}** , de manera que el paràmetre id siga numèric (és a dir, només continga dígits del 0 al 9) i obligatori. Fes que la ruta retorne el missatge "Fitxa del post XXXX", sent XXXX l'id que haja rebut com a paràmetre.

Posa un [nom](#named-routes) a les dos rutes que has definides fins ara:

* a la del llistat la direm "posts_llistat"
* a la de fitxa que acabes de crear, la direm "posts_fitxa".

A més, a la ruta que carrega el wellcome l'anomenarem "inici".

703. Definix una [plantilla](#definir-plantilles-comunes) anomenada plantilla.blade.php en la carpeta de vistes del projecte ( resources/views/layouts ). Defineix una capçalera amb una secció yield per al títol, i una altra per al contingut de la pàgina, com la de l'exemple que hem vist anteriorment.
     Defineix en un arxiu a part en la subcarpeta **partials** , anomenat **nav.blade.php** , una barra de navegació que ens permeta accedir a aquestes direccions de moment:

	* Pàgina d'inici
	* Llistat de posts

[Inclou la barra de navegació en la plantilla base](#incloure-vistes-dins-daltres) que has definit abans
A partir de la plantilla base, [defineix altres dues vistes](#definir-plantilles-comunes) en una subcarpeta posts , anomenades posts/llistat.blade.php i posts/fitxa.blade.php . Com a títol de cada pàgina posa un breu text del que són (per exemple, "Llistat posts" i "Fitxa post"), i com a contingut de moment deixa un encapçalat **h1** que indique la pàgina en la qual estem: "Llistat de posts" o "Fitxa del post XXXX", on XXXX serà [l'identificador del post](#pasar-valor-a-les-vistes) que haurem passat per la URL (i que deuràs passar a la vista).

Fes que les rutes corresponents de routes/web.php que ja has definit [renderitzen](#vistes) aquestes vistes en lloc de retornar text pla.

Edita l'arxiu **partials/nav.blade.php** per a modificar la barra de navegació i deixar-la amb un estil particular de tailwindcss. Pots consultar aquesta [pàgina](https://tailwindcss.com/docs/installation) per a prendre idees d'alguns dissenys que pots aplicar en la barra de navegació.
Modificat l'arxiu welcome.blade.php  i canvia-ho perquè també herete de la plantilla base. Afig algun text introductori com a contingut.

704. Instal·la el tailwind CSS.
704. Crea un components Alert per a vore les alertes de l'aplicació. Aquest component tindrà un atribut type que pot ser success, error o warning. El component mostrarà un missatge d'alerta amb el text que li passem com a contingut i el tipus d'alerta que li passem com a atribut. El component tindrà un estil diferent per a cada tipus d'alerta. Els estils els pots trobar en la documentació de tailwindcss.
705. Fes una pàgina d'error 404.blade i mostra un missatge mitjançant Alert. Aquesta pàgina s'ha de mostrar quan l'usuari accedix a una ruta que no existeix.

## Controladors

[Video](https://www.youtube.com/watch?v=VwNTfrN8XTU&t=629s)

Fins al moment hem vist solament com retornar una cadena per a una ruta i com associar una vista a una ruta directament en el fitxer de rutes. Però en general la forma recomanable de treballar serà associar aquestes rutes a un mètode d'un controlador. Els controladors permeten estructurar millor el codi de la nostra aplicació. La seua principal utilitat radica
a alliberar als arxius de rutes d'haver d'ocupar-se també de gestionar una certa lògica comuna de les
peticions, com l'accés a les dades, validació de formularis, etc.

Com ja vam veure en la secció d'introducció, els controladors són el punt d'entrada de les peticions dels usuaris i són els que han de contenir tota la lògica associada al processament d'una petició, encarregant-se de realitzar les consultes necessàries a la base de dades, de preparar les dades i de cridar a la vista corresponent amb aquestes dades.

### Definició de controladors


Per a definir un controlador en la nostra aplicació, hem de tirar mà de nou del comando **php artisan** vist prèviament. En concret, utilitzarem l'opció **make:controller** seguida del nom que li vulguem donar al controlador. Típicament, els noms de controladors acaben amb el sufix Controller, per la qual cosa podem crear un de prova així:

```php
php artisan make:controller PruebaController
```

Això generarà una classe buida amb el nom del controlador. Per defecte, els controladors es guarden en la subcarpeta **app/Http/Controllers** del nostre projecte Laravel.

#### Controladors de recursos

El comando anterior admet alguns paràmetres addicionals més. Si creem un controlador amb l'opció -r, crearà un controlador de recursos ( resources ), i predefinirà en ell una sèrie de mètodes d'utilitat per a les operacions principals que es poden realitzar sobre una entitat de la nostra aplicació:


```php
php artisan make:controller PruebaController -r
```


* index : mostra un llistat dels elements d'aqueixa entitat o recurs
* create : mostra el formulari per a donar d'alta nous elements
* store : emmagatzema en la base de dades el recurs creat amb el formulari anterior
* show : mostra les dades d'un recurs específic (a partir de la seua clau o id).
* edit : mostra el formulari per a editar un recurs existent
* update : actualitza en la base de dades el recurs editat amb el formulari anterior
* destroy : elimina un recurs pel seu identificador.

Òbviament, el codi de tots aquests mètodes apareixerà buit al principi, i els haurem d'emplenar amb les operacions corresponents més endavant.
Si volem utilitzar un controlador d'aquest tipus, i cridar a algun dels seus mètodes des d'alguna ruta, ja no n'hi ha prou amb posar el nom del controlador, com féiem abans amb els de tipus **invoke**, ja que ara hi ha més d'un mètode que triar. El que farem serà posar el nom del controlador, seguit d'una
arrova @ i el nom del mètode a invocar. Per exemple:

```php
Route::get('prueba', 'PruebaController@index')->name('listado_prueba');
```

!!! note Per a que esta definició de rutes funcione correctament hem d'afegir un linea al app/providers/RouteServiceProvider per afegir el espai de noms dels control·ladors:

```php
public function boot()
    {
        $this->configureRateLimiting();

        $this->routes(function () {
            Route::middleware('api')
                ->prefix('api')
                ->group(base_path('routes/api.php'));

            Route::middleware('web')
                ->namespace('App\Http\Controllers')
                ->group(base_path('routes/web.php'));
        });
    }
```

#### Unint totes les rutes d'un controlador

Al final de tot el procés d'implementació d'un controlador (de recursos o de API) tindrem en l'arxiude rutes una dedicada a cada mètode del controlador (una per a index , una altra per a show , etc.).
Aquestes rutes poden agrupar-se en una sola usant el mètode resource de la classe Route , en lloc de get, indicant-li com a paràmetres el nom base de la ruta, i el controlador que s'encarregarà d'ella:

```
Route::resource('catalog', CatalogController::class);
```

La ruta anterior definirà una ruta GET cap a /catalog , atesa pel mètode index del controlador,una altra ruta GET cap a /catalog/{id} atesa pel mètode show del controlador... etc.
També podem utilitzar el mètode only per a indicar per a quins mètodes volem rutes:

```
Route::resource('catalog', CatalogController::class)->only(['index', 'show']);
```

Des del costat oposat, tenim disponible el mètode **except** per a indicar que es generen totes les rutes excepte aquelles per als mètodes indicats:

```
Route::resource('catalog', CatalogController::class)->except(['update', 'edit']);
```



#### Reanomenant les vistes

A mesura que el projecte creix, generarem un bon nombre de vistes associades a controladors, i és necessari estructurar aquestes vistes d'una forma adequada per a poder-les identificar ràpidament. Una convenció que podem seguir és nomenar les vistes a partir del controlador o model al qual fan referència, i a l'operació que realitzen. Per exemple, si tenim un controlador anomenat
PruebaController , se suposa que actuarà sobre una taula anomenada prueba (ho veurem més endavant, en la sessió d'accés a dades). I, podem emmagatzemar les vistes en la subcarpeta **resources/views/pruebas** , i definir dins les vistes
associades a cada operació del controlador que tinguem definida. Per exemple:
index.blade.php
show.blade.php
...

##### Renderitzant les vistes
Paral·lelament, cada vegada que anem a carregar una vista des d'algun controlador o ruta, farem referència a aquest nom.

```
  public function index(){
    return view('catalog.index');
  }
```


#### Controladors i espais de noms

També podem crear sub-carpetes dins de la carpeta Controllers per a organitzar-nos millor. En aquest cas, l'estructura de carpetes que creem no tindrà res a veure amb la ruta associada a la petició i, de fet, a l'hora de fer referència al controlador únicament haurem de fer-ho a través del seu espai de noms.

Com hem vist en referenciar el controlador en el fitxer de rutes únicament hem d'indicar el seu nom i no tota la ruta ni l'espai de noms App\Http\Controllers. Açò és perquè el servei encarregat de carregar les rutes afig automàticament l'espai de noms arrel per als controladors.
Si fiquem tots els nostres controladors dins del mateix espai de noms no haurem d'afegir res més. Però si decidim crear sub-carpetes i organitzar els nostres controladors en sub-espais de noms, llavors sí que haurem d'afegir aqueixa part.

Per exemple, si vam crear un controlador en **App\Http\Controllers\Photos\AdminController**, llavors per a registrar una ruta fins a aquest controlador hauríem de fer:

```
	Route::get('foo', 'Photos\Admincontroller@method');
```

## Injecció de dependències

El concepte d'injecció de dependències és molt habitual en l'ús de frameworks. Consisteix en un mecanisme que facilita recursos als diferents components de l'aplicació, i és una cosa que ja hem utilitzat, sense saber-ho, en els mètodes que s'han generat per als controladors.
Per exemple, quan definim un mètode en un controlador que necessita processar una petició, se li passa
com a paràmetre un objecte de tipus **Request**. Automàticament, Laravel processa el tipus de dada i
obté l'objecte associat (en aquest cas, la petició del client).

```
class PruebaController extends Controller
{
	...
	public function store(Request $request)
	{
		...
	}
}
```

#### Controladors API

Com a alternativa als controladors de recursos vistos abans, podem crear els controladors amb l'opció --api. Crearà un controlador amb els mateixos mètodes que el de recursos, excepte els mètodes create i edit , encarregats de mostrar els formularis de creació i edició de recursos, ja que en les APIs aquests formularis no són necessaris, com veurem en sessions posteriors.

Amb els controladors de tipus API també podem generar automàticament totes les rutes per als seus mètodes, utilitzant el mètode apiResource de la classe Route , en lloc del mètode resource empleat abans:

```
Route::apiResource('prueba', 'PruebaController');
```


### Exemple: La resposta

Igual que tenim un objecte Request per a obtindre dades de la petició, també existeix un **Response** per a gestionar la resposta. Laravel proporciona un mètode **response** al qual li podem passar diversos paràmetres:

1. El contingut de la resposta
2. El codi d'estat HTTP de resposta (si no s'especifica, per defecte és 200)
3. Un array amb les capçaleres de resposta (per defecte està buit).

Així, si per exemple volem emetre una resposta determinada amb el seu codi d'estat des d'un
controlador, podem fer això (per exemple, per a un codi 201):

```
response("Mensaje de respuesta", 201);
```
Les capçaleres poden especificar-se com un array, o enllaçant anomenades al mètode **header** (una per a cada capçalera):

```
response("Mensaje de respuesta", 201)
->header('Cabecera1', 'Valor1')
->header('Cabecera2', 'Valor2');
```
En el cas de voler retornar un objecte com a resposta, podem emprar el mètode **json** de la resposta (més endavant veurem que tots els objectes emesos directament al client s'envien en
format **JSON**), i així podrem adjuntar un codi d'estat diferent de 200:

```
return response()->json(['datos' => datos], 201)
->header('Cabecera1', 'Valor1')
...;
```

### Utilitzar la resposta per fer redireccions


Existeix també un mètode redirect que podem emprar per a redirigir a una ruta des d'una altra,bé especificant la ruta com a paràmetre...
```
redirect('/');
```

... o bé indicant una ruta amb nom:

```
redirect()->route('inicio');
```

... O si volem tornar a la ruta anterior simplement podem usar el mètode back:

```	
	return back();
```


Podem passar valors a la següent redirecció, emmagatzemant-los en sessió amb el mètode **with** ,
encara que aquests valors es perdran en la següent petició (no es queden emmagatzemats en sessió):

```
redirect()->route('inicio')
->with('mensaje', 'Mensaje enviado correctamente');
```


Per a accedir a aquest missatge des de la vista afectada, hem d'utilitzar la funció session :

```
@if(session()->has('mensaje'))
	{{ session('mensaje') }}
@endif
```


Finalment, notar que si fem la redirecció des de dins d'un mètode d'un controlador (per exemple, per a redigir a una ruta des d'una altra), haurem de retornar ( return ) el resultat d'aqueixa
redirecció perquè faça efecte:

```
class LibroController extends Controller
{
	public function index()
	{
		...
	}
	public function store(...)
	{
		...
		return redirect()->route('libros.index');
	}
}
```


#### Redirecció amb els valors de la petició
Les redireccions se solen utilitzar després d'obtenir algun error en la validació d'un formulari o després de processar alguns paràmetres d'entrada. En aquest cas, perquè en mostrar el formulari amb els errors produïts puguem afegir les dades que havia escrit l'usuari haurem de tornar a enviar els valors enviats amb la petició usant el mètode withInput():

```
	return redirect('form')->withInput();
	// O per a reexpedir les dades d'entrada excepte alguns:
	return redirect('form')->withInput($request->except('password'));
```


### Exemple:Helpers

Per a acabar aquesta introducció al que suposa la injecció de dependències en frameworks de desenvolupament, farem ús d'una eina que ens pot ser útil en algunes situacions: els **helpers**.
Un helper és bàsicament una funció d'utilitat que podem voler utilitzar en diversos punts de la
nostra web, i que necessitem tindre localitzada i compartida. Per exemple, imaginem que volem
ressaltar en el nostre menú de navegació l'opció que tenim actualment visible.
Per a això, podem definir una classe **CSS** amb l'estil que vulguem per a ressaltar (això ho farem a part, en els arxius **CSS** del projecte), i després utilitzar aqueixa classe **CSS** en una condició per a cada menú de navegació.

Per exemple, suposem que la classe **CSS** per a identificar el menú actiu es diu actiu . En aquest cas,
per a un menú de diverses opcions com aquest, n'hi ha prou amb utilitzar el mètode **routeIs** de la petició
( **request** ) per a comprovar si la ruta coincideix amb cada menú, i mostrar-lo com a actiu o no, usant un
operador ternari de comparació:

```html
<nav>
	<ul>
		<li class="{{  request()->routeIs('inicio') ? 'activo' : '' " }}">
			<a href="/">Inicio</a>
		</li>
		<li class="{{   request()->routeIs('contacto') ? 'activo' : '' " }}">
			<a href="/contacto">Contacto</a>
		</li>
		...
	</ul>
</nav>
```
Aquesta característica també funciona si les rutes tenen paràmetres.
Podem, en canvi, traure fora de la vista la lògica d'establir un camp com a actiu o no. Per a això,
creem un arxiu d'utilitat o **helper**. Ho podem cridar **helpers.php** , i situar-ho en la mateixa
carpeta app, dins d'una carpeta **Helpers**. Dins, definim la funció que ens retornarà si una ruta està activa o no, a partir del seu nom:

```php
function setActivo($nombreRuta)
{
	return request()->routeIs($nombreRuta) ? 'activo' : '';
}
```

I d'aquesta manera, la nostra vista simplement es dedica a cridar a aquesta funció per a cada element del menú:

```html
<nav>
	<ul>
		<li class="{{  setActivo('inicio') }}">
			<a href="/">Inicio</a>
		</li>
		<li class="{{  setActivo('contacto')}}">
			<a href="/contacto">Contacto</a>
		</li>
		...
	</ul>
</nav>
```

En el cas de voler mantindre l'enllaç actiu per a qualsevol subruta a partir de l'original (per exemple,
quan estem veient la fitxa d'un registre a partir del llistat general, podem utilitzar el wildcard d'asterisc
* ):

```html
<li class="{{  setActivo('peliculas.*') }}">
	<a href="{{  route('peliculas')}}">Peliculas</a>
</li>
```

No obstant això, perquè Laravel carregue l'arxiu **helpers.php** que acabem de crear, com no és una classe, hem d'indicar-ho explícitament (Laravel càrrega automàticament totes les classes de la carpeta app , però no arxius solts que no siguen classes). Podem fer-ho amb l'autoloader del composer.json de l'arrel del nostre projecte. En la secció autoload cal afegir una secció **files** amb un **array** amb els
arxius que vulguem que es carreguen també:

```
	"autoload": {
	"classmap": [ ... ],
	"psr-4": { ... },
	"files": ["app/helpers.php"]
	},
```

Després d'efectuar el canvi, hem de dir-li a *composer que torne a compilar l'acte carregador. Des de la
carpeta del projecte, executem aquest comando:

```
composer dump-autoload
```

##### HelperServiceProvider

[Video](https://www.youtube.com/watch?v=sFvxC6zXFjM)

Però la millor forma de fer-ho per a que les funcions d'aquest fitxer siguen visibles en l'aplicació és a crear un ServiceProvider i a registrar-lo:

	php artisan make:provider HelperServiceProvider

Crearà un fitxer en la carpeta Providers.
L'editem per afegir el nostre Helper.

```php

	/**
	     * Register services.
	     *
	     * @return void
	     */
	    public function register()
	    {
	        require_once base_path() . '/app/Helpers/myHelpers.php';
	    }
```


I ara registrem el ServiceProvider en el fitxer **config/app.php**

```php

'providers' => [

        /*
         * Laravel Framework Service Providers...
         */
        Illuminate\Auth\AuthServiceProvider::class,
        
        .....

        /*
         * Package Service Providers...
         */

        /*
         * Application Service Providers...
         */
        App\Providers\AppServiceProvider::class,
        App\Providers\AuthServiceProvider::class,
        // App\Providers\BroadcastServiceProvider::class,
        App\Providers\EventServiceProvider::class,
        App\Providers\RouteServiceProvider::class,
        App\Providers\HelperServiceProvider::class,

    ],
```

I com cada volta que toquen un fitxer de configuració executem

	php artisan config:cache

#### Exercicis

#### Exercisi 711.

Sobre el projecte blog de la sessió anterior, afegirem aquests canvis:

* Crea un [controlador](#controladors-de-recursos) de recursos (opció -r ) anomenat **PostController** , que ens servirà per a gestionar tota la lògica dels posts del blog.
* [Assigna automàticament](#unint-totes-les-rutes-dun-controlador) amb el mètode **resource** cada ruta a la seua funció corresponent del controlador, en l'arxiu **routes/web.php** . Limita amb **only** les accions només a les funcions de llistat (index), fitxa (show), creació (create) i edició (edit).
* Canvia de nom les [vistes](#reanomenant-les-vistes) de **llistat** i **fitxa** d'un post a **index.blade.php** i show.blade.php, dins de la seua carpeta posts, i fes que els mètodes corresponents del controlador de posts [renderitzen](#renderitzant-les-vistes) aquestes vistes.
* Per als mètodes create i, simplement retorna un text pla en una vista indicant "Nou post" , per exemple.
* Fes els canvis addicionals que siguen convenients (per exemple, en el menú de navegació) perquè els enllaços continuen funcionant, i prova que les quatre rutes (llistat, fitxa, creació i edició) funcionen adequadament.
* Afegix el nou post al menú de navegació
*
#### Exercisi 712

Sobre el projecte blog anterior, afegirem aquests canvis:

* Fes que la funció **edit** del controlador de posts, en lloc de mostrar un missatge de text pla indicant que ací va un formulari, redirigisquen a la pàgina d'inici, usant la instrucció [**redirect**](#utilitzar-la-resposta-per-fer-redireccions) .
* Afig un [helper](#helperserviceprovider) al projecte que definisca una funció anomenada **fechaActual** . Rebrà com a paràmetre un format de data (per defecte, "d/m/Y") i traurà la data actual en aquest format. Utilitza-ho per a mostrar la data actual en format "d/m/Y" en la plantilla base alineada a la dreta de la barra de navegació.




