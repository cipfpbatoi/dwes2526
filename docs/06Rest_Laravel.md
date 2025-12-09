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

# Servicios REST


## 📘 Introducció als serveis REST


Una **API** (Application Programming Interface) és un conjunt de funcions i procediments pels quals, una aplicació externa accedeix a les dades, a manera de biblioteca com una capa d'abstracció i la API s'encarrega d'enviar la dada sol·licitada.

Una de les característiques fonamentals de les API és que són **Stateless**, la qual cosa vol dir que les peticions es fan i desapareixen, no hi ha usuaris loguejats ni dades que es queden emmagatzemats.

### 🧭 Característiques fonamentals de REST:
- **Stateless**: Cada petició HTTP conté tota la informació necessària per processar-la.
- **Mètodes HTTP**: Utilitza mètodes com GET, POST, PUT i DELETE.
- **Formats d'intercanvi de dades**: Habitualment JSON o XML.
 

## 🌐 Els serveis REST

### 🔍 Consultar una API externa

Per consultar una API externa com https://swapi.dev/ des de Laravel, pots utilitzar la biblioteca HTTP client de Laravel, que proporciona una interfície senzilla per a realitzar peticions HTTP. Ací tens un exemple de com fer una petició GET per a obtenir informació sobre personatges de "Star Wars":

**Client HTTP (Laravel 12):**
El client HTTP de Laravel ja ve preparat amb Guzzle de sèrie. Només caldria afegir `composer require guzzlehttp/guzzle` si l'has eliminat del `composer.json`.

```bash
composer require guzzlehttp/guzzle
```

**Realitza una Petició GET:**
Després, pots utilitzar el facade Http per a realitzar una petició GET. Aquí tens un exemple de com consultar informació sobre personatges:

```php
use Illuminate\Support\Facades\Http;

public function getStarWarsCharacters()
{
    $response = Http::get('https://swapi.dev/api/people/');

    if ($response->successful()) {
        $data = $response->json();
        // Manipula o mostra les dades com necessites
    } else {
        // Maneja l'error
    }
}
```

En aquest exemple, la petició GET a https://swapi.dev/api/people/ retorna informació sobre personatges de "Star Wars". La resposta es verifica per a comprovar si ha estat exitosa, i després es processen les dades JSON. Pots adaptar aquest codi per a fer altres tipus de consultes a l'API, depenent de la informació que necessites.
 

### 🛠️ Construïnt una API/REST bàsica amb Laravel

Amb aquesta metodologia anomenada **REST** podrem construir *APIs* perquè des d'un client extern es puguen consumir.

Gràcies a aquest **standard** de l'arquitectura del programari podrem muntar una API que utilitze els mètodes standard GET, POST, PUT , PATCH i DELETE.


#### Instal·lació Laravel Sanctum

Laravel Sanctum proporciona un sistema lleuger d'autenticació dissenyat per a SPAs (Single Page Applications), aplicacions mòbils i APIs senzilles basades en tokens. Amb Sanctum, cada usuari de la teua aplicació pot generar diversos tokens d'API, cadascun amb habilitats o permisos específics que defineixen quines accions poden realitzar amb aquests tokens.

Sanctum resol dues necessitats d'autenticació diferents. Vegem cadascuna abans d'entrar en detall.

##### **1. Tokens d'API**

Sanctum és un paquet senzill que et permet emetre tokens d'API als teus usuaris sense la complexitat d'OAuth. Aquesta funcionalitat està inspirada en plataformes com GitHub, que proporcionen "tokens d'accés personal". Per exemple, la pàgina de configuració del compte de la teua aplicació podria incloure una secció on els usuaris generen tokens d'API per als seus comptes. Aquests tokens solen tindre un temps d'expiració molt llarg (per exemple, anys), però poden ser revocats manualment pels usuaris en qualsevol moment.

Sanctum implementa aquesta funcionalitat mitjançant:
- L'emmagatzematge dels tokens d'API en una taula específica de la base de dades.
- L'autenticació de les peticions HTTP entrants mitjançant l'encapçalament `Authorization`, que ha d'incloure un token d'API vàlid.


##### **2. Autenticació per a SPAs**

Sanctum també ofereix una forma senzilla d'autenticar aplicacions de pàgina única (SPAs) que necessiten comunicar-se amb una API desenvolupada amb Laravel. Aquestes SPAs poden formar part del mateix repositori que la teua aplicació Laravel o ser un repositori totalment separat, com una SPA desenvolupada amb Next.js o Nuxt.

Per a aquesta funcionalitat:
- Sanctum **no utilitza tokens**, sinó que empra els serveis d'autenticació de sessió basats en galetes (cookies) ja integrats en Laravel.
- Normalment, utilitza el sistema d'autenticació web de Laravel per aconseguir-ho, oferint protecció contra CSRF, autenticació de sessió i prevenció de filtracions de credencials mitjançant XSS.

Sanctum només intentarà autenticar-se amb galetes si la petició prové del frontend de la SPA de la teua pròpia aplicació. Quan Sanctum examina una petició HTTP, comprova primer si existeix una galeta d'autenticació. Si no n'hi ha cap, llavors examina l'encapçalament `Authorization` per a un token d'API vàlid.

##### Instal·lació

En Laravel 12 `php artisan install:api` ja deixa Sanctum preparat (migra la taula i registra el middleware). Només hauries de fer `composer require laravel/sanctum` si l'has eliminat.

Es pot instal·lar amb el comanament d'artisan

```bash
php artisan install:api
```

