# ** Gestió de Dades amb Laravel  **

## **1. Introducció**
Laravel és un framework PHP modern que simplifica el desenvolupament d'aplicacions web, incloent-hi la gestió de bases de dades. La integració amb Eloquent, el seu ORM (Object-Relational Mapping), permet treballar amb bases de dades de forma intuïtiva i eficient.
 
## **2. Configuració inicial**
Laravel suporta diversos motors de bases de dades com MySQL, PostgreSQL, SQLite i SQL Server. La configuració principal es fa al fitxer `.env` i `config/database.php`.

**Exemple de configuració al fitxer `.env`:**
```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=nom_base_de_dades
DB_USERNAME=usuari
DB_PASSWORD=contrasenya
```

**Comprovació de connexió:**

Després de configurar el `.env`, utilitza el comandament:
```bash
php artisan migrate:status
```
Aquest comandament confirma si Laravel pot connectar-se a la base de dades configurada.

#### **Detecció de problemes comuns**

- Comprovar que l'extensió del driver de la base de dades (com `pdo_mysql` o `pdo_pgsql`) estigui habilitada al `php.ini`.
- Utilitzar `php artisan config:clear` per esborrar la memòria cau de configuracions si els canvis al `.env` no es reflecteixen. 

## **3. Migracions en Laravel  **

### **Introducció**
Les migracions són un sistema de control de versions per a bases de dades que permet treballar de manera col·laborativa, mantenint un històric dels canvis realitzats en l'esquema. Amb migracions, pots:
- Crear, modificar i esborrar taules.
- Gestionar l'esquema de manera programàtica utilitzant Artisan i el **Schema Builder**.
- Revertir canvis mitjançant `rollback` o tornar a aplicar tots els canvis amb `refresh`.

Laravel proporciona un conjunt d'eines intuïtives per gestionar migracions, com Artisan i la classe **Schema**.
 
### **Estructura de les migracions**
Totes les migracions es guarden a la carpeta `database/migrations` i segueixen una estructura predefinida amb dos mètodes principals:
- **`up`**: Defineix les operacions que s'han d'aplicar a la base de dades (crear taules, afegir columnes, etc.).
- **`down`**: Defineix les operacions inverses per revertir els canvis aplicats per `up`.

Exemple bàsic:
```php
public function up()
{
    Schema::create('usuarios', function (Blueprint $tabla) {
        $tabla->id();
        $tabla->string('nombre');
        $tabla->string('email')->unique();
        $tabla->timestamps();
    });
}

public function down()
{
    Schema::dropIfExists('usuarios');
}
```

Per defecte, Laravel afegeix un camp autonumèric `id` i dues columnes `timestamps` (`created_at` i `updated_at`) gestionades automàticament.

 
### **Crear una migració**
Utilitza Artisan per crear una nova migració:
```bash
php artisan make:migration nom_migracio
```

Aquest comando genera un fitxer amb un nom que inclou un **timestamp** per assegurar l'ordre cronològic.

### **Exemples**
- Crear una taula:
```bash
php artisan make:migration crear_tabla_usuarios --create=usuarios
```

- Modificar una taula existent:
```bash
php artisan make:migration afegir_camp_a_usuarios --table=usuarios
```

Laravel pot inferir accions del nom de la migració gràcies a la classe **TableGuesser**. Per exemple, si el nom conté `create` o `to`, Artisan deduirà si és per crear o modificar taules.

 
### **Schema Builder**
La classe **Schema** és el nucli per definir i modificar l'esquema de les bases de dades. Inclou constructors per crear, modificar i eliminar taules i columnes.

#### **Crear una taula**
```php
Schema::create('users', function (Blueprint $table) {
    $table->id();
    $table->string('username', 32);
    $table->timestamps();
});
```

#### **Eliminar una taula**
```php
Schema::dropIfExists('users');
```

#### **Afegir columnes**
```php
Schema::table('usuarios', function (Blueprint $table) {
    $table->string('telefono')->after('email')->nullable();
});
```

#### **Eliminar columnes**
```php
Schema::table('usuarios', function (Blueprint $table) {
    $table->dropColumn('telefono');
});
```
 
