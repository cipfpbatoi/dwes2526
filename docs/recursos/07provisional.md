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
 DB\_CONNECTION=mysql
 DB\_HOST=mysql
 DB\_PORT=3306
 DB\_DATABASE=batoiBook
 DB\_USERNAME=root
 DB\_PASSWORD=1234
 
5. ** Afegix el phpmyadmin a docker-compose.yml**
 
 ```php
 myadmin:
 image: 'phpmyadmin:latest'
 ports:
 - 8080:80
 environment:
 MYSQL\_ROOT\_PASSWORD: '${DB\_PASSWORD}'
 links:
 - "mysql:db"
 depends\_on:
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

11. **Genera els node\_modules**

$ npm install

$ npm run build

Ara podeu obrir la vostra aplicació amb el vostre navegador: http://localhost

Ara que ja tenim tot el sistema preparat per a desenvolupar projectes Laravel, vegem els primers passos que hem de donar per a crear aquests projectes.

### Contenidor de Serveis de Laravel

El **Contenidor de Serveis** de Laravel és una eina poderosa per gestionar les dependències de classes i realitzar la injecció de dependències. Aquesta funcionalitat permet que les dependències es "injecten" a les classes a través del constructor o, en alguns casos, mitjançant mètodes "setter".

#### Resolució Automàtica Sense Configuració

Si una classe no té dependències o només depèn d'altres classes concretes (no interfícies), el contenidor pot resoldre-la automàticament sense configuració prèvia. Per exemple, si tens una classe `Service`, pots injectar-la directament en una ruta:

```php
use App\Services\Service;

Route::get('/', function (Service $service) {
    // Ús del servei
});

```
En aquest cas, Laravel resoldrà automàticament la instància de Service i la injectarà a la funció de la ruta.

#### Quan Utilitzar el Contenidor

Tot i que moltes dependències es poden injectar automàticament, hi ha situacions on és necessari interactuar manualment amb el contenidor:

- Quan una classe depèn d'una interfície i cal indicar al contenidor quina implementació ha de proporcionar.
- Quan es desenvolupa un paquet que s'integrarà amb Laravel i cal registrar serveis específics.

#### Enllaços al Contenidor

Per registrar una classe o interfície al contenidor, es pot utilitzar el mètode bind:

```php
use App\Services\Transistor;
use App\Services\PodcastParser;
use Illuminate\Contracts\Foundation\Application;

$this->app->bind(Transistor::class, function (Application $app) {
return new Transistor($app->make(PodcastParser::class));
});
```
En aquest exemple, es registra la classe Transistor al contenidor, especificant com s'ha de crear la seva instància.

#### Resolució de Dependències

Per obtenir una instància d'una classe registrada al contenidor, es pot utilitzar el mètode make:

```php
use App\Services\Transistor;

$transistor = $this->app->make(Transistor::class);

```
Això crearà una nova instància de Transistor amb totes les seves dependències resoltes.

### Proveïdors de Serveis en Laravel

Els **proveïdors de serveis** són el punt central de l'arrencada de qualsevol aplicació Laravel. Tant la teva aplicació com els serveis interns de Laravel es configuren i inicialitzen a través d'aquests proveïdors.

#### Funcions Principals

- **Registre de serveis**: Defineixen com es registren els serveis al contenidor de serveis de Laravel.
- **Inicialització**: Configuren serveis, escoltadors d'esdeveniments, middleware i rutes.

#### Estructura d'un Proveïdor de Serveis

Un proveïdor de serveis típic estendrà la classe `Illuminate\Support\ServiceProvider` i inclourà dos mètodes principals:

- `register`: Aquí es vinculen serveis al contenidor. No s'ha d'executar cap acció que depengui d'altres serveis.
- `boot`: S'executa després de registrar tots els proveïdors, permetent accedir a tots els serveis registrats.

```php
<?php

namespace App\Providers;

use Illuminate\Support\ServiceProvider;

class ExampleServiceProvider extends ServiceProvider
{
    public function register()
    {
        // Registre de serveis
    }

    public function boot()
    {
        // Inicialització de serveis
    }
}
```

#### Registre de Proveïdors

Els proveïdors de serveis es registren al fitxer bootstrap/providers.php. Quan crees un nou proveïdor amb Artisan, Laravel l'afegirà automàticament a aquest fitxer.

```bash
php artisan make:provider ExampleServiceProvider

```

#### Proveïdors Deferits

Per millorar el rendiment, alguns proveïdors es carreguen només quan són necessaris. Aquests es coneixen com a proveïdors deferits. Per definir un proveïdor com a deferit, implementa el mètode provides que retorna els serveis que ofereix.

```php
public function provides()
{
return [Service::class];
}
```


