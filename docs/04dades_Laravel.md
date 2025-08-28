# SA4. Accés segur i estructurat a bases de dades amb Laravel

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


## SA 4.2 Primeres operacions amb Eloquent (Laravel 12)

Aquesta secció introdueix les operacions bàsiques que podem realitzar amb models Eloquent: crear, llegir, actualitzar i esborrar registres, així com treballar amb relacions entre models, càrrega eficient de dades i paginació.

---

### ➕🗄️ Inserir dades

Per a inserir dades en una taula associada a un model, podem crear una instància del model, assignar els valors i guardar-los. També es pot utilitzar el mètode `create`, però en aquest cas cal definir prèviament la propietat `$fillable` al model per evitar insercions no autoritzades de topa.
 
```php
//  Crear i desar una nova instància 
$movie = new Movie();
$movie->titulo = "La guerra de las galaxias";
$movie->director = "George Lucas";
$movie->precio = 3.95;
$movie->save();

// Obtenir l'ID assignat
$insertedId = $movie->id;
 
// Ús del mètode create
Movie::create([
'titulo'   => $request->titulo,
'director' => $request->director,
'precio'   => $request->precio,
]);
//Cada camp de la petició ha de tindre associat un camp del mateix nom en el model.

// Hem de definir en el model una propietat anomenada **\$fillable** amb els noms dels camps
// de la petició que ens interessa processar (la resta es descarten). Això és obligatori especificar-ho,
// encara que ens interessen tots els camps, per a evitar insercions massives malintencionades (per exemple
//, editant el codi font per a afegir altres camps i modificar dades inesperades).
```

```php
// requereix $fillable al model
class Movie extends Model
{
protected $fillable = ['titulo', 'director', 'precio'];
}
```

---

###  ✏️🗄️ Modificar dades

Per actualitzar un registre, primer el localitzem (per exemple amb `findOrFail`), modifiquem les propietats necessàries i cridem a `save`. També existeix el mètode `update`, que permet fer-ho més ràpidament si la propietat `$fillable` està definida correctament.

```php
// Localitzar i modificar un registre 
$movie = Movie::findOrFail($id);
$movie->titulo = "Nou títol";
$movie->save();

// O bé, de forma concisa

Movie::findOrFail($id)->update($request->only(['titulo', 'director', 'precio']));

```
---

###  🗑️ Esborrar dades

Per eliminar un registre, es pot utilitzar el mètode `delete` aplicat sobre una instància del model. Cal considerar que aquesta operació s’ha de fer des de formularis o accions protegides, no mitjançant enllaços directes, per evitar vulnerabilitats (com les peticions GET per esborrar). En Laravel això es resol amb formularis que especifiquen el mètode HTTP `DELETE` i el token `@csrf`.

```php
// Eliminar un registre
Movie::findOrFail($id)->delete();

// En un controlador, simplemente en el mètode destroy

public function destroy($id)
{
    Movie::findOrFail($id)->delete();
    return redirect()->route('movies.index')->with('success', 'Eliminat correctament');
}
```

!!! Important: Fer servir formularis amb @method('DELETE') i @csrf per garantir seguretat i evitar peticions GET.

```bladehtml
<form action="{{ "{{  route('movies.destroy', $movie) " }}}}" method="POST">
	@method('DELETE')
	@csrf
	<button>Borrar</button>
</form>
```
---

###  🔗 Relacions bàsiques entre models

Eloquent facilita la definició de relacions entre models com a mètodes dins de les classes:

| Tipus de relació | Descripció breu |
|------------------|------------------|
| Un a u | Relacions 1:1, com `hasOne` i `belongsTo` |
| Un a molts | Relacions 1:N, com `hasMany` i `belongsTo` |
| Molts a molts | Relacions N:N amb `belongsToMany`, utilitzant taules pivot |

Eloquent també permet enllaçar fàcilment les consultes a aquestes relacions i recuperar els models relacionats com si fossin propietats d’un objecte.

####  UN A U (1:1)

```php
// en Usuari
public function telefon()
{
return $this->hasOne(Telefon::class);
}
// en Telefon:
public function usuari()
{
return $this->belongsTo(Usuari::class);
}

// Accedir a la relació

$telefono = Usuario::findOrFail($id)->telefon;

```

