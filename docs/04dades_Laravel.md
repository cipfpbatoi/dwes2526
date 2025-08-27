# SA4 – Accés segur i estructurat a bases de dades amb Laravel

??? abstract "Duració i criteris d'evaluació"

    Duració estimada: 16 hores

    <hr />

    | Resultat d'aprenentatge  | Criteris d'avaluació  |
    | ------                    | -----                |
    | RA6.-Desenvolupa aplicacions web d'accés a magatzems de dades, aplicant mesures per a mantindre la seguretat i la integritat de la informació. | a) S'han analitzat les tecnologies que permeten l'accés mitjançant programació a la informació disponible en magatzems de dades.<br/> b) S'han creat aplicacions que establisquen connexions amb bases de dades.<br/> c) S'ha recuperat informació emmagatzemada en bases de dades.<br/> d) S'ha publicat en aplicacions web la informació recuperada.<br/> e) S'han utilitzat conjunts de dades per a emmagatzemar la informació.<br/> f) S'han creat aplicacions web que permeten l'actualització i l'eliminació d'informació disponible en una base de dades.<br/> g) S'han provat i documentat les aplicacions web.
 
##  SA 4.1  Connexió a la base de dades
  
### 🔧 Configuració de la base de dades en Laravel

Per a poder treballar amb bases de dades en Laravel, el primer pas és configurar l’accés al sistema gestor de base de dades (SGBD) que vulguem utilitzar. En aquest cas, farem servir MySQL.
 
#### 📁 1. Fitxer `.env` i separació de configuracions

Laravel utilitza un sistema de variables d'entorn, que permet separar la configuració segons la màquina, l'entorn (desenvolupament, producció...), o l’usuari.
Aquesta configuració s’indica al fitxer `.env` que està a l’arrel del projecte. Allí definirem el tipus de connexió, el servidor, el nom de la base de dades, l’usuari i la contrasenya.

```env
DB_CONNECTION=mysql
DB_HOST=localhost
DB_PORT=3306
DB_DATABASE=nom_base_de_dades
DB_USERNAME=usuari
DB_PASSWORD=contrasenya
```

#### ⚙️ 2. Fitxer `config/database.php`

Aquest fitxer defineix com Laravel interpreta aquestes variables. Per exemple, a l’inici veuràs:

```php
'default' => env('DB_CONNECTION', 'mysql'),
```

Això significa que Laravel utilitzarà la base de dades especificada a la variable DB_CONNECTION. Si no s’ha definit al .env, utilitzarà 'mysql' per defecte.
Més avall, hi ha la secció connections amb les configuracions específiques per a cada tipus de base de dades. Per a MySQL:

```php
'mysql' => [
'driver' => 'mysql',
'host' => env('DB_HOST', '127.0.0.1'),
'port' => env('DB_PORT', '3306'),
'database' => env('DB_DATABASE', 'forge'),
'username' => env('DB_USERNAME', 'forge'),
'password' => env('DB_PASSWORD', ''),
...
],
``` 

#### 🔐 3. Contrasenya i paràmetres necessaris

Perquè Laravel puga connectar-se correctament a la base de dades, és necessari configurar correctament els valors següents en el fitxer `.env`:

- L’adreça del servidor.
- El nom de la base de dades.
- L’usuari.
- La contrasenya d’accés.

En un entorn local, l’adreça del servidor sol ser “localhost”.
 
#### 🧱 4. Crear la base de dades (fora de Laravel)

Laravel pot crear taules, relacions i introduir dades, però la base de dades com a contenidor l’has de crear prèviament de forma manual.
Pots fer-ho de dues maneres:

- ✅ Amb una eina gràfica com phpMyAdmin (si tens XAMPP, Laragon, etc.).
- ✅ Per línia de comandes, per exemple:

```bash
mysql -u root -p
CREATE DATABASE nom_base_de_dades;
``` 
Una vegada creada, Laravel ja podrà accedir-hi i començar a treballar amb ella (creant taules, inserint dades...).

### 🔄 Migracions a Laravel 12

Les migracions són un sistema de control de versions per a la base de dades. Permeten mantindre un registre dels canvis estructurals que es fan (crear, modificar o eliminar taules i camps), i facilitar que tot l’equip de treball tinga la base de dades sincronitzada.
Les migracions funcionen conjuntament amb l’eina Schema Builder per definir l’estructura de la base de dades utilitzant codi PHP.

