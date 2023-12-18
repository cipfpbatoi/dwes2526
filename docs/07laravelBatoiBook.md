## Activitats 


701. Crea les migracions per a les taules **books**, **courses**, **families**, **modules** i **sales**. 
     * L'ordre per a crear les migracions depedrà de les claus alienes. Així en este cas hauria de ser (families,courses,modules,books,sales).
     * Mira de crear també les claus alienes
     * Tria el tipus de dades adequat per a cada camp.
     * Sigues curós en la nomenclatura de les claus aliènes.
     * Afegiex un camp administrador a la taula **users** per a saber si un usuari és administrador o no.

702. Crea els models per a les taules **books**, **courses**, **families**, **modules** i **sales**. 
     * Crea les relacions entre models.

703. Crea els seeders i els factorys per a cada model.
    * Per als models **courses**, **modules** i **families** fes-ho des del sql (**no cal factory**).

!!! tip "Recomanació"
        Hauràs de copiar els fitxers .json a la carpeta storage/app/public. Podràs accedir-hi amb l'instrucció **Storage::disk('public')->path('nomfitxer.json')**.

!!! tip "Recomanació"
        Una vegada que accedim al fitxer json, per a convertir-lo a un array associatiu, utilitzarem la funció **json_decode**. Després per a accedir a les dades utilitzarem la notació **$array[2]['data']**.


* Crea 100 usuaris registrats. Un ha de ser administrador.
* Crea 100 llibres amb un preu aleatori entre 5 i 25 i disponibles per a la venda.
* Crea les 100 vendes per a 100 llibres més.

!!! tip "Recomanació"
    Al crear el seeder de sales, pots crear primer el llibre i desprès vendre'l. Per això pots utilitzar el mètode **create** del model **Book**. Per exemple:
    
    ```php
    $soldDate = $this->faker->dateTimeBetween('-1 years', 'now');
    $book = Book::factory()->create([
        'soldDate' => $soldDate->format('Y-m-d'), // Data de l'any passat
    ]);
    ```

704. Crea les rutes corresponents a cada acció del controlador, i els mètodes per a visualitzar les vistes. 
    * Crea un controlador de recursos per a **Book**, **Course**,  **Family** i **Module**.
705. Crea les vistes corresponents a cada acció del controlador bookController (per a crear les vistes pots utilitzar el chatGtp). 
706. Fes que la pàgina principal (quan no s'estiga loguejat) mostre la llista de llibres disponibles(en modo fitxa, paginades de 10 en 10) (utilitza un component per a crear la fitxa del llibre).
707. Quan un usuari es logueja mostra-li la seua llista de llibres a la venda, amb el botons per modificar, esborrar i crear un llibre nou.
708. Ha de tenir un enllaç per vore les seues vendes.
709. L'administrador podrà veure la llista d'usuaris per a donar de baixa. 
710. Així mateix també podrà fer un manteniment de les taules modules, courses i families.