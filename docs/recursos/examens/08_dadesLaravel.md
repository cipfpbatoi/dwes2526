# Preguntes Tipus Test - Laravel Dades

## **Secció: Models i ORM**

1. **Quina és la relació un a molts entre models en Laravel?**
    - A) `hasOne`
    - B) `hasMany`
    - C) `belongsTo`
    - D) `belongsToMany`

2. **Com es desactiva l'ús de timestamps en un model?**
    - A) `$timestamps = true;`
    - B) `$timestamps = false;`
    - C) `$timestamps = null;`
    - D) No es pot desactivar.

3. **Quina estructura conté una migració per crear una taula?**
    - A) `up` i `rollback`
    - B) `start` i `stop`
    - C) `up` i `down`
    - D) `create` i `delete`

4. **Com s'executen totes les migracions pendents?**
    - A) `php artisan migrate:run`
    - B) `php artisan migrate`
    - C) `php artisan migration:execute`
    - D) `php artisan db:migrate`

5. **En quina carpeta es guarden els seeders?**
    - A) `database/migrations`
    - B) `app/Seeders`
    - C) `database/seeders`
    - D) `app/Database/Seeds`

6. **Com s'executa un seeder específic?**
    - A) `php artisan db:seed --class=<NomSeeder>`
    - B) `php artisan db:seed <NomSeeder>`
    - C) `php artisan seed:run --class=<NomSeeder>`
    - D) `php artisan seed:execute <NomSeeder>`

7. **Quina llibreria es fa servir per generar dades falses en els seeders?**
    - A) Faker
    - B) MockData
    - C) RandomData
    - D) TestData

8. **Quin comandament crea un factory?**
    - A) `php artisan make:factory`
    - B) `php artisan create:factory`
    - C) `php artisan factory:make`
    - D) `php artisan generate:factory`


9. **On es guarden els factories per defecte?**
    - A) `app/Factories`
    - B) `database/factories`
    - C) `resources/factories`
    - D) `database/seeders`

10. **Què fa el mètode `definition` dins d'un factory?**
    - A) Defineix les relacions entre models.
    - B) Defineix els valors aleatoris dels camps.
    - C) Executa els seeders associats.
    - D) Aplica les migracions pendents.

11. **Com es defineix una relació molts a molts?**
    - A) `hasMany`
    - B) `hasOne`
    - C) `belongsTo`
    - D) `belongsToMany`

12. **Com es pre-carreguen dades relacionades per evitar múltiples consultes?**
    - A) Amb el mètode `load`.
    - B) Amb el mètode `with`.
    - C) Amb el mètode `join`.
    - D) Amb el mètode `preload`.
 
13. **Quina regla de validació s’utilitza per un camp obligatori?**
    - A) `filled`
    - B) `exists`
    - C) `required`
    - D) `nullable`

14. **Quina regla de validació comprova si un camp és únic a la taula?**
    - A) `unique`
    - B) `distinct`
    - C) `exists`
    - D) `single`

15. **Quina regla de validació assegura que un valor és un número?**
    - A) `integer`
    - B) `digits`
    - C) `numeric`
    - D) `number`

### Preguntes obertes

- 1. **Si els formularis permeten pujar una foto de la jugadora, com gestionaries les validacions per assegurar-te que només s’accepten imatges i que tenen una mida màxima determinada?**
- 2. **Com modularitzaries els components Blade per evitar repetir codi en els formularis de creació i edició? Posa exemples de components que podrien ser útils.**
- 3. **Quins camps has validat en els formularis de creació o edició? Com has implementat aquestes validacions al controlador?** 
- 4. **Com has relacionat els camps equip_local i equip_visitant a la taula partits? Per què has triat aquest disseny i com afecta les consultes?**
- 5. **Com garantitzaries que les dades generades amb factories siguin realistes i coherents entre si, especialment per als partits? Per exemple, que el local i el visitant no siguin el mateix equip.**