---

#### 📁 1.Estructura i funcionament

Les migracions es troben a la carpeta `database/migrations`. Cada fitxer inclou un timestamp en el nom, que indica l’ordre d’execució. Cada migració conté dues funcions:

- `up`: per aplicar canvis (crear o modificar taules).
- `down`: per revertir els canvis aplicats.

Els fitxers de migració es creen mitjançant Artisan. És habitual trobar migracions per defecte en nous projectes Laravel (com la dels usuaris). Aquestes es poden modificar o eliminar segons les necessitats del projecte.

---

#### 🔧 2.Tipus de columnes i modificadors

A l’hora de definir les taules, Laravel proporciona molts tipus de columnes (`id`, `string`, `text`, `boolean`, `timestamp`...) i modificadors (`nullable`, `unique`, `default`, `after`, etc.).

Els camps `id` i `timestamps` solen afegir-se per defecte:

- `id`: clau primària auto-incremental.
- `timestamps`: afegeix `created_at` i `updated_at`, gestionats automàticament per Laravel.

Per columnes de text llarg, es recomana `text` o `longText` en lloc de `string`, que està limitat a 255 caràcters.

Per a definir claus primàries compostes, es pot utilitzar el mètode `primary`.

---

####  🛠️ 3.Crear una nova migració

Per a generar un fitxer de migració s’utilitza:

```bash
php artisan make:migration nom_de_la_migracio
```

Laravel analitza el nom de la migració i, si detecta patrons com `create_XXX_table` o `add_XXX_to_YYY_table`, assumeix el tipus d’operació.

També es poden especificar directament les opcions:

```bash
php artisan make:migration crear_tabla_equips --create=equips
php artisan make:migration afegir_telefon_a_usuaris --table=usuaris
```

---

#### 🔁 4.Modificar una taula existent

Per a afegir o llevar camps d’una taula ja creada, es fa una nova migració indicant que s’està treballant sobre una taula existent.
També es pot controlar l’ordre dels camps nous utilitzant modificadors com `after`.

---

#### 🚀 5.Executar migracions


```php
    // Per aplicar les migracions 
    php artisan migrate
    // Si es vol revertir l’última migració
    php artisan migrate:rollback
    // Si volem desfer totes les migracions
    php artisan migrate:reset
    // Un comanament interessant quan estem desenvolupant un nou lloc web és **migrate:refresh**, el qual desfarà tots els canvis i tornar a aplicar les migracions:
    php artisan migrate:fresh
``` 
 

#### 📐 6.Schema Builder

Una vegada creada una migració hem de completar els seus mètodes up i down per a indicar la taula que volem crear o el camp que volem modificar. En el mètode down sempre haurem d'afegir l'operació inversa, eliminar la taula que s'ha creat en el mètode up o eliminar la columna que s'ha afegit.

Açò ens permetrà desfer migracions deixant la base de dades en el mateix estat en el qual es trobaven abans que s'afegiren.

Per a especificar la taula a crear o modificar, així com les columnes i tipus de dades de les mateixes, s'utilitza la classe **Schema**. Aquesta classe té una sèrie de mètodes que ens permetrà especificar l'estructura de les taules independentment del sistema de base de dades que utilitzem.

##### Crear i esborrar una taula
Per a afegir una nova taula a la base de dades s'utilitza el següent constructor:

```php
	Schema::create('users', function (Blueprint $table) 	{ 
		$table->increments('id');
	});
``` 

On el primer argument és el nom de la taula i el segon és una funció que rep com a paràmetre un objecte
del tipus Blueprint que utilitzarem per a configurar les columnes de la taula.

En la secció down de la migració haurem d'eliminar la taula que hem creat, per a açò usarem algun dels
següents mètodes:

```php
	Schema::drop('users');
	Schema::dropIfExists('users');
``` 
En crear una migració amb el comando de Artisan make:migration ja ens ve aquest codi afegit per defecte, la creació i eliminació de la taula que s'ha indicat i a més s'afigen un parell de columnes per defecte (id i timestamps).

##### Afegir columnes
El constructor Schema::create rep com a segon paràmetre una funció que ens permet especificar les columnes que va a tenir aquesta taula.