Vegem ara quins passos donar per a construir una API REST en Laravel que done suport a les operacions bàsiques sobre una o diverses entitats: consultes (GET), insercions (POST), modificacions (PUT) i esborrats (DELETE). Emprarem per a això els denominats controladors de API i que proporcionen un conjunt de funcions ja definides per a donar suport a cadascun d'aquests comandos.



#### Definint els controlador de la API

Per a proporcionar una API REST als clients que ho requerisquen, necessitem definir un controlador (ocontroladors) orientats a oferir aquests serveis REST. Aquests controladors en Laravel es denominen de tipus **api**, com vam veure en sessions prèvies. Normalment es definirà un controlador API per cadascun dels models als quals necessitem accedir. 

```php
php artisan make:controller Api/JugadoraController --api --model=Jugadora
```

Això crearà el controlador en la carpeta **App\Http\Controllers\Api** amb una sèrie de funcions ja predefinides. No és obligatori situar-ho en aqueixa subcarpeta, òbviament, però això ens servirà per a separar els controladors de API de la resta. Aquesta serà l'aparença del controlador generat:

```php
<?php

namespace App\Http\Controllers\Api;

use App\Http\Controllers\Controller;
use App\Models\Jugadora;
use Illuminate\Http\Request;

class JugadoraController extends Controller
{
    /**
     * Display a listing of the resource.
     *
     * @return \Illuminate\Http\Response
     */
    public function index()
    {
        //
    }

    /**
     * Store a newly created resource in storage.
     *
     * @param  \Illuminate\Http\Request  $request
     * @return \Illuminate\Http\Response
     */
    public function store(Request $request)
    {
        //
    }

    /**
     * Display the specified resource.
     *
     * @param  \App\Models\Jugadora  $jugadora
     * @return \Illuminate\Http\Response
     */
    public function show(Jugadora $jugadora)
    {
        //
    }

    /**
     * Update the specified resource in storage.
     *
     * @param  \Illuminate\Http\Request  $request
     * @param  \App\Models\Jugadora  $jugadora
     * @return \Illuminate\Http\Response
     */
    public function update(Request $request, Jugadora $jugadora)
    {
        //
    }

    /**
     * Remove the specified resource from storage.
     *
     * @param  \App\Models\Jugadora  $jugadora
     * @return \Illuminate\Http\Response
     */
    public function destroy(Jugadora $jugadora)
    {
        //
    }
}
```

Observem que s'incorpora automàticament la clàusula use per a carregar el model associat, que hem indicat en el paràmetre **--model** . A més, els mètodes show , update i destroy ja vénen amb un paràmetre de tipus Jugadora que facilitarà molt algunes tasques.

##### Establint les rutes (endPoints)


Una vegada tenim el controlador API creat, definirem les rutes associades a cada mètode del controlador. Podem emprar el mètode **Route::apiResource** en l'arxiu
**routes/api.php** per a establir automàticament totes les rutes d'un controlador de API. Afegim aquesta línia en aquest arxiu **routes/api.php** :

```
Route::apiResource('jugadores', Api\JugadoraController::class)
    ->parameters(['jugadores' => 'jugadora']);
```

Recorda importar el controlador: `use App\Http\Controllers\Api\JugadoraController;`.

Les rutes de API (aquelles definides en l'arxiu **routes/api.php** ) per defecte tenen un prefix api , tal com s'estableix en el provider **RouteServiceProvider** . Per tant, hem definit una
ruta general **api/jugadores** , de manera que totes les subrutes que es deriven d'ella portaran a l'un o l'altre mètode del controlador de API de jugadores.
Podem comprovar quines rutes hi ha actives amb aquest comando:

```
php artisan route:list

+--------+-----------+--------------------------+-------------------+-----------------------------------------------------+------------+
| Domain | Method    | URI                      | Name              | Action                                              | Middleware |
+--------+-----------+--------------------------+-------------------+-----------------------------------------------------+------------+
|        | GET|HEAD  | api/jugadores            | jugadores.index   | App\Http\Controllers\Api\JugadoraController@index   | api        |
|        | POST      | api/jugadores            | jugadores.store   | App\Http\Controllers\Api\JugadoraController@store   | api        |
|        | GET|HEAD  | api/jugadores/{jugadora} | jugadores.show    | App\Http\Controllers\Api\JugadoraController@show    | api        |
|        | PUT|PATCH | api/jugadores/{jugadora} | jugadores.update  | App\Http\Controllers\Api\JugadoraController@update  | api        |
|        | DELETE    | api/jugadores/{jugadora} | jugadores.destroy | App\Http\Controllers\Api\JugadoraController@destroy | api        |

```

### 📥 Serveis GET

Començarem per definir el mètode index . En aquest cas, obtindrem el conjunt de jugadores de la base de dades i retornar-lo tal qual:

```php
public function index()
{
    $jugadores = Jugadora::get();
    return $jugadores;
}
```

Si accedim a la ruta **api/jugadores** des del navegador, s'activarà el mètode index que acabem d'implementar, i rebrem les jugadores de la base de dades, directament en format JSON.

```json
[
  {
    "id": 1,
    "nom": "Aitana Bonmatí",
    "equip": "FC Barcelona",
    "posicio": "Migcampista",
    "dorsal": 14,
    "edat": 26,
    "created_at": "2024-03-01T11:19:19.000000Z",
    "updated_at": "2024-04-01T10:36:20.000000Z"
  },
  {
    "id": 2,
    "nom": "Alexia Putellas",
    "equip": "FC Barcelona",
    "posicio": "Migcampista",
    "dorsal": 11,
    "edat": 29,
    "created_at": "2024-03-02T11:19:19.000000Z",
    "updated_at": "2024-03-02T11:19:19.000000Z"
  }
]
```


D'una forma similar, podríem implementar i provar el mètode show

```php
public function show(Jugadora $jugadora)
{
    return $jugadora;
}
```

En aquest cas, si accedim a la URI **api/jugadores/1** , obtindrem la informació de la jugadora amb id = 1. Notar que Laravel s'encarrega automàticament de buscar el registre per nosaltres (fer la corresponent operació **find** per a l'id proporcionat). És el que es coneix com a enllaç implícit, i és alguna cosa que també està disponible en els controladors web normals, sempre que els associem correctament amb el model vinculat. Això es fa automàticament si creem el controlador juntament amb el model o si usem el paràmetre --model per a associar-ho, com hem fet ací.

