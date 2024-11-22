# Qüestionari Avaluable

## Secció 1: Preguntes tancades (Teoria)

1. **Què és un framework i per què és útil en el desenvolupament d'aplicacions web?**
    - a) És una eina que facilita la gestió de bases de dades.
    - b) És un conjunt d’eines i regles que permeten estructurar aplicacions web de manera eficient.
    - c) És un llenguatge de programació utilitzat per desenvolupar aplicacions web.
    - d) És un conjunt de llibreries per afegir funcionalitats a l'aplicació.

2. **Què és el patró MVC i quines capes defineix?**
    - a) És un patró que separa la lògica de negoci, la base de dades i les vistes.
    - b) És un patró que separa models, vistes i controladors.
    - c) És una estructura que defineix mòduls, variables i connexions.
    - d) És una configuració de Laravel per gestionar les rutes.

3. **Quin és l'objectiu principal de la capa de presentació en MVC?**
    - a) Gestionar les dades d’entrada i sortida.
    - b) Connectar directament amb la base de dades.
    - c) Mostrar el resultat de la lògica de negoci a l’usuari de manera visual.
    - d) Validar els formularis de l'usuari.

4. **Què fa la funció `@vite` en una vista Blade?**
    - a) Crea un formulari dinàmic.
    - b) Inclou fitxers CSS o JavaScript i activa Hot Module Replacement (HMR).
    - c) Genera rutes automàtiques.
    - d) Valida dades dins del controlador.

5. **Per què és important utilitzar controladors en Laravel?**
    - a) Perquè Laravel obliga a utilitzar-los.
    - b) Per gestionar la lògica de negoci de manera separada de les rutes.
    - c) Per emmagatzemar dades temporals.
    - d) Per fer que les vistes siguin més eficients.

6. **Quina diferència hi ha entre `view()` i `return` en Laravel?**
    - a) `return` sempre retorna dades JSON, mentre que `view()` mostra vistes HTML.
    - b) `view()` s'utilitza per carregar vistes, mentre que `return` pot retornar qualsevol tipus de dades.
    - c) `return` només funciona amb rutes, i `view()` amb controladors.
    - d) No hi ha cap diferència funcional.

7. **Com es passa informació del controlador a la vista en Laravel?**
    - a) Mitjançant un array o la funció `compact`.
    - b) Amb variables globals.
    - c) Utilitzant sessions.
    - d) Directament amb JSON.

8. **Quina diferència hi ha entre `Route::get()` i `Route::post()`?**
    - a) `Route::get()` és per obtenir dades, mentre que `Route::post()` s'utilitza per enviar dades al servidor.
    - b) No hi ha cap diferència funcional.
    - c) `Route::post()` només funciona amb AJAX.
    - d) `Route::get()` és per formularis, i `Route::post()` per JSON.

9. **Com es defineixen rutes en Laravel?**
    - a) Mitjançant el fitxer `routes/web.php`.
    - b) Des del controlador directament.
    - c) Amb la funció `route()` dins d’una vista Blade.
    - d) No cal definir-les, Laravel les crea automàticament.

10. **Què és una vista Blade i quins avantatges ofereix?**
    - a) És un tipus especial de controlador que conté codi HTML i PHP.
    - b) És una plantilla de presentació que permet estructurar HTML amb codi Blade.
    - c) És un mètode que genera automàticament formularis dinàmics.
    - d) És un fitxer CSS que s’inclou amb `@vite`.

11. **Quina diferència hi ha entre utilitzar `Route::resource()` i definir rutes manualment?**
    - a) `Route::resource()` genera automàticament totes les rutes principals d'un controlador de recursos.
    - b) No hi ha cap diferència; totes dues fan el mateix.
    - c) `Route::resource()` és per a models, mentre que les rutes manuals són per a funcions estàtiques.
    - d) Les rutes manuals són més ràpides d'executar que `Route::resource()`.

12. **Què és el mètode `compact()` i per què és útil en Laravel?**
    - a) Crea un array associatiu a partir de variables existents amb el mateix nom.
    - b) És un mètode que optimitza el rendiment de les vistes.
    - c) Permet passar dades d'un controlador a un altre.
    - d) Genera rutes dinàmicament.

13. **Com es pot reutilitzar codi a les vistes Blade?**
    - a) Utilitzant components Blade o plantilles amb `@include` i `@extends`.
    - b) Definint variables globals accessibles des de totes les vistes.
    - c) Emprant sessions per compartir informació entre vistes.
    - d) Copiant el codi en cada vista per assegurar que funcioni correctament.

14. **Què fa el mètode `redirect()` en Laravel?**
    - a) Redirigeix a una altra pàgina o ruta.
    - b) Genera una resposta amb codi d'estat 404.
    - c) Crea una nova vista en temps real.
    - d) Converteix una resposta en un fitxer descarregable.

15. **Com pots protegir un projecte Laravel contra atacs Cross-Site Request Forgery (CSRF)?**
    - a) Utilitzant el middleware `VerifyCsrfToken` i el token `@csrf` en els formularis.
    - b) Definint polítiques estrictes de permisos a la base de dades.
    - c) Encriptant totes les respostes enviades al client.
    - d) Limitant l'accés a les vistes només a usuaris autenticats.

---

## Secció 2: Preguntes obertes (Pràctica)

1. Explica breument com has creat el llistat d'estadis a l'exercici pràctic.

2. Què fa la ruta `/estadis/crear` en el projecte, i quina funcionalitat afegeix al llistat d'estadis?

3. Com es pot incloure un fitxer CSS al projecte i fer que s’aplique a una vista concreta?

4. Què és la directiva @include a Blade, i com pots utilitzar-la per fer el teu codi més modular?

5. Què passa si a la vista Blade intentes accedir a una clau que no existeix en un array? Com pots evitar errors?

6. Què passa si una ruta definida en el fitxer web.php no troba una vista o controlador associat? Com pots evitar errors en aquests casos?