En aquesta funció podem anar afegint tots els camps que vulguem, indicant per a cadascun d'ells el seu tipus i nom, i a més si volem també podrem indicar una sèrie de modificadors com a valor per defecte, índexs, etc. Per exemple:

```php
	Schema::create('users', function($table) {
		$table->increments('id'); 
		$table->string('username', 32); 
		$table->string('password'); 
		$table->smallInteger('vots'); 
		$table->string('direccion'); 
		$table->boolean('confirmat')->default(false);
		$table->timestamps();
	});
```

Schema defineix molts tipus de dades que podem utilitzar per a definir les columnes d'una taula, alguns dels principals són:

|Comando|Tipus de camp|
|--|--|
|$table->boolean('confirmed');| BOOLEAN|
|$table->enum('choices', array('foo', 'bar'));| ENUM |
|$table->float('amount');| FLOAT|
|$table->increments('id');| Clau principal tipus INTEGER amb Acte-Increment| 
|$table->integer('votes');| INTEGER|
|$table->mediumInteger('numbers');| MEDIUMINT|
|$table->smallInteger('votes');| SMALLINT|
|$table->tinyInteger('numbers');| TINYINT|
|$table->string('email');| VARCHAR|
|$table->string('name', 100);| VARCHAR amb la longitud indicada TEXT|
|$table->text('description');| TEXT|
|$table->timestamp('added_on');| |TIMESTAMP|
|$table->timestamps();|Afig els timestamps "created_at" i "updated_at"|
|->nullable()|Indicar que la columna permet valors NULL|
|->default($value)|Declara un valor per defecte per a una columna|
|->unsigned()|Afig UNSIGNED a les columnes tipus INTEGER|

Els tres últims es poden combinar amb la resta de tipus per a crear, per exemple, una columna que permeta nuls, amb un valor per defecte i de tipus unsigned.

