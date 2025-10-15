# Preguntes Tipus Test - Laravel Dades
 
1. **Què és un model en Laravel?**
     - A) Una representació d’una taula de la base de dades.
     - B) Una vista d'una base de dades.
     - C) Un representació de la base de dades.
     - D) Una plantilla Blade.

2. **Quina propietat del model indica els camps que es poden omplir mitjançant assignació massiva?**
     - A) `$guarded`
     - B) `$timestamps`
     - C) `$fillable`
     - D) `$fields`
 
3. **Per defecte, com s’anomena la propietat que referència la clau primària en els models de Laravel?**
     - A) `id`
     - B) `primary`
     - C) `key`
     - D) `primaryKey`

4. **Com s'executen totes les migracions pendents?**
     - A) `php artisan migrate:run`
     - B) `php artisan migrate`
     - C) `php artisan migration:execute`
     - D) `php artisan db:migrate`

5. **Quin mètode es fa servir per desfer els canvis d’una migració?**
     - A) `rollback`
     - B) `reset`
     - C) `migrate:rollback`
     - D) `migrate:reset`

6. **Què fa el comandament `php artisan migrate:fresh`?**
     - A) Actualitza totes les migracions.
     - B) Comprova l'estat de les migracions.
     - C) Esborra només les taules buides.
     - D) Esborra totes les dades de la base de dades i torna a aplicar les migracions.

7. **Què són els seeders en Laravel?**
     - A) Una eina per gestionar models.
     - B) Scripts per modificar esquemes de la base de dades.
     - C) Funcions per generar dades fictícies.
     - D) Classes per generar dades inicials o de prova.
 
8. **Què fa el comandament `php artisan db:seed`?**
     - A) Executa tots els seeders configurats a la classe DatabaseSeeder.
     - B) Esborra totes les dades de la base de dades.
     - C) Actualitza els models.
     - D) Aplica només els seeders pendents.

9. **Què és un factory en Laravel?**
     - A) Una classe per definir regles de validació.
     - B) Una eina que defineix regles per a poder generar dades fictícies.
     - C) Un component per gestionar vistes.
     - D) Una classe per generar migracions.

10. **Com s’utilitza un factory per crear 5 registres?**
     - A) `Model::factory(5)->create();`
     - B) `Model::factory()->create(5);`
     - C) `Model::factory()->count(5)->create();`
     - D) `Model::factory(5)->make();`

11. **Quina relació permet que un model tinga  molts altres models associats?**
     - A) `hasOne`
     - B) `hasMany`
     - C) `belongsTo`
     - D) `belongsToMany`

12. **Quin mètode es fa servir per definir una clau aliena en una relació?**
    - A) `foreign`
    - B) `hasForeign`
    - C) `belongsTo`
    - D) `references`

13. **Quina estructura conté una migració per crear una taula?**
    - A) `up` i `rollback`
    - B) `start` i `stop`
    - C) `up` i `down`
    - D) `create` i `delete`

14. **Com s’apliquen regles de validació a un formulari?**
    - A) `$request->check();`
    - B) `$request->validate();`
    - C) `$request->apply();`
    - D) `$request->rules();`
 
15. **Quin mètode retorna tots els missatges d’error després de validar?**
    - A) `$errors->get()`
    - B) `$errors->messages()`
    - C) `$errors->all()`
    - D) `$errors->list()`

Preguntes obertes :

1. **Com modularitzaries els components Blade per evitar repetir codi en els formularis de creació i edició? Posa exemples de components que podrien ser útils.**





 
2. **Com has utilitzat laravel per recuperar dades relacionades, com per exemple totes les jugadores d’un equip? Mostra un fragment del teu codi que ho demostre.**





3. **Has utilitzat alguna tècnica o eina específica per assegurar-te que les migracions es creen en el mateix ordre que les relacions entre les taules? Explica-ho.**





4. **Si afegim un nou camp edat a les jugadores, quins passos específics haurien de fer-se perquè el canvi es reflectís correctament a totes les parts de l'aplicació?**





5. **Quines estratègies has utilitzat per mostrar errors als usuaris quan els formularis no són validats o les dades no són desades correctament?**