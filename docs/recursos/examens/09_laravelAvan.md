# **Examen - Funcionalitats Avançades de Laravel**

## **Preguntes Tipus Test**

1. **Quin paquet de Laravel s'utilitza per implementar funcionalitats bàsiques d'autenticació de manera ràpida i senzilla?**
- A) Laravel Jetstream
- B) Laravel Passport
- C) Laravel Breeze
- D) Laravel Sanctum

2. **Com es poden assignar rols als usuaris en una aplicació Laravel?**
- A) Mitjançant middleware predeterminats
- B) Afegint un camp 'rol' a la taula d'usuaris i gestionant la lògica corresponent
- C) Utilitzant el sistema de cues de Laravel
- D) Configurant les rutes en el fitxer `web.php`

3. **Quina és la funció principal d'un middleware en Laravel?**
- A) Gestionar les migracions de la base de dades
- B) Manipular les sol·licituds HTTP entrants abans d'arribar al controlador
- C) Crear vistes Blade dinàmicament
- D) Enviar correus electrònics automàticament

4. **Com es poden mostrar les traduccions en una vista Blade de Laravel?**
- A) Utilitzant la funció `{{ trans('clau') }}`
- B) Utilitzant la funció `{{ __('clau') }}`
- C) Definint les traduccions directament en les vistes Blade.
- D) Utilitzant la funció `{{ config('clau') }}`

5. **Quina és la finalitat d'un Form Request en Laravel?**
- A) Gestionar les dades dels formularis d'una vista Blade.
- B) Validar i autoritzar les dades d'una sol·licitud HTTP abans de processar-les en el controlador.
- C) Enviar respostes JSON als clients.
- D) Crear components d'interfície d'usuari reactius sense necessitat de JavaScript.

6. **Quin mètode s'utilitza per enviar correus electrònics en Laravel?**
- A) `Mail::dispatch()`
- B) `Mail::mail()`
- C) `Mail::queue()`
- D) `Mail::send()`

7. **En Laravel, quin és el propòsit principal d'utilitzar el trait `RefreshDatabase` en les proves?**
- A) Millorar el rendiment de les proves evitant l'ús de la base de dades.
- B) Automatitzar la creació de fàbriques de models per a les proves.
- C) Restablir l'estat de la base de dades després de cada prova per assegurar un entorn net.
- D) Permetre l'accés a serveis externs durant les proves.
 
8. **Quina és la funció de Laravel Livewire?**
- A) Gestionar les migracions de la base de dades
- B) Crear components d'interfície d'usuari reactius sense necessitat de JavaScript
- C) Enviar correus electrònics automàticament
- D) Validar i autoritzar les dades d'una sol·licitud HTTP abans de processar-les en el controlador.

9. **Com es pot restringir l'accés a una ruta perquè només certs usuaris autenticats hi puguen accedir?**
- A) Definint la restricció en les rutes en el fitxer `routes/web.php`
- B) Implementant la lògica de restricció directament en els controladors associats.
- C) Utilitzant middleware que verifiquen els permisos de l'usuari.
- D) Configurant les opcions de la base de dades

10. **Com es poden programar tasques periòdiques en Laravel, com l'enviament automàtic de correus electrònics?**
- A) Utilitzant el sistema de cues de Laravel
- B) Configurant el fitxer `schedule.php` en la carpeta `config`
- C) Definint tasques en el mètode `schedule` de la classe `App\Console\Kernel` i utilitzant el planificador de tasques de Laravel
- D) Creant un controlador específic per a tasques programades
 
11. **En una classe de `Form Request` de Laravel, quin és el propòsit principal del mètode `rules()`?
- A) Definir les regles de validació per als camps del formulari.
- B) Personalitzar els missatges d'error de validació.
- C) Autoritzar l'usuari per a realitzar la sol·licitud.
- D) Establir valors per defecte per als camps del formulari.

12. **En una classe de `Form Request` de Laravel, quin és l'objectiu principal de sobrescriure el mètode `messages()`?
- A) Definir les regles de validació per als camps del formulari.
- B) Personalitzar els missatges d'error de validació.
- C) Autoritzar l'usuari per a realitzar la sol·licitud.
- D) Configurar els atributs HTML dels elements del formulari.

13. **Quin mètode s'utilitza per verificar si un usuari està autoritzat a realitzar una acció definida en una política?**
- A) `$user->check()`
- B) `$user->authorize()`
- C) `$user->can()`
- D) `$user->validate()`

14. **Quina és la funció principal d'una política (policy) en Laravel?**
- A) Manipular les sol·licituds HTTP entrants abans d'arribar al controlador
- B) Programa tasques periòdiques en Laravel.
- C) Enviar correus electrònics automàticament.
- D) Autoritzar accions dels usuaris sobre models específics.

15. **¿Quina de les següents opcions és correcta per a emmagatzemar un valor en la sessió en Laravel?**
- A) `Session::put('clau', 'valor');`
- B) `session(['clau' => 'valor']);`
- C) `$request->session()->put('clau', 'valor');`
- D) Totes les anteriors


Preguntes obertes :

1. Has creat un component Livewire per a mostrar la classificació dels equips. Descriu els passos seguits per a desenvolupar aquest component i com has gestionat la presentació de les dades de manera dinàmica.

2. En les vistes, has restringit les operacions per als usuaris no autenticats utilitzant les directives `@auth` i `@endauth`. Explica com has aplicat aquestes directives per a ocultar o mostrar elements específics de la interfície segons l'estat d'autenticació de l'usuari.

3. Per a assegurar que només els usuaris amb rol d'àrbitre poden modificar els partits, has utilitzat el mètode `authorize()` en el `Form Request` corresponent. Detalla com has implementat aquesta validació i com has configurat el middleware de rol per a reforçar aquesta restricció.

4. Has creat un correu electrònic per a enviar a tots els àrbitres el seu calendari anual de partits. Descriu el procés seguit per a generar i enviar aquest correu, incloent-hi com has obtingut les dades necessàries i com has assegurat que cada àrbitre reba la informació correcta.

5. En el component de jugadora, has implementat funcionalitats perquè els managers puguen crear, modificar o esborrar les seues jugadores, i que aquestes es mostren correctament en els equips. Explica com has gestionat aquestes operacions i com has assegurat que només els managers puguen realitzar-les sobre les jugadores dels seus propis equips.