Per a consultar tots els tipus de dades que podem utilitzar podeu consultar la documentació de Laravel [en](http://laravel.com/docs/8.x/migrations#creating-columns):

##### Afegir índexs

Schema suporta els següents tipus d'índexs:

| Comanament                               | Descripció|
|------------------------------------------|--|
| $table->id();                            |Afegir un clau primària id|
| $table->primary('id');                   | Afegir una clau primària|
| $table->primary(array('first', 'last')); | Definir una clau primària composta|
| $table->unique('email');                 |  Definir el camp com UNIQUE|
| $table->index('state');                  |Afegir un índex a una columna|

En la taula s'especifica com afegir aquests índexs després de crear el camp, però també permet indicar aquests índexs alhora que es crea el camp:

```php
	$table->string('email')->unique();
```

##### Claus alienes
Amb Schema també podem definir claus alienes entre taules:

```php
	$table->foreignId('module_id')->constrained('modules');
 	$table->foreign('module_id')->references('code')->on('modules');
```

En el primer exemple, a més de crear el camp crea la rel·lacio, i serveix si la clau a la que faig referència s'ha creat utilitzant $table->id();

En cas contrari he d'especificar el camp ja creat i on es rel·laciona.

La columna amb la clau aliena ha de ser del **mateix tipus** que la columna a la qual apunta. Si per exemple vam crear una columna a un índex auto-incremental haurem d'especificar que la columna siga **unsigned** per que no es produïsquen errors.

També podem especificar les accions que s'han de realitzar per a "**on delete**" i "**on update**":

```php
	$table->foreign('user_id')->references('id')->on('users')->onDelete('cascade');
```

###  🧩 Models de dades amb Eloquent ORM (Laravel 12)

L’**Object-Relational Mapping (ORM)** és una tècnica que permet treballar amb una base de dades relacional utilitzant **objectes** en lloc de consultes SQL directes. Laravel inclou el seu propi ORM anomenat **Eloquent**, que permet fer operacions sobre la base de dades de forma molt intuïtiva.

Amb Eloquent, cada **model** representa una **taula** de la base de dades, i cada **instància del model** representa un registre d’aquesta taula.

---

### 🔧 Creació d’un model

Els models es creen dins la carpeta `app/Models`. Per generar-ne un:

```php
     //  crearà una classe `Movie` associada, per defecte, a la taula `movies`. Si la taula té un nom diferent, podem indicar-ho al model amb la propietat `$table`.
    php artisan make:model Movie
     // Model + migració 
    php artisan make:model Movie -m
     // Model + migració + controlador buit 
    php artisan make:model Movie -mc
     // Model + migració + controlador de recursos 
    php artisan make:model Movie -mcr
```
---

### 📐 Bones pràctiques de nomenclatura

És recomanable mantindre una coherència entre:

- Model → `Movie`
- Controlador → `MovieController`
- Taula → `movies`
- Vistes → `resources/views/movies/index.blade.php`, etc.

---

#### 🔑 Propietats especials dels models

- `$primaryKey`: per indicar una clau primària diferent de `id`.
- `$timestamps = false`: si la taula no té camps `created_at` i `updated_at`.

Exemple de definició completa:

```php
class User extends Model
{
    protected $table = 'my_users';
    protected $primaryKey = 'my_id';
    public $timestamps = false;
}
```

#### 📥 Ús dels models per a consultar dades

Una vegada creat el model, es pot utilitzar en els controladors per consultar la base de dades i passar la informació a les vistes.

#####  Consultes bàsiques

 
```php

// Tots els registres 
$movies = Movie::all();
// Condicionals 
$movies = Movie::where('precio', '<', 10)->get();
 // Ordre
$movies = Movie::orderBy('titulo', 'desc')->get();
// Funcions agregades 
$total = Movie::count();
$max = Movie::max('preu');
$min = Movie::min('preu');
$avg = Movie::avg('preu');
$sum = Movie::sum('preu');
```

### 🌱 Seeders i 🏭 Factories en Laravel 12

Qun estem desenvolupant una aplicació, sovint necessitem disposar de **dades de prova** per poder treballar amb consultes, validacions, formularis, etc. Laravel ens ofereix dues eines molt útils per generar aquestes dades: els **seeders** i els **factories**.

---

#### 🌱 Seeders (Sembradors de dades)

Els **seeders** són classes que permeten **inserir dades inicials** a la base de dades de forma programada.

##### Crear un seeder

Per crear un seeder:

    php artisan make:seeder NomDelSeeder


Es crearà una classe dins `database/seeders`. Dins del mètode `run()` podrem escriure les instruccions per crear els registres.

##### Registrar el seeder

Perquè s’execute, cal registrar-lo al `DatabaseSeeder.php`:

```php
$this->call(NomDelSeeder::class); 
``` 
###### Executar els seeders
Per executar tots els seeders registrats:

```php
php artisan db:seed
```

Per netejar i tornar a sembrar la base de dades:

```php
php artisan migrate:fresh --seed
```

### 🏭 Factories (Fàbriques de dades)

Els factories permeten generar dades falses de manera automatitzada i en gran quantitat.

#### Crear una factory
Per crear una factory:

```php
php artisan make:factory NomDelModelFactory
``` 
Es crearà dins database/factories una classe associada automàticament al model corresponent.

#### Definir la factory
En el mètode definition(), s’utilitza el sistema faker per generar dades aleatòries (noms, correus, dates...).
Els models han d’incloure el trait HasFactory per poder utilitzar les factories.

#### 🧪 Exemple de seeder amb factory
Un seeder pot usar una factory per generar múltiples registres:
```php
User::factory()->count(10)->create();
``` 
Per generar dades relacionades:

```php
$usuaris = User::all();
$usuaris->each(function($usuari) {
Post::factory()->count(2)->create([
'user_id' => $usuari->id
]);
});
```

#### 🧰 Resum

| Eina       | Finalitat                                                  |
|------------|------------------------------------------------------------|
| Seeder     | Inserir dades específiques o inicials                      |
| Factory    | Generar dades aleatòries amb estructura definida           |
| Faker      | Generador integrat per crear valors falsos                 |

---

#### 📚 Referència

- [Laravel Docs – Database Seeding](https://laravel.com/docs/12.x/seeding)
- [Laravel Docs – Model Factories](https://laravel.com/docs/12.x/database-testing#defining-model-factories)


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




###  📎  Annex I: Instal·lació de phpMyAdmin amb Docker (opcional)

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
I ara, ja podem accedir a http://localhost:8080 amb les credencials del .env.