#### Maneig de Respostes JSON en Laravel

Laravel ofereix diverses eines per gestionar respostes JSON, ja siga directament o utilitzant API Resources. Aquesta guia mostra com personalitzar les respostes, controlar els camps visibles i gestionar la paginació.

##### 1. Ús de `response()->json()`

Aquest mètode et permet retornar respostes JSON personalitzades amb un codi d'estat específic.

```php
public function show(Jugadora $jugadora)
{
    return response()->json($jugadora, 200); // JSON amb codi 200 (èxit)
}

```


| Codi | Significat                   |
|------|-------------------------------|
| 200  | Operació correcta.            |
| 201  | Recurs creat (ex. POST).      |
| 204  | Sense contingut (ex. DELETE). |
| 400  | Petició incorrecta.           |
| 404  | No trobat.                    |
| 500  | Error del servidor.           |

##### 2. Camps Ocults o Visibles en Models

Laravel permet configurar directament al model quins camps es mostraran o s'ocultaran a les respostes JSON.

- **Ocultar camps:** Utilitza la propietat `hidden` en el model.

```php
protected $hidden = ['password'];
``` 

- **Mostrar només camps seleccionats:** Utilitza la propietat `visible` en el model.

```php
protected $visible = ['id', 'name', 'email'];
```

##### 3. Personalització Directa a Controladors

Si necessites un control més gran sobre els camps retornats, pots definir manualment un array al controlador.

```php
public function show(Jugadora $jugadora)
{
    return [
        'nom' => $jugadora->nom,
        'equip' => $jugadora->equip,
    ];
}

```

##### 4. Ús de Recursos (API Resources)

Els **API Resources** permeten controlar millor el format de les respostes JSON, separant la lògica de transformació del model.

**Generar un recurs:**
Es pot generar un recurs amb Artisan, i aquest recurs s'utilitza per personalitzar les dades que es retornen.

```php
php artisan make:resource JugadoraResource
```

**Definir el format al reecurs**

```php
namespace App\Http\Resources;

use Illuminate\Http\Resources\Json\JsonResource;

class JugadoraResource extends JsonResource
{
    public function toArray($request)
    {
        return [
            'id' => $this->id,
            'nom' => $this->nom,
            'equip' => $this->equip,
            'posicio' => $this->posicio,
            'dorsal' => $this->dorsal,
            'edat' => $this->edat,
        ];
    }
}
```

**Ús al controlador:**

```php
use App\Http\Resources\JugadoraResource;

public function show(Jugadora $jugadora)
{
    return new JugadoraResource($jugadora);
}
```

##### 5. Col·leccions i Paginació

**Generar un recurs per col·leccions:**
També es poden crear recursos per transformar col·leccions de dades, incloent-hi metadades i enllaços addicionals.

```bash
php artisan make:resource JugadoraCollection
```

**Personalitzar les col·leccions:**

```php
namespace App\Http\Resources;

use Illuminate\Http\Resources\Json\ResourceCollection;

class JugadoraCollection extends ResourceCollection
{
    public function toArray($request)
    {
        return [
            'data' => $this->collection,
            'meta' => [
                'total_jugadores' => $this->resource->total(),
                'per_page' => $this->resource->perPage(),
                'current_page' => $this->resource->currentPage(),
                'last_page' => $this->resource->lastPage(),
            ],
            'links' => [
                'self' => url('/api/jugadores'),
            ],
        ];
    }
}
```


### 📑 **Paginar resultats:**
Utilitza el mètode `paginate()` per retornar resultats paginats. Les respostes amb `paginate()` inclouen metadades com el nombre total de registres, la pàgina actual i els enllaços de navegació.

```php
use App\Http\Resources\JugadoraCollection;

public function index()
{
    return new JugadoraCollection(Jugadora::paginate(10));
}
```


### 📄 **Respostes JSON amb paginació:**
Quan utilitzes `paginate()`, Laravel afegeix metadades útils a la resposta JSON, com ara el total de registres, el nombre per pàgina, la pàgina actual, etc.

```json
{
    "data": [
        {
            "id": 1,
            "nom": "Aitana Bonmatí",
            "equip": "FC Barcelona",
            "posicio": "Migcampista",
            "dorsal": 14,
            "edat": 26
        },
        {
            "id": 2,
            "nom": "Alexia Putellas",
            "equip": "FC Barcelona",
            "posicio": "Migcampista",
            "dorsal": 11,
            "edat": 29
        }
    ],
    "meta": {
        "total_jugadores": 50,
        "per_page": 10,
        "current_page": 1,
        "last_page": 5
    },
    "links": {
        "self": "http://example.com/api/jugadores"
    }
}
```

## 🎛️ 6. Personalització dels Recursos

Els recursos també poden incloure dades de relacions o camps calculats, com ara informació agregada o camps derivats.

