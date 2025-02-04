# Exercicis per treballar els resultats d'aprenentatge (RA3 - RA8)

## 📌 RA3 - Escriu blocs de sentències embeguts en llenguatges de marques

### 1️⃣ Formulari de registre amb validació bàsica
- Crea un formulari en HTML que demane: nom, email, contrasenya i data de naixement.
- Usa PHP per validar que tots els camps estan plens i que l'email té el format correcte.
- Mostra missatges d'error si la validació falla.

### 2️⃣ Calculadora bàsica amb PHP
- Crea un formulari HTML amb dos camps numèrics i quatre botons (sumar, restar, multiplicar i dividir).
- Quan l'usuari prem un botó, mostra el resultat en la mateixa pàgina.
- Usa `$_POST` per processar les operacions.

### 3️⃣ Simulació d’una botiga amb carret de compra
- Mostra una llista de productes amb un botó "Afegir al carret".
- Quan es polsa el botó, el producte s’afegeix a una sessió.
- Mostra el total de la compra i permet eliminar productes.

---

## 📌 RA4 - Desenvolupa aplicacions web embegudes en llenguatges de marques

### 4️⃣ Sistema de sessió d’usuari
- Crea un sistema d’inici de sessió amb PHP on els usuaris puguen entrar amb un nom d'usuari i una contrasenya.
- Mostra un missatge de benvinguda si la sessió està activa.
- Afig un botó de tancament de sessió que esborre la sessió.

### 5️⃣ Control d'accés a una pàgina web
- Crea dues pàgines: una pública i una privada.
- Els usuaris només poden accedir a la privada si estan autenticats.
- Redirigeix els usuaris no autenticats a la pàgina de login.

### 6️⃣ Sistema de comentaris amb sessions
- Permet als usuaris afegir comentaris a una pàgina sense base de dades.
- Guarda els comentaris en `$_SESSION` i mostra’ls ordenats per ordre d'inserció.
- Afig la possibilitat d’eliminar comentaris.

---

## 📌 RA5 - Desenvolupa aplicacions web separant el codi de presentació de la lògica de negoci

### 7️⃣ Refactorització d’una aplicació en PHP amb MVC
- Crea una aplicació PHP que gestione una llista de tasques (CRUD bàsic).
- Implementa la separació del codi en:
    - Model (`Task.php`): Gestiona les dades.
    - Vista (`tasks.view.php`): Mostra les tasques.
    - Controlador (`TaskController.php`): Gestiona les operacions (crear, eliminar, modificar).

### 8️⃣ Plantilles amb Twig
- Instal·la Twig i refés una aplicació existent per a utilitzar plantilles.
- Separa les dades del codi HTML usant `{{ variable }}` dins de les plantilles.

### 9️⃣ Autenticació avançada amb Laravel
- Implementa un sistema d’autenticació amb Laravel `Auth`.
- Personalitza la vista de login i registre.
- Crea diferents rols d’usuari (administrador, usuari).

---

## 📌 RA6 - Aplicacions web amb accés a bases de dades

### 🔟 CRUD de gestió d'usuaris en PHP
- Crea una aplicació que permeta afegir, modificar i eliminar usuaris en una base de dades MySQL.
- Utilitza `PDO` per fer consultes segures.
- Mostra un llistat d'usuaris en una taula HTML.

### 1️⃣1️⃣ Sistema de gestió de publicacions en Laravel
- Crea un projecte Laravel amb autenticació.
- Genera un model `Post` amb camps `title`, `content`, `user_id`.
- Implementa el CRUD amb Eloquent i Blade.

### 1️⃣2️⃣ Autenticació d'usuaris amb base de dades
- Adapta el sistema d’autenticació PHP per utilitzar una base de dades.
- Desa les credencials en MySQL i verifica els accessos fent consultes a la BD.

---

## 📌 RA7 - Desenvolupament de serveis web reutilitzables

### 1️⃣3️⃣ Creació d'una API REST amb Laravel
- Implementa un controlador d'API per gestionar tasques (`TaskController`).
- Implementa endpoints:
    - `GET /tasks` (llistat de tasques)
    - `POST /tasks` (crear una nova tasca)
    - `PUT /tasks/{id}` (actualitzar tasca)
    - `DELETE /tasks/{id}` (esborrar tasca)

### 1️⃣4️⃣ Autenticació JWT en una API
- Instal·la `laravel/passport` o `sanctum` per gestionar autenticació per tokens.
- Crea un endpoint `/login` que retorne un token JWT.
- Protegeix altres endpoints perquè només funcionen amb autenticació.

### 1️⃣5️⃣ Consumir una API externa amb Laravel
- Utilitza `GuzzleHTTP` per consumir una API externa, per exemple, obtenir dades meteorològiques des d’una API com OpenWeather.
- Mostra la informació en una vista Laravel.

---

## 📌 RA8 - Generació de pàgines web dinàmiques amb frameworks

### 1️⃣6️⃣ Generació de documents PDF amb Laravel
- Instal·la `barryvdh/laravel-dompdf`.
- Implementa una funcionalitat per generar un informe en PDF amb dades d’una base de dades.
- Exemple: Generar una factura en PDF amb la informació del client i els productes comprats.

### 1️⃣7️⃣ Gestió de permisos amb Middleware
- Crea un middleware per restringir accés a certes rutes segons el rol de l’usuari.
- Exemple: `/admin` només pot ser accedit per administradors.

### 1️⃣8️⃣ Aplicació en temps real amb Laravel i Pusher
- Implementa un xat en temps real amb Laravel, Pusher i WebSockets.
- Mostra missatges instantanis entre dos usuaris sense necessitat de recarregar la pàgina.
