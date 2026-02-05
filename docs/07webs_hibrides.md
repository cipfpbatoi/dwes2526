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

# Webs híbrides

> Duració estimada: 8 sessions

## Característiques de les webs híbrides

Les aplicacions web híbrides, també conegudes com a "mashups", són una combinació de dades i/o funcionalitats provinents de diverses fonts per a crear un nou tipus d'aplicació o servei.
Les seues característiques principals són:

* **Integració de Dades de Diversos Orígens**: Les aplicacions web híbrides aprofiten dades i funcionalitats de múltiples fonts, com ara serveis web, APIs, i altres recursos en línia. Això permet combinar i reutilitzar recursos existents de manera creativa per a desenvolupar aplicacions més complexes i funcionals.
* **Ús de Serveis Web i APIs**: Moltes d'aquestes aplicacions utilitzen dades accessibles a través de serveis web. En este tema prioritzarem APIs gratuïtes o d'accés obert (open data), amb respostes en JSON o XML, per a poder integrar-les sense costos per a l'alumnat.
* **Sindicació Web (RSS/Atom)**: Algunes aplicacions web híbrides fan ús de protocols de sindicació web, com RSS o Atom, per accedir a continguts actualitzats de manera regular. Aquests protocols simplifiquen el procés de compartir i distribuir continguts web.
* **Dades Internes**: A més de les fonts externes, les aplicacions web híbrides poden incloure dades internes generades i gestionades per l'entitat propietària de l'aplicació, com podrien ser les dades corporatives o de negoci.
* **Web Scraping**: Encara que és menys comú, algunes aplicacions utilitzen tècniques d'enginyeria inversa, com el web scraping, per extreure dades des de llocs web. Això pot ser útil per obtenir informació com els preus dels productes en les botigues en línia.

Aquesta actualització reflecteix l'evolució constant en el camp del desenvolupament web i la integració de tecnologies, destacant la importància de les fonts diverses de dades i la capacitat de combinar-les de forma innovadora en el disseny d'aplicacions web híbrides​​.

## Utilització de repositoris d'informació

Per a poder reutilitzar codi i informació cal que tingem en conte les següents consideracions:

* **Integració de Serveis Web de Tercers**: En el desenvolupament d'aplicacions web híbrides, és comú utilitzar serveis proporcionats per tercers. Aquests serveis poden oferir funcionalitats específiques que enriquiran l'aplicació sense necessitat de desenvolupar-les des de zero. Un exemple podria ser l'ús d'OpenStreetMap per mostrar la ubicació geogràfica de les franquícies d'una empresa en un mapa.
* **Desenvolupament d'Aplicacions Pràctiques**: En aquest context, es posa l'accent en el desenvolupament d'aplicacions que faciliten processos específics, com podria ser la gestió d'enviaments en una botiga en línia. Aquest tipus d'aplicació pot millorar significativament l'experiència dels usuaris i l'eficiència de les operacions de l'empresa.
* **Reconeixement de Necessitats i Oportunitats**: És important identificar funcionalitats que poden ser útils per als usuaris, fins i tot quan aquests no les han sol·licitat explícitament. Aquesta anticipació de necessitats pot ser un factor clau en el desenvolupament d'aplicacions web híbrides exitoses.
* **Condicions i Límits en l'Ús de Serveis de Tercers**: Quan s'utilitzen serveis de tercers, cal tenir en compte les condicions i límits que aquests imposen. Això inclou restriccions d'ús, límits de sol·licituds, entre d'altres aspectes legals i tècnics.
* **Adquisició d'Experiència en Desenvolupament Web**: El desenvolupament d'aquestes aplicacions també serveix com una oportunitat per adquirir experiència pràctica en l'àmbit del desenvolupament web, millorant així les habilitats tècniques dels desenvolupadors.

Per exemple podriem desenvolupar:

* **Mapa amb OpenStreetMap**: Imaginem que estàs desenvolupant una aplicació web per a una cadena de restaurants. Pots mostrar la ubicació de tots els restaurants en un mapa interactiu amb OpenStreetMap i Leaflet (sense necessitat de clau de pagament). Els usuaris poden buscar el restaurant més proper i veure informació bàsica.
* **Gestió d'Enviaments amb APIs de Logística**: Per una botiga en línia, pots integrar APIs de serveis de missatgeria com UPS, FedEx o DHL. Això permet als usuaris fer seguiment dels seus enviaments en temps real, calcular costos d'enviament, i gestionar devolucions de manera eficient.
* **Integració de Passarel·les de Pagament**: En una aplicació d'e-commerce, l'ús de passarel·les de pagament com Stripe, PayPal, o Square és essencial. Això no només ofereix una solució de pagament segura als usuaris, sinó que també simplifica la gestió financera de la botiga.
* **Ús de APIs de Xarxes Socials**: Podries integrar APIs de xarxes socials com Facebook, Twitter, o Instagram per permetre als usuaris compartir productes o experiències directament des de la teva aplicació. Això pot augmentar la visibilitat i l'engagement del teu negoci.
* **Serveis Meteorològics Integrats**: Per a una aplicació d'activitats a l'aire lliure, com una app de senderisme, integrar dades meteorològiques en temps real amb APIs gratuïtes com Open-Meteo pot ser molt útil. Els usuaris podrien planificar les seves activitats basant-se en les condicions meteorològiques actuals i les previsions.
* **Recollida d'Opinions amb Dades Obertes**: En una aplicació per a hotels o restaurants, pots partir de dades obertes (open data municipal o autonòmic) o construir el teu propi sistema de ressenyes dins l'aplicació.