#### Un a Molts (1:M)

```php
// en Autor
public function libros()
{
return $this->hasMany(Libro::class);
}
// En Libro 
public function autor()
{
return $this->belongsTo(Autor::class);
}

// Accedir a la relació
$libros = Autor::findOrFail($id)->libros;
```
---

#### Molts a molts

```php
// en User
public function roles()
{
    return $this->belongsToMany(Role::class)->withTimestamps();
}
// en  Role:
public function users()
{
    return $this->belongsToMany(User::class);
}
// per accedir-hi 
$roles = User::findOrFail($id)->roles;
foreach ($roles as $rol) {
    echo $rol->pivot->created_at;
}
```


#### ⚡🔗 Accés eficient: Eager Loading

Quan obtenim registres amb relacions, Eloquent pot fer consultes addicionals per cada relació accedida de manera diferida. Amb **Eager loading** (`with`) podem indicar les relacions que volem carregar de manera anticipada, reduint considerablement el nombre de consultes i millorant el rendiment.

```php
//Evita el problema N+1 amb with():
$posts = Post::with('comments')->get();
//Aquest exemple carrega tots els posts i els seus comments associats amb només dues consultes a la base de dades.
```
---

#### 📑◀️▶️ Paginació

Per gestionar resultats de manera coŀlapsible, Laravel ofereix mètodes de paginació integrats (com `paginate()` i `simplePaginate()`), que faciliten la navegació entre grans llistats.
 
```php
public function index()
	{
		$movies = Movie::paginate(5);
		return view('movies.index', compact('moviemovies'));
	}
```