```php
class JugadoraResource extends JsonResource
{
    public function toArray($request)
    {
        return [
            'id' => $this->id,
            'nom' => $this->nom,
            'equip' => $this->equip,
            'posicio' => $this->posicio,
            'dorsal' => $this->dorsal,
            'edat' => $this->edat,
            'partits_jugats' => $this->partits->count(), // Exemple de relació
            'mitjana_gols' => $this->partits->avg('gols'), // Camps derivats
        ];
    }
}
```


##### Resum

1. **`response()->json()`**: Útil per a respostes senzilles.
2. **Camps ocults o visibles**: Control directe al model.
3. **API Resources**: Separen la lògica de transformació i ofereixen flexibilitat.
4. **Paginació**: Facilita la navegació de dades grans amb `paginate()`.

Laravel 12 fa que el maneig de respostes JSON siga flexible, escalable i fàcil d'implementar.

### 🔄 Resta dels serveis


Vegem ara com implementar la resta de serveis (POST, PUT i DELETE). En el cas de la inserció (POST), haurem de rebre en la petició les dades de l'objecte a inserir (una jugadora, en el nostre exemple). Igual que les dades del servidor al client s'envien en format JSON, és d'esperar en aplicacions que segueixen l'arquitectura REST que les dades del client al servidor també s'envien en format JSON.

Abans de res, crea un **Form Request** per validar (evitem validar directament al controlador):

```bash
php artisan make:request JugadoraRequest
```

Defineix-hi les regles pertinents (`rules()`), i utilitza'l als mètodes.

```php
use App\Http\Requests\JugadoraRequest;

public function store(JugadoraRequest $request)
{
    $jugadora = Jugadora::create($request->validated());
    return response()->json($jugadora, 201); // Recurs creat
}

public function update(JugadoraRequest $request, Jugadora $jugadora)
{
    $jugadora->update($request->validated());
    return response()->json($jugadora, 200); // Actualització correcta
}
```

Finalment, pel servei DELETE, hem d'implementar el mètode **destroy** , que podria quedar així:

```php
public function destroy(Jugadora $jugadora)
{
    $jugadora->delete();
    return response()->noContent(); // 204 sense cos
}
```

Com podem començar a intuir, provar aquests serveis no és tan senzill com provar serveis de tipus GET, ja que no podem simplement teclejar una URL en el navegador. Necessitem un mecanisme per a passar-li les dades al servidor en format JSON, i també el mètode (POST, PUT o DELETE).

##### Validació de dades

A l'hora de rebre dades en format JSON per a serveis REST, també podem establir mecanismes de validació similars als vistos per als formularis, a través dels corresponents **requests**, com ja hem fet en els exemples anteriors.

##### Respostes d'error


D'altra banda, hem d'assegurar-nos que qualsevol error que es produïsca en la part del API retorne un contingut en format JSON, i no una pàgina web. Per exemple, si sol·licitem veure la fitxa d'una jugadora que el seu id no existeix, no hauria de retornar-nos una pàgina d'error 404, sinó un codi d'estat 404 amb un missatge d'error en format JSON.
Això no es compleix per defecte, ja que Laravel està configurat per a renderitzar una vista amb l'error produït.  Ho podem fer modificant el fitxer bootstrap/app.php.

```php
->withExceptions(function (Exceptions $exceptions) {
        // Laravel 12: força JSON a les rutes api/*
        $exceptions->shouldRenderJsonWhen(fn (Request $request) => $request->is('api/*'));

        $exceptions->render(function (\Illuminate\Validation\ValidationException $e, Request $request) {
            return response()->json([
                'message' => 'Dades no vàlides.',
                'errors' => $e->errors(),
            ], 422);
        });

        $exceptions->render(function (\Illuminate\Auth\AuthenticationException $e, Request $request) {
            return response()->json(['message' => 'No autenticat.'], 401);
        });

        $exceptions->render(function (\Illuminate\Database\Eloquent\ModelNotFoundException|\Symfony\Component\HttpKernel\Exception\NotFoundHttpException $e, Request $request) {
            return response()->json(['message' => 'Recurs o ruta no trobada.'], 404);
        });

        $exceptions->render(function (\Throwable $e, Request $request) {
            return response()->json(['message' => 'Error del servidor.'], 500);
        });
});
```
#### Provant els serveis amb POSTMAN

Ja hem vist que provar uns serveis de llistat (GET) és senzill a través d'un navegador. Però els serveis d'inserció (POST), modificació (PUT) o esborrat (DELETE) exigeixen d'altres eines per a poder ser provats. Podríem definir formularis amb aquests mètodes encapsulats, però l'esforç de definir
aqueixos formularis per a després no utilitzar-los més no mereix molt la pena. Veurem a continuació una eina molt útil per a provar tot tipus de serveis sense necessitat d'implementar gens addicional.

**Postman** és una aplicació gratuïta i multiplataforma que permet enviar tot tipus de peticions a un servidor determinat, i examinar la resposta que aquest produeix. D'aquesta forma, podem comprovar que els serveis ofereixen la informació adequada abans de ser usats per una aplicació client real.

La primera vegada que l'executem ens preguntarà si volem registrar-nos, de manera que puguem compartir els projectes que fem entre els diferents equips en què estiguem registrats, però podem saltar aquest pas fent clic en l'enllaç inferior.

Després d'iniciar l'aplicació, veurem la pantalla d'inici de Postman. Al principi apareixeran diverses opcions en la zona central, per a crear col·leccions o peticions, encara que també les podem crear des del
botó **New** a la cantonada superior esquerra. Per exemple, podem crear una col·lecció "Jugadores", i apareixerà en el panell esquerre:

