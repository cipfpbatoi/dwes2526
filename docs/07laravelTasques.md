# Tasques

## Tasques Programades (Task Scheduling)

Laravel proporciona una manera elegant d'executar tasques programades com l'enviament de correus, neteja de la base de dades, etc., sense necessitat de crear crons complexos al servidor.

### Configuració del Scheduler
Cron a Nivell de Servidor: Necessites afegir una entrada a crontab en el teu servidor que executa schedule:run cada minut.

```bash
* * * * * cd /path-de-tu-projecte && php artisan schedule:run >> /dev/null 2>&1
```

### Creació de Comandos

Pots crear comandos amb Artisan per a ser programats:

```bash
php artisan make:command NomComando
```

Això generarà una nova classe de comando en el directori app/Console/Commands.

#### Estructura del Comando
La classe del comando contindrà un parell de propietats i mètodes importants:

$signature: Una cadena que defineix com s'invoca el comando des de la línia de comandes.
$description: Una breu descripció del que fa el comando.
handle(): El mètode on escriuràs la lògica que s'executarà quan es cridi el comando.

#### Exemple de Comando
Suposem que vols crear un comando per a enviar correus de recordatori als usuaris. Ací tens un exemple:

```php
namespace App\Console\Commands;

use Illuminate\Console\Command;
use App\Models\User;
use App\Mail\ReminderMail;
use Illuminate\Support\Facades\Mail;

class SendReminders extends Command
{
    protected $signature = 'send:reminders';
    protected $description = 'Envia correus de recordatori als usuaris.';

    public function handle()
    {
        $users = User::all(); // Obtenir tots els usuaris

        foreach ($users as $user) {
            Mail::to($user->email)->send(new ReminderMail());
        }

        $this->info('Correus de recordatori enviats correctament!');
    }
}
```

### Programar el Comando

Una vegada creat el comando, el següent pas és programar-lo en l'arxiu app/Console/Kernel.php. Ací, pots definir quan s'ha d'executar el comando usant una varietat de mètodes com daily, hourly, everyMinute, etc.
    
```php
protected function schedule(Schedule $schedule)
{
$schedule->command('send:reminders')->daily();
}
```

En aquest exemple, el comando send:reminders s'executarà diàriament.



## Esdeveniments (Events) i Oïdors (Listeners)

Els esdeveniments són una forma de desacoplar diverses parts de l'aplicació i consisteixen en dos parts principals: esdeveniments (events) i oïdors (listeners).

### Creació d'Esdeveniments

```bash
php artisan make:event NomEsdeveniment
```
Açò crearà una nova classe d'esdeveniment dins del directori app/Events.

Exemple d'Esdeveniment:

```php  
namespace App\Events;

use Illuminate\Foundation\Events\Dispatchable;
use Illuminate\Queue\SerializesModels;

class UserRegistered
{
    use Dispatchable, SerializesModels;

    public $user;

    public function __construct(User $user)
    {
        $this->user = $user;
    }
}
```
En aquest exemple, l'esdeveniment UserRegistered s'utilitza per a anunciar que un usuari s'ha registrat.


### Creació d'Oïdors**

```bash
php artisan make:listener NomOidor --event=NomEsdeveniment
```

Els oïdors reaccionen quan s'activa un esdeveniment. Defineix la lògica de resposta en l'oïdor.

Exemple d'Oïdor:

```php
namespace App\Listeners;

use App\Events\UserRegistered;
use Illuminate\Queue\InteractsWithQueue;
use Illuminate\Contracts\Queue\ShouldQueue;

class SendWelcomeEmail
{
    use InteractsWithQueue;

    public function handle(UserRegistered $event)
    {
        // Enviar correu de benvinguda
        Mail::to($event->user->email)->send(new WelcomeEmail($event->user));
    }
}
```
En aquest exemple, l'oïdor SendWelcomeEmail escolta l'esdeveniment UserRegistered i envia un correu de benvinguda.

### Registrar Esdeveniments i Oïdors

Has de registrar els teus esdeveniments i oïdors en l'arxiu EventServiceProvider.php dins del directori app/Providers.
    
```php
protected $listen = [
'App\Events\UserRegistered' => [
'App\Listeners\SendWelcomeEmail',
],
];
```