Després, en la vista associada ( **movies.index** en l'exemple anterior), podem emprar el mètode
links perquè mostre els botons de paginació en el lloc desitjat:

```bladehtml
	@forelse($movies as $movie)
		{{  $movie->titulo " }}
	@endforelse
	{{   $movies->links() }}
```
---

 ---

### 🧰 Resum visual de 4.2 – Primeres operacions amb Eloquent

| Acció             | Mètode                       | Notes                                              |
|------------------|------------------------------|----------------------------------------------------|
| 🔄 Llegir tot     | `Model::all()`               | Recupera tots els registres                       |
| 🔍 Buscar per ID  | `Model::find($id)`           | Retorna o `null` si no troba                      |
| ✅ Crear          | `Model::create([...])`       | Cal definir `$fillable`                           |
| ✏️ Actualitzar    | `Model::find($id)->update([...])` | També necessita `$fillable`                  |
| 🗑️ Esborrar       | `Model::find($id)->delete()` | Recomanat usar `findOrFail()`                     |

---

### 🔗 Tipus de relacions

| Relació       | Definició Model A         | Inversa Model B           |
|---------------|---------------------------|----------------------------|
| Un a u (1:1)  | `hasOne(ModelB::class)`   | `belongsTo(ModelA::class)` |
| Un a molts    | `hasMany(ModelB::class)`  | `belongsTo(ModelA::class)` |
| Molts a molts | `belongsToMany(ModelB::class)` | `belongsToMany(ModelA::class)` |

---

### ⚡️ Altres utilitats

| Funcionalitat     | Mètode                      | Finalitat                                         |
|------------------|-----------------------------|--------------------------------------------------|
| Eager loading    | `Model::with('relacio')->get()` | Evita consultes N+1                            |
| Paginació        | `Model::paginate(10)`       | Llista paginada amb 10 resultats per pàgina      |
| Taula pivot extra| `->withPivot('camp')`       | Accedir a camps extra en relació N:N             |
| Timestamp pivot  | `->withTimestamps()`        | Afegix `created_at` i `updated_at` a pivot       |

### 🔍 Introducció al Query Builder

Laravel proporciona una altra manera d’interactuar amb la base de dades a través del **Query Builder**, una eina que permet construir consultes SQL de forma més directa i eficient, però encara dins del marc de Laravel.

#### 📌 Quan usar-lo?
- Quan necessites **consultes més complexes** (joins, agregacions, subconsultes).
- Quan no calen **models Eloquent complets**.
- Per a consultes amb **millor rendiment** o més específiques.

---

#### 🧱 Exemple bàsic

```php
$movies = DB::table('movies')->get();
//Açò retorna totes les files de la taula movies com a objectes estàndard (no instàncies d’Eloquent).

```
#### 🔍 Amb condicions
```php
$cheapMovies = DB::table('movies')
                ->where('precio', '<', 5)
                ->orderBy('precio')
                ->get();
```php
#### 📊 Agregats

```php
$total = DB::table('movies')->count();
$max = DB::table('movies')->max('precio');
``` 

#### 🧩 Joins

```php
$peliculas = DB::table('movies')
    ->join('directores', 'movies.director_id', '=', 'directores.id')
    ->select('movies.*', 'directores.nom as director')
    ->get();
``` 

#### ⚠️ Diferències amb Eloquent

| **Eloquent**                        | **Query Builder**                   |
|------------------------------------|-------------------------------------|
| Retorna models Eloquent complets   | Retorna objectes estàndard (stdClass) |
| Suporta relacions automàtiques     | Cal fer joins manualment           |
| Permet guardar, modificar i esborrar registres | Només per a consultes (lectura) |
| Sintaxi més expressiva i OO        | Sintaxi més propera a SQL          |
| Ideal per a CRUD bàsics i mitjans  | Ideal per a consultes complexes    |
| Pot ser més lent en consultes grans| Més eficient per a grans volums    |

###  Referència

- Documentació oficial: [Eloquent ORM – Laravel 12](https://laravel.com/docs/12.x/eloquent)
- Vídeo d’introducció a les operacions amb Eloquent

## SA4.3  Patrons de disseny orientats a objectes 

### Principis SOLID (microresum)

- Single Responsibility: cada classe, una responsabilitat.
- Open/Closed: oberta a extensió, tancada a modificació.
- Liskov: substitució segura de tipus base per derivats.
- Interface Segregation: interfícies xicotetes i específiques.
- Dependency Inversion: dependències d’abstraccions, no implementacions.

### Patrons útils en Laravel

- DAO / Repository: aïlla l’accés a dades.
- Service (Domini / Aplicació): conté la lògica de negoci (regles).
- Factory: creació d’objectes (ja l’uses amb Models Factory).

**Arquitectura recomanada**

Controller  ->  Service  ->  Repository  ->  Eloquent Model
(presentació)   (negoci)      (accés dades)    (ORM)

### Exemple: Repository + Service

**Interfície del Repositori**
// app/Repositories/ProducteRepository.php
```php 
namespace App\Repositories;

use App\Models\Producte;
use Illuminate\Support\Collection;

interface ProducteRepository {
    public function tots(): Collection;
    public function crear(array $dades): Producte;
    public function actualitzar(Producte $p, array $dades): Producte;
    public function esborrar(Producte $p): void;
}
``` 

**Implementació Eloquent**
// app/Repositories/EloquentProducteRepository.php

```php 
namespace App\Repositories;

use App\Models\Producte;
use Illuminate\Support\Collection;

class EloquentProducteRepository implements ProducteRepository
{
    public function tots(): Collection   { return Producte::latest()->get(); }
    public function crear(array $d): Producte { return Producte::create($d); }
    public function actualitzar(Producte $p, array $d): Producte { $p->update($d); return $p; }
    public function esborrar(Producte $p): void { $p->delete(); }
}
``` 

**Servei de negoci**
// app/Services/ProducteService.php
``` 
namespace App\Services;

use App\Models\Producte;
use App\Repositories\ProducteRepository;

class ProducteService
{
public function __construct(private ProducteRepository $repo) {}

    public function llistar() { return $this->repo->tots(); }

    public function crear(array $dades): Producte
    {
        // Ex. lògica: descompte, normalització...
        if (isset($dades['preu'])) {
            $dades['preu'] = max(0, (float)$dades['preu']);
        }
        return $this->repo->crear($dades);
    }

    public function actualitzar(Producte $p, array $dades): Producte
    {
        return $this->repo->actualitzar($p, $dades);
    }

    public function esborrar(Producte $p): void
    {
        $this->repo->esborrar($p);
    }
}
``` 

**Binding al contenidor (Service Provider)**

// app/Providers/AppServiceProvider.php
``` 
use App\Repositories\ProducteRepository;
use App\Repositories\EloquentProducteRepository;

public function register(): void
{
$this->app->bind(ProducteRepository::class, EloquentProducteRepository::class);
}
``` 

**Controlador depenent del Servei**
// app/Http/Controllers/ProducteController.php
``` 
use App\Models\Producte;
use App\Services\ProducteService;
use Illuminate\Http\Request;

class ProducteController extends Controller
{
public function __construct(private ProducteService $svc) {}

    public function index()  { return view('productes.index', ['productes'=>$this->svc->llistar()]); }
    public function store(Request $r)   { $this->svc->crear($r->validate(['nom'=>'required','preu'=>'required|numeric|min:0'])); return back()->with('ok','Creat'); }
    public function update(Request $r, Producte $producte) { $this->svc->actualitzar($producte, $r->validate(['nom'=>'required','preu'=>'required|numeric|min:0'])); return back()->with('ok','Actualitzat'); }
    public function destroy(Producte $producte) { $this->svc->esborrar($producte); return back()->with('ok','Esborrat'); }
}
``` 

### ✅ Beneficis d'utilitzar Repository + Service en Laravel


| Benefici                            | Descripció                                                                 |
|-------------------------------------|----------------------------------------------------------------------------|
| 🔁 Reutilització de codi            | El codi de consultes i lògica de negoci es pot reutilitzar en diferents llocs. |
| 🧼 Separació de responsabilitats    | Cada capa fa una sola cosa: controlador presenta, servei decideix, repositori consulta. |
| 🧪 Facilita els tests               | Es poden substituir fàcilment per mocks en proves unitàries.               |
| 🔄 Facilita el manteniment         | Si canvies la BBDD o la lògica, no cal tocar controlador ni vistes.        |
| 🧱 Escalabilitat                    | Permet créixer el projecte sense que el codi es torne incontrolable.       |
| 👥 Col·laboració més clara          | Equips poden treballar en capes diferents sense solapar-se.                |
| 🧩 Canvi de backend o font de dades| Pots canviar MySQL per API externa o Mongo sense canviar la lògica.        |
| 📁 Organització clara del projecte  | Estructura neta i coherent per a projectes grans.                          |

### 🧩 Decisió d'ús de Repository i Service en Laravel

 
| Cas | Repository | Service | Explicació |
|-----|------------|---------|------------|
| CRUD simple (index, show, store, update, delete) | ❌ | ❌ | Eloquent cobreix tot |
| Consultes reutilitzables i complexes | ✅ | ❌ | Repository encapsula consultes |
| Vols canviar el backend (API, MongoDB, etc.) | ✅ | ❌ | Separació de dependències amb interface |
| Lògica de negoci específica (ex: descomptes, validacions especials) | ❌ | ✅ | La lògica no ha d'anar al controlador |
| Validacions de negocis en diverses rutes | ✅ | ✅ | Reutilització i separació de responsabilitats |
| Necessites *mockejar* dades en tests | ✅ | ✅ | Dependency Injection facilita proves |
| Controlador massa llarg o amb massa responsabilitats | ✅ | ✅ | Desacobles i neteges el codi |
| Backend ja madur, busques escalabilitat | ✅ | ✅ | Segueixes arquitectura neta i escalable |


 


 

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

##  Exercicis

###  🏟️ Exercici guiat: Reestructurar projecte Futbol Femení amb BD + Repository + Service

#### 🎯 Objectiu
Reestructurar l’aplicació de futbol femení (feta sense persistència) cap a una arquitectura escalable amb:
- Model Eloquent
- Migració i base de dades
- Repository + Service
- Validació amb FormRequest

---

#### 1. 🧱 Migració i model

##### 1.1 Crear migració
```bash
php artisan make:migration create_equips_table
php artisan make:migration create_estadis_table
```
Afegir els camps necessaris:

- (Equips)[https://github.com/Curs-2025-26/futbol-femeni/blob/bdd/database/migrations/2025_08_27_171209_create_equips_table.php]
- (Estadis)[https://github.com/Curs-2025-26/futbol-femeni/blob/bdd/database/migrations/2025_08_28_102228_create_estadis_table.php]

##### 1.2 Crear els models
```bash
php artisan make:model Equip
php artisan make:model Estadi
```
Definir els camps i les rel·lacions:




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