### **Tipus de columnes disponibles**
Laravel ofereix una àmplia varietat de tipus de columnes per satisfer diferents [necessitats](https://laravel.com/docs/11.x/migrations#available-column-types) 
  
### **Índexs i claus forànies**
#### **Crear índexs**
```php
$table->unique('email');
$table->index('state');
$table->primary(['first_name', 'last_name']);
```

#### **Definir claus forànies**
```php
$table->foreignId('user_id')->constrained()->onDelete('cascade');
```
 
### **Executar i revertir migracions**
- **Executar migracions pendents:**
```bash
php artisan migrate
```

- **Revertir l'última migració:**
```bash
php artisan migrate:rollback
```

- **Revertir totes les migracions:**
```bash
php artisan migrate:reset
```

- **Refrescar totes les migracions:**
```bash
php artisan migrate:refresh
```

- **Comprovar l'estat de les migracions:**
```bash
php artisan migrate:status
```

Aquest conjunt de comandes permet un control complet sobre l'estat de les migracions durant el desenvolupament.
 

##  **4. Laravel Query Builder**

El **Query Builder** de Laravel proporciona una interfície fluida per construir i executar consultes de bases de dades. Permet treballar amb diverses bases de dades de manera senzilla sense escriure SQL brut.

---

### **Exemples d'ús**

#### Obtenir tots els registres:
```php
$users = DB::table('users')->get();
```

#### Filtrar registres:
```php
$users = DB::table('users')
    ->where('active', 1)
    ->get();
```

#### Seleccionar columnes específiques:
```php
$users = DB::table('users')
    ->select('name', 'email')
    ->get();
```
 
#### Ordenar resultats:
```php
$users = DB::table('users')
    ->orderBy('name', 'asc')
    ->get();
```

#### Comptar registres:
```php
$count = DB::table('users')->count();
```

#### Consultes amb agregats:
```php
$maxSalary = DB::table('employees')->max('salary');
```
 
#### Consultes amb subconsultes:
```php
$users = DB::table('users')
    ->whereExists(function ($query) {
        $query->select(DB::raw(1))
              ->from('orders')
              ->whereColumn('orders.user_id', 'users.id');
    })
    ->get();
```

#### Unions:
```php
$first = DB::table('users')->where('type', 'admin');
$second = DB::table('users')->where('type', 'customer');

$users = $first->union($second)->get();
```
#### Inserir un registre:
```php
DB::table('users')->insert([
    'name' => 'John Doe',
    'email' => 'john@example.com',
]);
```
#### Actualitzar un registre:
```php
DB::table('users')
    ->where('id', 1)
    ->update(['name' => 'Updated Name']);
```
#### Esborrar un registre:
```php
DB::table('users')
    ->where('id', 1)
    ->delete();
```

#### Esborrar tots els registres:
```php
DB::table('users')->truncate();
```
  
###  **Avantatges**
El Query Builder és ideal per a:

- Consultes personalitzades on el rendiment és una prioritat.
- Consultes complexes que no es poden expressar fàcilment amb Eloquent.

---
 

## **5.Laravel Eloquent**

Eloquent és l'ORM (Object-Relational Mapping) de Laravel. Proporciona una interfície senzilla i elegant per treballar amb bases de dades relacionals mitjançant models.
 
### **Definició de Models**

Els models es defineixen dins de la carpeta `app/Models` i es poden crear mitjançant Artisan:
```bash
php artisan make:model Movie
```

#### Exemple bàsic:
```php
namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class Movie extends Model
{
    // Taula associada al model
    protected $table = 'movies';
}
```

Per defecte:
- El model s'associa a una taula plural (`movies` per al model `Movie`).
- Utilitza `id` com a clau primària.
- Assumeix l'ús de camps `created_at` i `updated_at` gestionats automàticament.
 
### **Ús bàsic d'un model**
#### Recuperar dades:
- Tots els registres:
```php
$movies = Movie::all();
```

- Registres filtrats:
```php
$movies = Movie::where('rating', '>', 4)->get();
```

- Registre únic:
```php
$movie = Movie::findOrFail($id);
```

#### Inserir dades:
```php
$movie = new Movie();
$movie->title = "Inception";
$movie->director = "Christopher Nolan";
$movie->save();
```

#### Actualitzar dades:
```php
$movie = Movie::find($id);
$movie->title = "Updated Title";
$movie->save();
```

#### Esborrar dades:
```php
$movie = Movie::find($id);
$movie->delete();
```
 
### **Relacions en Eloquent**

#### 1. **Un a un (One-to-One):**
Un usuari té un perfil:
```php
class User extends Model
{
    public function profile()
    {
        return $this->hasOne(Profile::class);
    }
}

$user = User::find(1);
$profile = $user->profile;
```

#### 2. **Un a molts (One-to-Many):**
Un autor té molts llibres:
```php
class Author extends Model
{
    public function books()
    {
        return $this->hasMany(Book::class);
    }
}

$author = Author::find(1);
$books = $author->books;
```

#### 3. **Molts a molts (Many-to-Many):**
Un usuari té molts rols:
```php
class User extends Model
{
    public function roles()
    {
        return $this->belongsToMany(Role::class);
    }
}

$user = User::find(1);
$roles = $user->roles;
```

#### 4. **Has Many Through (Relacions transitives):**
Permet accedir a dades relacionades a través d'un altre model.
```php
class Country extends Model
{
    public function posts()
    {
        return $this->hasManyThrough(Post::class, User::class);
    }
}
```
 
### **Eager Loading (Càrrega eficient de relacions)**

Per evitar múltiples consultes a la base de dades, pots carregar relacions amb `with`:
```php
$authors = Author::with('books')->get();
```
 
### **Col·leccions i Agrupacions**

Eloquent retorna col·leccions per defecte, que permeten treballar amb [mètodes](https://laravel.com/docs/11.x/eloquent-collections#available-methods)  
 
 
### **Mutators i Accessors**

Els **mutators** permeten transformar dades abans de guardar-les, i els **accessors** les transformen en recuperar-les.

#### Exemple:
```php
class User extends Model
{
    // Accessor
    public function getFullNameAttribute()
    {
        return "{$this->first_name} {$this->last_name}";
    }

    // Mutator
    public function setPasswordAttribute($value)
    {
        $this->attributes['password'] = bcrypt($value);
    }
}
```

#### Ús:
```php
$user = User::find(1);
$fullName = $user->full_name;

$user->password = 'new_password';
$user->save();
```

---

### **Paginació**

Laravel facilita la paginació:
```php
$movies = Movie::paginate(10);
```

En la vista:
```php
{{ $movies->links() }}
```
 