Des del mateix botó*New a la cantonada superior esquerra podem crear noves peticions i associar-les a una col·lecció. Existeix una forma alternativa (potser més còmoda) de crear aqueixes peticions, a través del panell
de pestanyes, afegint noves:

##### Afegir peticions GET


Per a afegir una petició, habitualment triarem el tipus de comando sota les pestanyes (GET, POST, PUT, DELETE) i la URL associada a aquest comando. Per exemple:

![](imagenes/08/postman_1.png)

Llavors, podem fer clic en el botó "Save" en la part dreta, i guardar la petició per a poder-la reutilitzar. En guardar-la, ens demanarà que li assignem un nom (per exemple, "GET jugadores" en aquest cas), i la
col·lecció en la qual s'emmagatzemarà (la nostra col·lecció de "Jugadores").

![](imagenes/08/postman_2.png)

Després, podrem veure la prova associada a la col·lecció, en el panell esquerre, i si seleccionem aquesta prova i premem en el botó blau de "*Send" (part dreta), podem veure la resposta emesa pel servidor en el panell inferior de resposta (si tenim, és clar, el servidor en marxa)

![](imagenes/08/postman_3.png)

Seguint aquests mateixos passos, podem també crear una nova petició per a obtindre una jugadora a partir del seu id, per GET:

![](imagenes/08/postman_4.png)

Bastaria amb reemplaçar l'id de la URL pel qual vulguem consultar realment. Si provem aquesta petició, obtindrem la resposta corresponent:

![](imagenes/08/postman_5.png)

##### Afegir altres tipus de peticions

Les peticions POST difereixen de les peticions GET en què s'envia certa informació en el cos de la petició. Aquesta informació normalment són les dades que es volen afegir en el servidor. Com podem fer això amb Postman?
En primer lloc, creem una nova petició, triem el comando POST i definim la URL (en el nostre cas, lliga.local/api/jugadores o una cosa similar, depenent de com tinguem en marxa el servidor).
Llavors, fem clic en la pestanya Body, sota la URL, i establim el tipus com **raw** perquè ens deixe escriure'l sense restriccions. També convé canviar la propietat **Text** perquè siga JSON, i que així el servidor reculla el tipus de dada adequada. S'afegirà automàticament una capçalera de petició (**Header**)
que especificarà que el tipus de contingut que s'enviarà són dades JSON. Després, en el quadre de text sota aquestes opcions, especifiquem l'objecte JSON que volem enviar per a inserir:

![](imagenes/08/postman_6.png)

Després d'això, n'hi ha prou amb guardar la petició com hem fet amb les anteriors, i llançar-la per a veure el resultat.

Quant a les peticions PUT, procedirem de manera similar a les peticions POST: hem de triar el comando (PUT en aquest cas), la URL, i completar el cos de la petició amb les dades que vulguem modificar de la jugadora. En aquest cas, a més, l'id de la jugadora l'enviarem també en la pròpia URL:

![](imagenes/08/postman_7.png)

Per a peticions DELETE, la mecànica és similar a la fitxa de l'element (operació GET), canviant el comando GET per DELETE, i sense necessitat d'establir res en el cos de la petició:

![](imagenes/08/postman_8.png)

### 🔒 Autenticació en serveis REST

 
En una API REST també pot ser necessari protegir certs serveis, de manera que només puguen accedir a ells els usuaris autenticats. No obstant això, en aquest cas no tenim disponible el mecanisme d'autenticació basat en sessions que vam veure en temes anteriors, ja que la parteix client que consula la API
REST no té per què estar basada en un navegador. Podríem accedir des d'una aplicació d'escriptori feta a Java, per exemple, o des d'una aplicació mòbil, i en aquests casos no podríem disposar de les sessions, pròpies de clients web o navegadors. En el seu lloc, emprarem un mecanisme d'autenticació basat en tokens.

#### Fonaments de l'autenticació basada en tokens

L'autenticació basada en tokens és un mecanisme de validació d'usuaris en aplicacions client/servidor que podríem dir que és més universal que l'autenticació basada en sessions, ja que permet autenticar usuaris provinents de diferents tipus de clients. El que es fa és el següent:

* L'usuari necessita enviar les seues credencials (login i password), de manera similar a com es fa en una aplicació web normal, encara que aquesta vegada les dades s'envien normalment en format JSON.
* El servidor valida aqueixes credencials i, si són correctes, genera una cadena de text anomenada **token**, d'una certa longitud, i que servirà per a identificar unívocament a l'usuari a partir d'aqueix moment. Dit token ha de ser enviat de tornada (també en format JSON) al client que es va validar.
* A partir d'aquest punt, el client ha d'adjuntar el token com a part de la informació en cada petició que realitza a una zona d'accés restringit, de manera que el servidor puga consultar el token i comprovar si correspon amb el d'algun usuari autoritzat. Aquest token normalment s'envia en una capçalera de la petició anomenada **Authorization**, com veurem després, i el servidor pot consultar el valor d'aquesta capçalera per a verificar l'accés del client.

  
#### Generant tokens

Sanctum us permet emetre tokens API / tokens d'accés personal que es poden utilitzar per autenticar les peticions API a la vostra aplicació. Quan es fan sol·licituds utilitzant tokens API, el token s'ha d'incloure a la capçalera d'autorització com a token Bearer.

Per començar a emetre tokens per als usuaris, el model d'usuari hauria d'utilitzar el trait Laravel\Sanctum\HasApiTokens:

```php
use Laravel\Sanctum\HasApiTokens;

class User extends Authenticatable
{
use HasApiTokens, HasFactory, Notifiable;
}
```

