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
    * Per als models **courses**, **modules** i **families** fes-ho des del sql (no cal factory).
    * Crea 100 usuaris registrats. Un ha de ser administrador.
    * Crea 100 llibres amb un preu aleatori entre 10 i 100 i disponibles per a la venda.
    * Crea 100 llibres més amb un preu aleatori entre 10 i 100 i no disponibles per a la venda, per que ja ho estan.
    * Crea les 100 vendes per a eixos llibres.

704. Crea les rutes corresponents a cada acció del controlador, i els mètodes per a visualitzar les vistes. 
    * Crea un controlador de recursos per a **Book**, **Course**,  **Family** i **Module**. 

705. Crea les vistes corresponents a cada acció del controlador. 
706. Fes que la pàgina principal mostre la llista de llibres disponibles.
707. Quan un usuari es logueja mostra-li la seua llista de llibres a la venda, amb el botons per modificar, esborrar i crear un llibre nou.
708. Ha de tenir un enllaç per vore les seues vendes.
709. L'administrador podrà veure la llista d'usuaris per a donar de baixa. Així mateix també podrà fer un manteniment de les taules modules, courses i families.