### Disparar Esdeveniments

Pots disparar un esdeveniment en qualsevol part de la teua aplicació:    
```php  
event(new NomEsdeveniment($data));
```

## WebSockets

Els WebSockets permeten comunicacions bidireccionals en temps real entre el servidor i els clients. Laravel facilita treballar amb WebSockets a través de Laravel Echo i canals de difusió.

### Configuració Bàsica

**Instal·lar Laravel Echo**: Utilitza npm per a instal·lar les dependències necessàries.

```bash
npm install --save laravel-echo pusher-js
```

**Configuració del Fitxer .env**: Defineix les claus i secrets de Pusher (o la teua solució WebSocket).

### Creació de Canals

Defineix canals en routes/channels.php. Per exemple, un canal privat:

```php
Broadcast::channel('channel-name', function ($user) {
    return true; // Autorització
});
```

### Escoltar Esdeveniments amb Echo

A l'frontend, utilitza Laravel Echo per a escoltar esdeveniments en un canal:
    
```js
Echo.channel('channel-name')
.listen('EventName', (e) => {
console.log(e);
});
```

### Disparar Esdeveniments en Temps Real

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

### Exemple Complet

#### Pas 1: Configuració dels WebSockets
Primer, has de configurar el teu sistema per a utilitzar WebSockets. Laravel Echo i Laravel WebSockets (un paquet que permet crear un servidor de WebSockets directament en Laravel) són opcions populars.

1. Instal·la Laravel WebSockets:
    
```bash
composer require beyondcode/laravel-websockets
```

2. Publica les Configuracions i Migracions:

```bash
php artisan vendor:publish --provider="BeyondCode\LaravelWebSockets\WebSocketsServiceProvider" --tag="migrations"
php artisan vendor:publish --provider="BeyondCode\LaravelWebSockets\WebSocketsServiceProvider" --tag="config"
```
   
3. Executa les Migracions:
    
```bash
php artisan migrate
```
   
4. Configura .env per a usar el driver pusher:

```bash
BROADCAST_DRIVER=pusher

PUSHER_APP_ID=local
PUSHER_APP_KEY=local
PUSHER_APP_SECRET=local
PUSHER_APP_CLUSTER=mt1
```

5. Inicia el servidor de WebSockets:

```bash
php artisan websockets:serve
```

#### Pas 2: Crear Event Que Utilitza WebSockets

Ara, crearem un esdeveniment Laravel que utilitza WebSockets per a enviar notificacions.

1. Crea un esdeveniment que implemente ShouldBroadcast:

```bash
php artisan make:event BookSold
```

2. Edita l'esdeveniment BookSold:

```php
namespace App\Events;

use Illuminate\Broadcasting\Channel;
use Illuminate\Queue\SerializesModels;
use Illuminate\Broadcasting\PrivateChannel;
use Illuminate\Broadcasting\PresenceChannel;
use Illuminate\Foundation\Events\Dispatchable;
use Illuminate\Broadcasting\InteractsWithSockets;
use Illuminate\Contracts\Broadcasting\ShouldBroadcast;

class BookSold implements ShouldBroadcast
{
    use Dispatchable, InteractsWithSockets, SerializesModels;

    public $book;
    public $user;

    public function __construct($book, $user)
    {
        $this->book = $book;
        $this->user = $user;
    }

    public function broadcastOn()
    {
        return new PrivateChannel('user.'.$this->user->id);
    }
}
```

#### Pas 3: Disparar l'Esdeveniment

Quan es realitze una venda, dispara l'esdeveniment:

```php
event(new BookSold($book, $user));
```

#### Pas 4: Escoltar l'Esdeveniment al Frontend

Amb Laravel Echo, pots escoltar l'esdeveniment al frontend. Primer, assegura't de tindre Laravel Echo instal·lat i configurat al teu projecte frontend.

```js
Echo.private('user.' + userId)
    .listen('BookSold', (e) => {
        alert("El teu llibre s'ha venut!");
        // Actualitza la UI segons corresponga
    });
```

Aquest codi JavaScript escoltarà l'esdeveniment BookSold en un canal privat associat amb l'usuari. Quan es dispara l'esdeveniment, es mostrarà una alerta (o qualsevol altra acció que vulgues realitzar).