Per a emetre un token, podeu utilitzar el mètode createToken. El mètode createToken retorna una instància Laravel\Sanctum\NewAccessToken. Els tokens de l'API es generen utilitzant el hash SHA-256 abans de ser emmagatzemats a la vostra base de dades, però podeu accedir al valor de text net del token utilitzant la propietat PlainTextToken de la instància NewAccessToken.
Per a vincular la generació del token amb un procediment d'autenticació podem fer-ho definint un mètode login , per exemple, que validarà les credencials que li arriben (login i password). Si són correctes, cridarà al mètode **createToken** de Sanctum (incorporat a l'usuari a través del **trait HasApiTokens** ), associant-lo al login de l'usuari entrant, i li retornarà el token en
format text pla, com un objecte JSON. En cas que hi haja un error en l'autenticació, enviarà de tornada un missatge d'error, amb el codi 401 d'accés no autoritzat.


```console
php artisan make:controller Api/AuthController
```


```php
namespace App\Http\Controllers\Api;
 use App\Http\Controllers\Controller as Controller;
class BaseController extends Controller
{
    /**
     * success response method.
     *
     * @return \Illuminate\Http\JsonResponse
     */
    public function sendResponse($result, $message, $code = 200)
    {
        $response = [
            'success' => true,
            'data'    => $result,
            'message' => $message,
        ];
        return response()->json($response, $code);
    }
    /**
     * return error response.
     *
     * @return \Illuminate\Http\JsonResponse
     */
    public function sendError($error, $errorMessages = [], $code = 200)
    {
        $response = [
            'success' => false,
            'message' => $error,
        ];
        if(!empty($errorMessages)){
            $response['info'] = $errorMessages;
        }
        return response()->json($response, $code);
    }
}
```

```php
namespace App\Http\Controllers\Api;

use Illuminate\Http\Request;
use App\Http\Controllers\Api\BaseController as BaseController;
use Illuminate\Support\Facades\Auth;
use Illuminate\Support\Facades\Validator;
use Illuminate\Support\Facades\Hash;
use App\Models\User;

class AuthController extends BaseController
{
    public function login(Request $request)
    {
        $credentials = $request->validate([
            'email' => 'required|email',
            'password' => 'required',
        ]);

        if (!Auth::attempt($credentials)) {
            return $this->sendError('Unauthorised.', ['error' => 'Credencials incorrectes'], 401);
        }

        $authUser = $request->user();
        $result['token'] =  $authUser->createToken('MyAuthApp')->plainTextToken;
        $result['name'] =  $authUser->name;

        return $this->sendResponse($result, 'User signed in');
    }
    public function register(Request $request)
    {
        $validator = Validator::make($request->all(), [
            'name' => 'required',
            'email' => 'required|email',
            'password' => 'required',
            'confirm_password' => 'required|same:password',
        ]);

        if ($validator->fails()){
            return $this->sendError('Error validation', $validator->errors());
        }

        try {
            $input = $validator->validated();
            $input['password'] = Hash::make($input['password']);
            $user = User::create($input);
            $result['token'] =  $user->createToken('MyAuthApp')->plainTextToken;
            $result['name'] =  $user->name;

            return $this->sendResponse($result, 'User created successfully.');
        } catch (\Exception $e) {
            return $this->sendError('Registration Error' , $e->getMessage());
        }
    }
    public function logout(Request $request)
    {
 
        $user = request()->user(); //or Auth::user()
        $user->tokens()->where('id', $user->currentAccessToken()->id)->delete();
        $success['name'] =  $user->name;
         return $this->sendResponse($success, 'User successfully signed out.');
    }

}

```

Definim en l'arxiu **routes/api.php** una ruta que redirigisca a aquest mètode, per a quan l'usuari vulga autenticar-se (recorda afegir amb use la corresponent classe):

```php
Route::post('login', [AuthController::class, 'login'])->middleware('api');
Route::post('register', [AuthController::class, 'register'])->middleware('api');


Route::middleware(['auth:sanctum','api'])->group( function () {
    Route::post('logout', [AuthController::class, 'logout']);

});

 ```