En este tema evitarem APIs de pagament. Els exemples de passarel·les de pagament o logística són referències conceptuals, però les pràctiques es faran amb dades obertes i serveis gratuïts.

## Autenticació amb Google

### Configuració de l'Autenticació amb Google en Laravel

#### **1. Instal·lar Laravel Socialite**

Laravel **Socialite** és la biblioteca oficial per gestionar l'autenticació amb proveïdors socials.

#### **1. Instal·la Socialite** 
   ```bash
   composer require laravel/socialite
   php artisan vendor:publish --provider="Laravel\Socialite\SocialiteServiceProvider"
   ```
 
#### **2. Configura Google API**
1. Accedeix a la [Consola de Desenvolupadors de Google](https://console.developers.google.com/).
2. Crea un nou projecte o selecciona un projecte existent.
3. Activa "Google Identity Services" (o l'API de People si cal).
4. Crea una credencial d'OAuth 2.0 i configura:
    - **Tipus d'aplicació**: Aplicació web.
    - **URI de redirecció autoritzat**:
      ```
      http://localhost/auth/google/callback
      ```

5. Copia el **Client ID** i el **Client Secret**.

 
#### **3. Configura les Variables d'Entorn**
Afegeix les credencials al fitxer `.env`:

```dotenv
GOOGLE_CLIENT_ID=your-client-id
GOOGLE_CLIENT_SECRET=your-client-secret
GOOGLE_REDIRECT=http://localhost/auth/google/callback
```
  
Afegeix la configuració de Google al fitxer `config/services.php`:

```php
'google' => [
    'client_id' => env('GOOGLE_CLIENT_ID'),
    'client_secret' => env('GOOGLE_CLIENT_SECRET'),
    'redirect' => env('GOOGLE_REDIRECT'),
],
```
 
#### **4. Configura les Rutes**
Defineix les rutes necessàries al fitxer `routes/web.php`:

```php
use App\Http\Controllers\AuthController;

Route::get('/auth/google/redirect', [AuthController::class, 'redirectToGoogle'])->name('google.redirect');
Route::get('/auth/google/callback', [AuthController::class, 'handleGoogleCallback'])->name('google.callback');
```
 
#### **5. Crea el Controlador**
Crea un controlador per gestionar l'autenticació amb Google amb els seguents mètodes:

```php
namespace App\Http\Controllers;

use Laravel\Socialite\Facades\Socialite;
use Illuminate\Support\Facades\Auth;
use App\Models\User;

class AuthController extends Controller
{
    public function redirectToGoogle()
    {
        return Socialite::driver('google')->redirect();
    }

    public function handleGoogleCallback()
    {
        $googleUser = Socialite::driver('google')->stateless()->user();

        // Cerca l'usuari o crea'l si no existeix
        $user = User::firstOrCreate(
            ['email' => $googleUser->getEmail()],
            [
                'name' => $googleUser->getName(),
                'google_id' => $googleUser->getId(),
                'avatar' => $googleUser->getAvatar(),
                'password' => bcrypt(str()->random(24)), // Contrassenya aleatòria
            ]
        );

        // Inicia sessió amb l'usuari
        Auth::login($user);

        return redirect('/home'); // Redirigeix a la pàgina principal
    }
}
```
 
#### **6. Modifica el Model `User` per afegir els camps nou i modifica la migració**
 
#### **7. Prova l'Autenticació**
- Accedeix a l'URL: `http://localhost/auth/google/redirect`
- Segueix el procés d'autenticació amb Google.

  

##  Difusió d'Esdeveniments en Temps Real amb WebSockets
 
Els **WebSockets** permeten implementar interfícies d'usuari que s'actualitzen en temps real de manera eficient. A diferència del *polling* constant, els WebSockets envien dades del servidor al client només quan hi ha canvis, millorant el rendiment i l'experiència d'usuari.
 
### Funcionament
- **Canals**: Els clients es connecten a canals amb noms específics al frontend.
- **Esdeveniments**: L'aplicació Laravel envia esdeveniments a aquests canals des del backend. Els esdeveniments poden incloure dades que el frontend utilitza per actualitzar la interfície.

### Drivers de Difusió Suportats
Laravel proporciona diverses opcions per gestionar WebSockets. En este tema prioritzarem opcions gratuïtes i autogestionades:

1. **Laravel Reverb**: Solució autogestionada i integrada amb Laravel (recomanada per a no dependre de serveis de pagament).
2. **Pusher Channels**: Servei gestionat per a WebSockets (no gratuït en la majoria de casos).
3. **Ably**: Plataforma avançada per a comunicacions en temps real (amb límits gratuïts, però de pagament en producció).

 
### Implementació Bàsica en el servidor

Laravel facilita la difusió d'esdeveniments (*event broadcasting*) gràcies a un driver de difusió que envia els esdeveniments al client mitjançant Laravel Echo (una biblioteca JavaScript).

#### Configuració
 
```bash
  php artisan install:broadcasting
```
Em preguntarà si vull instal·lar Reverb (sí) i la part de client (sí). Aquesta ordre ja instal·la Reverb i Laravel Echo, així que no cal repetir la instal·lació després.         

Aquesta ordre:

- Crearà el fitxer `config/broadcasting.php`.
- Crearà el fitxer `routes/channels.php`, on pots registrar rutes d'autorització i callbacks per als canals de difusió.

#### Proveïdor de serveis (Broadcasting)

Assegura't que el **BroadcastServiceProvider** està creat i registrat. És el que activa les rutes de difusió i carrega `routes/channels.php`.

```php
// app/Providers/BroadcastServiceProvider.php
public function boot(): void
{
    Broadcast::routes();
    require base_path('routes/channels.php');
}
```

Registre del provider:

 
- **Laravel 11** (`bootstrap/app.php`):
  ```php
  ->withProviders([
      App\Providers\BroadcastServiceProvider::class,
  ])
  ```

 
#### Configuració Bàsica amb Laravel Reverb (gratuït i autogestionat)

Reverb permet fer WebSockets sense dependre de serveis externs:

1. Configura les variables al `.env`:

```env
BROADCAST_DRIVER=reverb

REVERB_APP_ID=your-app-id
REVERB_APP_KEY=your-app-key
REVERB_APP_SECRET=your-app-secret
REVERB_HOST=localhost
REVERB_PORT=8080
REVERB_SCHEME=http

VITE_REVERB_APP_KEY=your-app-key
VITE_REVERB_HOST=localhost
VITE_REVERB_PORT=8080
VITE_REVERB_SCHEME=http
```

2. Configura el driver de difusió en `config/broadcasting.php`:

```php
'reverb' => [
    'driver' => 'reverb',
    'key' => env('REVERB_APP_KEY'),
    'secret' => env('REVERB_APP_SECRET'),
    'app_id' => env('REVERB_APP_ID'),
    'host' => env('REVERB_HOST'),
    'port' => env('REVERB_PORT'),
    'scheme' => env('REVERB_SCHEME'),
],
```
  
3. Configuració de Laravel Echo

(Si has fet `php artisan install:broadcasting`, ja està instal·lat.)

**On posar el JS?**  
En Laravel, el codi d’Echo va a `resources/js/bootstrap.js` (o `resources/js/app.js` si preferixes).  
Després assegura’t que Vite carrega el fitxer a `resources/views/layouts/app.blade.php`:

```php
@vite(['resources/css/app.css', 'resources/js/app.js'])
```

```js
// resources/js/app.js (o bootstrap.js)
import Echo from 'laravel-echo';
import Pusher from 'pusher-js';
window.Pusher = Pusher;

window.Echo = new Echo({
    broadcaster: 'reverb',
    key: import.meta.env.VITE_REVERB_APP_KEY,
    wsHost: import.meta.env.VITE_REVERB_HOST,
    wsPort: import.meta.env.VITE_REVERB_PORT,
    wssPort: import.meta.env.VITE_REVERB_PORT,
    forceTLS: import.meta.env.VITE_REVERB_SCHEME === 'https',
    enabledTransports: ['ws', 'wss'],
});
```
  
al front-end, afegeix el següent codi per connectar amb el servidor de WebSockets:

 
```js
Echo.channel('channel-name')
.listen('EventName', (e) => {
    console.log(e);

});
```
5. **Creació de Canals**

Defineix canals en routes/channels.php. Per exemple, un canal privat:

```php
Broadcast::channel('channel-name', function ($user) {
    return true; // Autorització
});
```
 
6. **Disparar Esdeveniments en Temps Real**

Crea esdeveniments que implementen ShouldBroadcast i defineix en quin canal s'han d'emetre.

```php
class EventName implements ShouldBroadcast
{
    public function broadcastOn()
    {
        return new Channel('channel-name');
    }
}
```
7. **Configuració de la Cua**

- Tots els esdeveniments de difusió s'envien a través de treballs en cua (queued jobs).
- És necessari configurar i executar un treballador de cua per evitar que la resposta de l'aplicació es veja afectada durant la difusió dels esdeveniments:

```bash
  php artisan queue:work
```

#### Proveïdor extern (exemple: Pusher Channels)

Si prefereixes un proveïdor gestionat (sense Reverb), pots usar **Pusher**.

1. Crea una app a Pusher Channels (dashboard) i copia `app_id`, `key`, `secret`, `cluster`.
2. `.env`:

```env
BROADCAST_DRIVER=pusher

PUSHER_APP_ID=your-app-id
PUSHER_APP_KEY=your-app-key
PUSHER_APP_SECRET=your-app-secret
PUSHER_APP_CLUSTER=eu

VITE_PUSHER_APP_KEY=your-app-key
VITE_PUSHER_APP_CLUSTER=eu
```

3. `config/broadcasting.php`:

```php
'pusher' => [
    'driver' => 'pusher',
    'key' => env('PUSHER_APP_KEY'),
    'secret' => env('PUSHER_APP_SECRET'),
    'app_id' => env('PUSHER_APP_ID'),
    'options' => [
        'cluster' => env('PUSHER_APP_CLUSTER'),
        'useTLS' => true,
    ],
],
```

4. JS (mateix fitxer que abans, però canviant el provider):

```js
window.Echo = new Echo({
    broadcaster: 'pusher',
    key: import.meta.env.VITE_PUSHER_APP_KEY,
    cluster: import.meta.env.VITE_PUSHER_APP_CLUSTER,
    forceTLS: true,
});
```

5. **Crear un canal**:
   - En Pusher **no “crees” canals al dashboard**. Els canals s’obrin automàticament quan el client es connecta a `channel-name`.  
   - En Laravel, defineix el canal a `routes/channels.php` (autorització).
 
## Integració amb IA (Gemini i/o ChatGPT)

Ara substituïm l'opció local per serveis externs. **Gemini** (Google) i **ChatGPT via API d'OpenAI** són de pagament, però solen tindre trams gratuïts o crèdits inicials. 

### Configura l'entorn

```dotenv
OPENAI_API_KEY=your-openai-key
OPENAI_MODEL=gpt-5.2

GEMINI_API_KEY=your-gemini-key
GEMINI_MODEL=gemini-2.5-flash
```

En `config/services.php` afegeix:

```php
'openai' => [
    'api_key' => env('OPENAI_API_KEY'),
    'model' => env('OPENAI_MODEL', 'gpt-5.2'),
],
'gemini' => [
    'api_key' => env('GEMINI_API_KEY'),
    'model' => env('GEMINI_MODEL', 'gemini-2.5-flash'),
],
```

> **Nota**: Canvia el model pel que tingues disponible al teu compte.

### Service per a ChatGPT (OpenAI)

```php
namespace App\Services;

use GuzzleHttp\Client;
use Illuminate\Support\Facades\Log;

class OpenAIService
{
    public static function getResponse(string $question): string|array
    {
        try {
            $client = new Client([
                'base_uri' => 'https://api.openai.com/',
                'headers' => [
                    'Content-Type' => 'application/json',
                    'Authorization' => 'Bearer ' . config('services.openai.api_key'),
                ],
            ]);

            $response = $client->post('v1/chat/completions', [
                'json' => [
                    'model' => config('services.openai.model'),
                    'messages' => [
                        ['role' => 'user', 'content' => $question],
                    ],
                ],
            ]);

            $body = json_decode($response->getBody()->getContents(), true);
            return $body['choices'][0]['message']['content'] ?? '';
        } catch (\Exception $e) {
            Log::error('Error en la resposta d\'OpenAI: ' . $e->getMessage());
            return ['error' => 'No s\'ha pogut obtenir una resposta.'];
        }
    }
}
```

### Service per a Gemini (Google)

```php
namespace App\Services;

use GuzzleHttp\Client;
use Illuminate\Support\Facades\Log;

class GeminiService
{
    public static function getResponse(string $question): string|array
    {
        try {
            $client = new Client([
                'base_uri' => 'https://generativelanguage.googleapis.com/',
                'headers' => [
                    'Content-Type' => 'application/json',
                ],
            ]);

            $model = config('services.gemini.model');
            $response = $client->post("v1beta/models/{$model}:generateContent", [
                'headers' => [
                    'x-goog-api-key' => config('services.gemini.api_key'),
                ],
                'json' => [
                    'contents' => [
                        [
                            'parts' => [
                                ['text' => $question],
                            ],
                        ],
                    ],
                ],
            ]);

            $body = json_decode($response->getBody()->getContents(), true);
            return $body['candidates'][0]['content']['parts'][0]['text'] ?? '';
        } catch (\Exception $e) {
            Log::error('Error en la resposta de Gemini: ' . $e->getMessage());
            return ['error' => 'No s\'ha pogut obtenir una resposta.'];
        }
    }
}
```

### Ús bàsic

```php
$descripcio = OpenAIService::getResponse('Dona una descripció del '.$equip->nom.' de Futbol Femení');
// o bé
$descripcio = GeminiService::getResponse('Dona una descripció del '.$equip->nom.' de Futbol Femení');
```

A partir d'ací pots adaptar prompts, controlar costos i afegir memòria o historial de conversa segons necessites.


## Gestió de pagaments

> **Nota**: Aquesta part és informativa. Les passarel·les de pagament són serveis de pagament i es treballaran només en mode sandbox. Per a pràctiques, usarem **PayPal Sandbox** i **Stripe test mode (targeta)**.

La primera decisió que hem de pendre es triar la passarel·la de Pagament: Hi ha moltes opcions com Stripe, PayPal, PayU, Braintree, Square, Authorize.Net...
Totes solen tindre entorn de proves(sanbox) on fer transaccions fictícies per a provar el funcionament de la passarel·la de pagament.

### PayPal

Per permetre que un usuari pague amb el seu compte PayPal Sandbox a un compte Business de Sandbox en una aplicació Laravel, hauràs de seguir una sèrie de passos. Aquests passos impliquen la configuració del teu entorn de Sandbox a PayPal i la integració amb la teva aplicació Laravel utilitzant el paquet paypal/rest-api-sdk-php o una altra biblioteca similar. Aquí tens una guia pas a pas:

* Configura els Comptes Sandbox: Assegura't que tens dos comptes en PayPal Sandbox: un compte personal (que simula el comprador) i un compte Business (que simula el venedor).

* Instal·la el Paquet de PayPal en Laravel: Utilitza Composer per instal·lar el paquet `paypal/rest-api-sdk-php` o una altra biblioteca de PayPal compatible amb Laravel.

* Configura les Credencials de Sandbox en Laravel: Obté les credencials del teu compte Business de Sandbox (ID de client i secret) i configura-les en el teu projecte Laravel, normalment a través del fitxer .env. i configura el `services.php
     
```php
'paypal' => [
'client_id' => env('PAYPAL_CLIENT_ID'),
'client_secret' => env('PAYPAL_CLIENT_SECRET'),
],
```  

* Crea un Context d'API de PayPal: Utilitza les credencials del teu compte Business de Sandbox per crear un objecte ApiContext. Aquest objecte s'utilitzarà per a realitzar crides a l'API de PayPal.

```php
use PayPal\Rest\ApiContext;
use PayPal\Auth\OAuthTokenCredential;

// ...

public function createPayment()
{
    $apiContext = new ApiContext(new OAuthTokenCredential(
            env('PAYPAL_CLIENT_ID'),     // ClientID
            env('PAYPAL_SECRET')         // ClientSecret
        )
    );

    // Configura el `ApiContext` segons les teves necessitats
    $apiContext->setConfig([
        'mode' => 'sandbox', // Mode Sandbox per a proves
        // Altres configuracions...
    ]);

    // Aquí va la resta de la teva lògica de pagament...
}
```

* Implementa la Lògica de Pagament:

        * Desenvolupa la lògica en els teus controladors Laravel per crear sol·licituds de pagament. Això inclou la creació d'objectes de pagament amb detalls com l'import, la moneda, i la descripció.
        * Redirigeix l'Usuari a PayPal: Quan un usuari iniciï un pagament, redirigeix-lo a la pàgina de pagament de PayPal utilitzant l'URL proporcionada per la biblioteca. L'usuari iniciarà sessió amb el seu compte personal de Sandbox per completar el pagament.
        * Gestiona la Resposta de PayPal: Després que l'usuari completi el pagament, serà redirigit de tornada a la teva aplicació. Necessitaràs gestionar aquesta resposta per confirmar la transacció.
        * Prova el Procés de Pagament: Realitza proves utilitzant els teus comptes de Sandbox per assegurar-te que tot funciona com s'espera. Això inclou iniciar un pagament amb el compte personal de Sandbox i rebre el pagament en el compte Business de Sandbox.
        * Revisa i Depura: Comprova que les transaccions es mostren correctament en els panells de control de Sandbox tant del comprador com del venedor. Depura qualsevol problema que puguis trobar.

Exemple de creació d'un pagament amb el SDK de PayPal:

```php
use PayPal\Api\Amount;
use PayPal\Api\Payer;
use PayPal\Api\Payment;
use PayPal\Api\RedirectUrls;
use PayPal\Api\Transaction;
use PayPal\Rest\ApiContext;
use PayPal\Auth\OAuthTokenCredential;

class PaymentController extends Controller
{
    private $apiContext;

    public function __construct()
    {
        $this->apiContext = new ApiContext(
            new OAuthTokenCredential(
                env('PAYPAL_SANDBOX_CLIENT_ID'),     // ClientID
                env('PAYPAL_SANDBOX_SECRET')         // ClientSecret
            )
        );
    }

    public function createPayment()
    {
        $payer = new Payer();
        $payer->setPaymentMethod('paypal');

        $amount = new Amount();
        $amount->setTotal('10.00');  // Defineix l'import del pagament
        $amount->setCurrency('EUR'); // Defineix la moneda

        $transaction = new Transaction();
        $transaction->setAmount($amount);
        $transaction->setDescription('Descripció del pagament');

        $redirectUrls = new RedirectUrls();
        $redirectUrls->setReturnUrl(url('/payment/success')) // URL de retorn en cas d'èxit
                     ->setCancelUrl(url('/payment/cancel')); // URL de retorn en cas de cancel·lació

        $payment = new Payment();
        $payment->setIntent('sale')
                ->setPayer($payer)
                ->setTransactions([$transaction])
                ->setRedirectUrls($redirectUrls);

        try {
            $payment->create($this->apiContext);
            return redirect()->away($payment->getApprovalLink());
        } catch (Exception $e) {
            // Gestiona l'error aquí
            return back()->with('error', 'Hi ha hagut un problema en processar el pagament');
        }
    }
    
    public function successPayment(Request $request)
    {
        $paymentId = $request->get('paymentId');
        $payerId = $request->get('PayerID');
    
        if (empty($paymentId) || empty($payerId)) {
            // Redirigeix a una pàgina d'error o mostra un missatge
            return redirect('/')->with('error', "El pagament no s'ha pogut verificar.");
        }
    
        $payment = Payment::get($paymentId, $this->apiContext);
    
        $execution = new PaymentExecution();
        $execution->setPayerId($payerId);
    
        try {
            // Executa el pagament
            $result = $payment->execute($execution, $this->apiContext);
    
            // Comprova que el pagament s'ha completat amb èxit
            if ($result->getState() == 'approved') {
                // Aquí pots processar la informació de la transacció, 
                // com ara actualitzar la base de dades, etc.
                return redirect('/')->with('success', 'Pagament completat amb èxit.');
            }
        } catch (Exception $e) {
            // Gestiona els errors aquí
            return redirect('/')->with('error', 'Hi ha hagut un problema en processar el teu pagament.');
        }
    
        return redirect('/')->with('error', "El pagament no s'ha pogut completar.");
    }

    // Aquí pots afegir els mètodes per gestionar la cancel·lació  del pagament
}
```
Defineix les rutes
    
```php  
Route::get('/payment/create', 'PaymentController@createPayment');
Route::get('/payment/success', 'PaymentController@successPayment');
Route::get('/payment/cancel', 'PaymentController@cancelPayment');
```

És important seguir aquests passos detalladament i referir-se a la documentació específica de la biblioteca que estàs utilitzant per obtenir instruccions detallades i exemples de codi. La clau està en la correcta configuració i integració de les credencials de PayPal Sandbox i la correcta gestió de les respostes de l'API de PayPal.

**Notes Importants**
Aquest exemple és molt bàsic i només per a fins educatius. En un entorn de producció, hauràs de gestionar molts altres aspectes com la verificació de seguretat, el maneig d'errors més detallat, i la integració amb la base de dades.
Assegura't de provar aquest codi en l'entorn de Sandbox de PayPal abans de considerar la seva implementació en producció.
Personalitza els imports del pagament (import, moneda, descripció) segons les necessitats del teu projecte.

### Stripe (test mode amb targeta)

Stripe permet fer proves amb targetes fictícies en **test mode**. És recomanable usar **Stripe Checkout** perquè simplifica el flux.

1. Crea un compte a Stripe i activa el **test mode**.
2. Obté les claus de test i afegeix-les al `.env`:

```dotenv
STRIPE_KEY=pk_test_your_key
STRIPE_SECRET=sk_test_your_secret
```

3. Instal·la el SDK de Stripe:

```bash
composer require stripe/stripe-php
```

4. Endpoint bàsic per crear una sessió de Checkout:

```php
use Stripe\Stripe;
use Stripe\Checkout\Session;

public function createStripeCheckout()
{
    Stripe::setApiKey(env('STRIPE_SECRET'));

    $session = Session::create([
        'mode' => 'payment',
        'line_items' => [[
            'price_data' => [
                'currency' => 'eur',
                'product_data' => ['name' => 'Subscripció Demo'],
                'unit_amount' => 1000, // 10,00 €
            ],
            'quantity' => 1,
        ]],
        'success_url' => url('/stripe/success'),
        'cancel_url' => url('/stripe/cancel'),
    ]);

    return redirect()->away($session->url);
}
```

5. Per a provar, utilitza una targeta de test (p. ex. `4242 4242 4242 4242` amb qualsevol data futura i CVC).

## Integració de n8n en el desenvolupament web (mashups)

n8n és una eina d'automatització que pot actuar com a **orquestrador de dades** entre serveis gratuïts i la teua app web. Pots fer que n8n agregue dades de diverses APIs obertes i expose un endpoint únic per a la teua aplicació.

### Patró recomanat
1. **n8n** rep una petició (Webhook).
2. **n8n** consulta una o més APIs gratuïtes (open data, Open-Meteo, OpenStreetMap, etc.).
3. **n8n** normalitza i respon amb JSON.
4. **Laravel** consumeix eixe JSON com si fora una API pròpia.

### Exemple de flux en n8n
- **Webhook** (trigger) → **HTTP Request** (API externa) → **Set** (netejar camps) → **Respond to Webhook**.

### Mini-exemple n8n + OpenStreetMap (Nominatim)

Objectiu: rebre un nom de lloc i tornar coordenades bàsiques.

**Flux en n8n**
1. **Webhook** (POST) amb cos:
   ```json
   { "q": "Universitat de València" }
   ```
2. **HTTP Request**:
   - Method: `GET`
   - URL: `https://nominatim.openstreetmap.org/search`
   - Query:
     - `q` = `{{$json.q}}`
     - `format` = `json`
     - `limit` = `1`
   - Headers:
     - `User-Agent`: `dwes-mashup-class`
3. **Set** (netejar resposta):
   - `name` = `{{$json[0].display_name}}`
   - `lat` = `{{$json[0].lat}}`
   - `lon` = `{{$json[0].lon}}`
4. **Respond to Webhook** amb:
   ```json
   { "name": "...", "lat": "...", "lon": "..." }
   ```

**Consum des de Laravel**

```php
use Illuminate\Support\Facades\Http;

$response = Http::post(env('N8N_WEBHOOK_URL'), [
    'q' => 'Universitat de València',
]);

$coords = $response->json();
```

### Exemple de crida des de Laravel

```php
use Illuminate\Support\Facades\Http;

$response = Http::post(env('N8N_WEBHOOK_URL'), [
    'city' => 'València',
    'date' => '2026-01-27',
]);

$data = $response->json();
```

### Seguretat bàsica
- Usa URLs de webhook amb token o afegeix un header secret.
- Limita i valida els paràmetres que accepts.
- Registra errors i temps de resposta per a depurar.

## Exemple de reutilització de codi

### Autenticació amb Google


#### Pas 1 - Instal·lació

Instal·lem el paquet de Google:

```console
composer require laravel/socialite
```

#### Pas 2 - Crear credencials a Google cloud

* Obre la Consola de Google Cloud: Visita [Google Cloud Console](https://goo.gle/3oFLcJ5).

**Crear un Projecte a Google Cloud**

* Crea un Nou Projecte: En la consola, crea un nou projecte si encara no en tens cap.
* Navega al Projecte: Un cop creat, selecciona el projecte per a configurar les credencials.

**Configurar OAuth Consent Screen**

* Vés a "APIs & Services > OAuth consent screen".
* Selecciona l'usuari extern i omple els detalls necessaris. ![Fig.1](imagenes/09/consentiment1.png).
* Afegeix la informació del teu domini i els detalls de l'aplicació. ![Fig.2](imagenes/09/consentiment2.png).


**Crear Credencials**

* Vés a "APIs & Services > Credentials".
* Clica a "Create Credentials" i selecciona "OAuth client ID".
* Selecciona l'aplicació web com a tipus d'aplicació. ![Fig.3](imagenes/09/credencials1.png).
* Afegeix les URL de redirecció autoritzades des de Laravel (p. ex., http://localhost/auth/google/callback per a l'entorn de desenvolupament).
* Obté l'ID de Client i el Secret de Client: Després de crear les credencials, anota l'ID de client i el secret que Google proporciona. ![Fig.4](imagenes/09/credencials2.png).

#### Pas 3 - Configuració de Socialite per a Google

```php
GOOGLE_CLIENT_ID=your-client-id
GOOGLE_CLIENT_SECRET=your-client-secret
GOOGLE_REDIRECT=http://localhost/auth/google/callback
```
Afegeix la Configuració de Google a config/services.php:

```php
'google' => [
    'client_id' => env('GOOGLE_CLIENT_ID'),
    'client_secret' => env('GOOGLE_CLIENT_SECRET'),
    'redirect' => env('GOOGLE_REDIRECT'),
],
```
#### Pas 4 - Creació de Rutes i Controladors

Defineix rutes en routes/web.php per a redirigir cap a Google i per al callback.

```php  
Route::get('auth/google', [LoginController::class, 'redirectToGoogle'])->name('auth.google');
Route::get('auth/google/callback', [LoginController::class, 'handleGoogleCallback'])->name('auth.google.callback');
```

En LoginController, afegeix la lògica per a redirigir a l'usuari cap a Google i manejar el callback.

redirectToGoogle: Redirigeix l'usuari a la pàgina d'autenticació de Google.
handleGoogleCallback: Processa la resposta de Google, crea o troba un usuari, i genera un token de Sanctum.

```php  
<?php
// En LoginController 

public function redirectToGoogle()
{
    return Socialite::driver('google')->redirect();
}


public function handleGoogleCallback()
{
    try {
        $googleUser = Socialite::driver('google')->stateless()->user();

            // Cerca o crea l'usuari a la base de dades
            $user = User::updateOrCreate(
                ['email' => $googleUser->email],
                [
                    'name' => $googleUser->name,
                    'google_id' => $googleUser->id,
                    'avatar' => $googleUser->avatar,
                ]
            );

            // Autentica l'usuari
            Auth::login($user);

        // Generar token Sanctum
        // Si volem autenticar en l'API podriem generar un token
        $token = $userr->createToken('Personal Access Token')->plainTextToken;

        // Redirigir l'usuari amb el token
        return view('auth.success', ['token' => $token]); // Asumint que tens una vista 'auth.success'

    } catch (\Exception $e) {
        // Maneig d'errors
        return view('auth.error', ['error' => $e->getMessage()]); // Asumint que tens una vista 'auth.error'
    }
}
```
Caldrà fer unes modificacions en el model User.php

```php
 
    protected $fillable = [
        'name',
        'email',
        'password',
        'google_id',
        'avatar',
    ];
 
```

I afegir el camp google_id i avatar a la migració de la base de dades

#### Pas 5 - Creació de les vistes de comprovació

Crea dues vistes en resources/views/auth: success.blade.php i error.blade.php.

```php
{{-- resources/views/auth/success.blade.php --}}

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Autenticació Exitosa</title>
</head>
<body>
    <h1>Benvingut/da!</h1>
    <p>La teua autenticació ha sigut exitosa.</p>
    <p>El teu token d'accés és: {{ $token }}</p>
</body>
</html>
```

```php
{{-- resources/views/auth/error.blade.php --}}

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Error d'Autenticació</title>
</head>
<body>
    <h1>Error d'Autenticació</h1>
    <p>Ha ocorregut un error durant el procés d'autenticació: {{ $error }}</p>
</body>
</html>
```

#### Pas 6. Inclou l'enllaç en el login per redirigir a google

```html
<a href="{{ route('auth.google') }}">Inicia sessió amb Google</a>
```

### Actualització de la classificació en temps real.

Després de configurar el pusher i el Laravel Echo, podem implementar que la classificació s'actualitze de forma automàtica quan es canvie un resultat.

1. Afegir el codi per a gestionar l'escolta en el frontend:

```bootstrap.js
window.Echo.channel('futbol-femeni')
    .listen('.PartitActualitzat', (data) => {
        console.log('Esdeveniment rebut:', data);
        Livewire.dispatch('PartitActualitzat',data);
    });
```

2. Modificar el routes/channel.php per a autoritzar l'accés al canal:

```php

use Illuminate\Support\Facades\Broadcast;

Broadcast::channel('futbol-femeni', function () {
    return true;
});
```

3. Modificar el component livewire per a gestionar l'esdeveniment rebut:

```php
    #[On('PartitActualitzat')] 
    public function actualitzarClassificacio()
    {
        $this->calcularClassificacio();
        $this->dispatch('$refresh');
    }
```

4. Crear el esdeveniment que s'enviarà al canal:

```php
namespace App\Events;

use Illuminate\Broadcasting\Channel;
use Illuminate\Broadcasting\InteractsWithSockets;
use Illuminate\Contracts\Broadcasting\ShouldBroadcast;
use Illuminate\Foundation\Events\Dispatchable;
use Illuminate\Queue\SerializesModels;

class PartitActualitzat implements ShouldBroadcast
{
    use Dispatchable, InteractsWithSockets, SerializesModels;

    public $partit;

    public function __construct($partit)
    {
         $this->partit = $partit;
    }

    public function broadcastOn()
    {
        return new Channel('futbol-femeni');
    }

    public function broadcastAs()
    {
         return 'PartitActualitzat';
    }
}
```

5. Disparar l'esdeveniment des del model:

```php
protected static function booted()
    {
        static::updated(function ($partit) {
            event(new PartitActualitzat($partit));
        });
    }
```

### Exemple d'integració amb IA (Gemini o ChatGPT)

Utilitza el servei en el teu controlador per obtenir una descripció (equip o estadi):

```php
public function show(Equip $equip) {
    $descripcio = OpenAIService::getResponse(
        'Dona una descripció del '.$equip->nom.' de Futbol Femení'
    );
    // o bé
    // $descripcio = GeminiService::getResponse(
    //     'Dona una descripció de l\'estadi '.$equip->estadi->nom
    // );

    return view('equips.show', compact('equip','descripcio'));
}
```

Modifica la vista per a mostrar la descripció:

```php
@extends('layouts.futbolFemeni')
@section('title', "Pàgina equip Femení" )
@section('content')
<x-equip
   :nom="$equip->nom"
   :estadi="$equip->estadi->nom"
   :titols="$equip->titols"
   :escut="$equip->escut"
   :jugadores="$equip->jugadores"
   :descripcio="$descripcio"
/>
@endsection
```

Modifica el component de la vista ...

### Activitats

1. Autenticació amb Google per a Futbol-femeni: crea el rol [convidat], sense permisos en BD i sense password; només pot entrar amb Google. La resta d'usuaris no poden autenticar-se amb Google.
2. IA al projecte de Futbol-femeni: genera una descripció d'equip o estadi amb Gemini o ChatGPT i mostra-la a la vista (cache simple opcional).
3. Mashup amb dades obertes (crides directes): **meteorologia**. Propostes:
   - **Open‑Meteo** (sense API key, forecast global).
   - **AEMET OpenData** (API oficial d’Espanya amb clau gratuïta).
   Agrega la predicció del dia o el risc de pluja i mostra-ho en la fitxa d’equip/estadi.
4. Opcional (si teniu classificació): quan canvia la classificació, mostra una alerta i canvia el color de l'equip a roig si baixa o a verd si puja.








 