(`routes/api.php` ja porta el middleware `api` per defecte; l'indiquem ací només a mode d'exemple. L'important és afegir `auth:sanctum` a les rutes protegides.)

##### Protecció de rutes


Per protegir rutes de manera que totes les sol·licituds entrants s'hagin d'autenticar, hauríeu d'adjuntar el guard d'autenticació sanctum a les rutes protegides dins dels vostres fitxers de rutes/api.php. Aquest guard assegurarà que les peticions entrants s'autentiquen com a peticions d'estat, galetes autenticades o continguin una capçalera vàlida de testimoni API si la petició és d'un tercer.


 ```php
  
Route::get('/user',[userController::class,'show'])->middleware('auth:sanctum');
```

##### Revocant tokens

Podeu "revocar" tokens suprimint-los de la base de dades utilitzant la relació tokens que proporciona el tret Laravel\Sanctum\HasApiTokens:

```php
// Revoke all tokens...
$user->tokens()->delete();

// Revoke the token that was used to authenticate the current request...
$request->user()->currentAccessToken()->delete();

// Revoke a specific token...
$user->tokens()->where('id', $tokenId)->delete();
```

##### Caducitat del tokens
Per defecte, els tokens de Sanctum no caduquen i només poden ser invalidats revocant el token. No obstant això, si voleu configurar un temps de venciment per als toekns API de la vostra aplicació, podeu fer-ho mitjançant l'opció de configuració de venciment definida al fitxer de configuració de sanctum de la vostra aplicació. Aquesta opció de configuració defineix el nombre de minuts fins que un token emès es consideri expirat:

```
'expiració' =, 525600,
```

Si heu configurat un temps de venciment del token per a la vostra aplicació, també podeu programar una tasca per a eliminar els tokens caducats de la vostra aplicació. Afortunadament, Sanctum inclou un ordre sanctum:prune-expired Artisan que podeu utilitzar per aconseguir això. Per exemple, podeu configurar les tasques programades per a suprimir tots els registres de la base de dades de tokens caducats que hagin expirat almenys 24 hores:

```console
$schedule->command('sanctum:prune-expired --hours=24')->daily();
```

##### Prova d'autenticació amb POSTMAN

Vegem com provar l'autenticació per token en el projecte de lliga femenina, per qualsevol dels mètodes vistos abans.
En primer lloc, i després de posar en marxa el projecte, ens assegurarem que podem accedir sense restriccions als dos serveis que no requereixen autorització ( index o show ), igual que abans.


Si accedim a un recurs protegit obtenim 

```json
{ "error": "Credenciales no válidas"}
```

Ara anem a loguejar-se


![](imagenes/08/postman_9.png)

Ara hem de copiar aquest token, i pegar-ho en la petició d'accés restringit. Haurem de pegar-ho en la capçalera Authorization (obrir aqueixa pestanya sota la URL de la petició en Postman), i el normal és enviar-ho com un **Bearer token**, segons els estàndards. Llavors sí que tindrem la resposta correcta de l'operació
sol·licitada.

![](imagenes/08/postman_10.png)

A l'hora de traslladar aquestes proves a una aplicació "real", enviaríem les credencials per JSON al servidor, obtindríem el token de tornada i l'emmagatzemaríem localment en alguna variable o suport
(per exemple, en l'element localStorage , si treballem amb algun framework Javascript). Després, davant cada petició JSON que férem al servidor, adjuntaríem aquest token en la capçalera Authorization perquè fóra validat pel servidor.



## 📎 Annex I : API per a la Guia d'Equips de Futbol Femení.

 
### ⚙️ Pas 1: Configuració inicial de l’API (instal·lació Sanctum)

- Instal·la Laravel Sanctum al projecte:
  
  ```bash
  composer require laravel/sanctum
  php artisan vendor:publish --provider="Laravel\Sanctum\SanctumServiceProvider"
  php artisan migrate
  ```
  
- Configura el fitxer bootstrap/app.php per tal que els missatges d'errada vinguen en format json:

```php
return Application::configure(basePath: dirname(__DIR__))
->withRouting(
    web: __DIR__.'/../routes/web.php',
    api: __DIR__.'/../routes/api.php',
    commands: __DIR__.'/../routes/console.php',
    health: '/up',
)
->withMiddleware(function (Middleware $middleware) {

})
->withExceptions(function (Exceptions $exceptions) {
    $exceptions->render(function (Exception $e, Request $request) {
        if ($request->is('api/*')) {
            $statusCode = method_exists($e, 'getStatusCode') ? $e->getStatusCode() : 500;
            return response()->json([
                'success' => false,
                'message' => $e->getMessage(),
            ], $statusCode);
        }
    });

    $exceptions->render(function (Throwable $e, Request $request) {
        if ($request->is('api/*')) {
            return response()->json([
                'success' => false,
                'message' => $e->getMessage(),
            ], 500);
        }
    });
})->create();
```

### 🛣️ Pas 2: Controladors i Rutes 
 
- Genera controladors per als models utilitzant Artisan:
  
  ```bash
   php artisan make:controller Api/JugadoraController --api --model=Jugadora
  ```
-   Crea les rutes CRUD per als models:

```php
Route::apiResource('jugadores', Api\JugadoraController::class)
    ->parameters(['jugadores' => 'jugadora'])
    ->middleware('api');
 ```
- Crea un controller BaseController per a gestionar les respostes de l'API:

```php

namespace App\Http\Controllers\Api;
 use App\Http\Controllers\Controller as Controller;
class BaseController extends Controller
{
    /**
     * success response method.
     *
     * @return \Illuminate\Http\JsonResponse
     */
    public function sendResponse($result, $message, $code = 200)
    {
        $response = [
            'success' => true,
            'data'    => $result,
            'message' => $message,
        ];
        return response()->json($response, $code);
    }
    /**
     * return error response.
     *
     * @return \Illuminate\Http\JsonResponse
     */
    public function sendError($error, $errorMessages = [], $code = 200)
    {
        $response = [
            'success' => false,
            'message' => $error,
        ];
        if(!empty($errorMessages)){
            $response['info'] = $errorMessages;
        }
        return response()->json($response, $code);
    }
}
```


- Completa els mètodes CRUD en el controlador utilitzant els models i Form Requests per validar les dades:

```php
namespace App\Http\Controllers\Api;

 
use App\Http\Requests\JugadoraRequest;
use App\Models\Jugadora;
 

class JugadoraController extends BaseController
{
    /**
     * Display a listing of the resource.
     */
    public function index()
    {
        return Jugadora::paginate(10);
    }

    public function store(JugadoraRequest $request)
    {
        $jugadora = Jugadora::create($request->validated());
        return $this->sendResponse($jugadora, 'Jugadora Creada amb exit', 201);
    }

    public function show(Jugadora $jugadora)
    {
        return $this->sendResponse($jugadora, 'Jugadora Recuperada amb exit', 200);
    }

    public function update(JugadoraRequest $request, Jugadora $jugadora)
    {
        $jugadora->update($request->validated());
        return $this->sendResponse($jugadora, 'Jugadora Actualitzada amb èxit', 200);
    }

    public function destroy(Jugadora $jugadora)
    {
        $jugadora->delete();
        return $this->sendResponse(null, 'Jugadora Eliminada amb exit', 200);
    }
}

``` 
### 📦 Pas 3: Resources

- Genera un Recurso per a la Jugadora:

```bash
php artisan make:resource JugadoraResource
```

- Implementa el Recurs JugadoraResource:

```php
namespace App\Http\Resources;

use Illuminate\Http\Request;
use Illuminate\Http\Resources\Json\JsonResource;

class JugadoraResource extends JsonResource
{
    /**
     * Transform the resource into an array.
     *
     * @return array<string, mixed>
     */
    public function toArray(Request $request): array
    {
        return [
            'id' => $this->id,
            'nom' => $this->nom,
            'equip' => $this->Equip->nom,
            'posicio' => $this->posicio,
            'dorsal' => $this->dorsal,
            'edat' => $this->edat
        ];
    }
}
```

- Modifica el controlador JugadoraController per a utilitzar el Recurs JugadoraResource:

```php

    public function index()
    {
        return JugadoraResource::collection(Jugadora::paginate());
    }
    
    public function show(Jugadora $jugadora)
    {
        return $this->sendResponse(new JugadoraResource($jugadora), 'Jugadora Recuperada amb èxit', 200);
    }
    
    public function update(JugadoraRequest $request, Jugadora $jugadora)
    {
        $jugadora->update($request->validated());
        return $this->sendResponse($jugadora, 'Jugadora Actualitzada amb èxit', 200);
    }
    
    public function store(JugadoraRequest $request)
    {
        $jugadora = Jugadora::create($request->validated());
        return $this->sendResponse(new JugadoraResource($jugadora), 'Jugadora Creada amb èxit', 201);
    }
    
    public function destroy(Jugadora $jugadora)
    {
        $jugadora->delete();
        return $this->sendResponse(null, 'Jugadora Eliminada amb èxit', 200);
    }
```
    



### 🔐 Pas 4: Autenticació i autorització

- Afegir al model User el trait HasApiTokens:

```php
use Laravel\Sanctum\HasApiTokens;
class User extends Authenticatable
{
    use HasApiTokens, HasFactory, Notifiable;
}
``` 

- Afegir les rutes d'autenticació a **routes/api.php**:

```php

Route::post('login', [AuthController::class, 'login'])->middleware('api');
Route::post('register', [AuthController::class, 'register'])->middleware('api');
 

Route::middleware(['auth:sanctum','api'])->group( function () {
    Route::apiResource('jugadores',  JugadoraController::class)
        ->parameters(['jugadores' => 'jugadora']);
    Route::post('logout', [AuthController::class, 'logout']);

});
```

- Implementar el controlador AuthController amb els mètodes login, register i logout:
 
```php
namespace App\Http\Controllers\Api;

use Illuminate\Http\Request;
use App\Http\Controllers\Api\BaseController as BaseController;
use Illuminate\Support\Facades\Auth;
use Illuminate\Support\Facades\Validator;
use Illuminate\Support\Facades\Hash;
use App\Models\User;

class AuthController extends BaseController
{
    public function login(Request $request)
    {
        $credentials = $request->validate([
            'email' => 'required|email',
            'password' => 'required',
        ]);

        if (!Auth::attempt($credentials)) {
            return $this->sendError('Unauthorised.', ['error'=>'incorrect Email/Password'], 401);
        }

        $authUser = $request->user();
        $result['token'] =  $authUser->createToken('MyAuthApp')->plainTextToken;
        $result['name'] =  $authUser->name;

        return $this->sendResponse($result, 'User signed in');
    }
    public function register(Request $request)
    {
        $validator = Validator::make($request->all(), [
            'name' => 'required',
            'email' => 'required|email',
            'password' => 'required',
            'confirm_password' => 'required|same:password',
        ]);

        if ($validator->fails()){
            return $this->sendError('Error validation', $validator->errors());
        }

        try {
            $input = $validator->validated();
            $input['password'] = Hash::make($input['password']);
            $user = User::create($input);
            $result['token'] =  $user->createToken('MyAuthApp')->plainTextToken;
            $result['name'] =  $user->name;

            return $this->sendResponse($result, 'User created successfully.');
        } catch (\Exception $e) {
            return $this->sendError('Registration Error' , $e->getMessage());
        }
    }
    public function logout(Request $request)
    {
 
        $user = request()->user(); //or Auth::user()
        $user->tokens()->where('id', $user->currentAccessToken()->id)->delete();
        $success['name'] =  $user->name;
         return $this->sendResponse($success, 'User successfully signed out.');
    }

}

```

## 🧪 Exercici     

# Enunciat: Creació d'una API i la seva documentació

Aquest exercici consisteix a crear una API per gestionar les taules que no són `jugadores` i documentar-la correctament utilitzant Swagger (`l5-swagger`). Segueix els passos indicats per implementar i documentar les operacions CRUD i altres funcionalitats específiques.

  
### 🏟️ 1. **Entitats a gestionar**
- **Estadis**
- **Equips**
- **Partits**

### 🛤️ 2. **Endpoints**
Implementa els següents endpoints per a cada entitat, seguint els estàndards REST:

- `GET /api/{resource}`: Retorna una llista paginada de recursos.
- `POST /api/{resource}`: Crea un nou recurs.
- `GET /api/{resource}/{id}`: Retorna un recurs específic.
- `PUT /api/{resource}/{id}`: Actualitza un recurs específic.
- `DELETE /api/{resource}/{id}`: Elimina un recurs específic.


 
