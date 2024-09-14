---
title: Arquitectures Web en Entorn Servidor
author: [Ignasi Gomis Mullor]
date: 2024
---

# Introducció a les Arquitectures Web

- **Client-Servidor**: Model tradicional de comunicació.
- **Execució del codi**:
    - **Client**: JavaScript, HTML, CSS
    - **Servidor**: PHP, Python, Node.js
- **Flux de dades**:
    - Peticions del client → Respostes del servidor

---

# Generació Dinàmica de Pàgines Web

- **Definició**: Pàgines web que es generen sobre la marxa en resposta a peticions del client.
- **Avantatges**:
    - Contingut personalitzat per l'usuari.
    - Interacció amb bases de dades.
    - Millor manteniment del codi.
- **Comparació** amb la inclusió de scripts:
    - Scripts: Es poden incloure directament a HTML.
    - Generació dinàmica: Major flexibilitat i escalabilitat.

---

# Execució de Codi en Servidors Web

- **Serveis Web**:
    - **Apache**, **Nginx**, **IIS**: Exemples de servidors web.
- **Mecanismes d'execució**:
    - **PHP**: Codi interpretat en temps real.
    - **Node.js**: Basat en esdeveniments asíncrons.
    - **ASP.NET**: Integrat amb serveis Windows.

---

# Serveis i Servidors d'Aplicacions

- **Funcionalitats dels servidors d'aplicacions**:
    - Processament d'aplicacions web complexes.
    - Gestió de sessions i autenticació d'usuaris.
    - Comunicació entre bases de dades i aplicacions web.
- **Exemples**:
    - **Tomcat**: Servidor d'aplicacions Java.
    - **WildFly**: Suport per a aplicacions Java EE.

---

# Llenguatges i Tecnologies del Servidor

- **Principals llenguatges**:
    - **PHP**: Popular per aplicacions web dinàmiques.
    - **Node.js**: Basat en JavaScript, ideal per aplicacions asíncrones.
    - **ASP.NET**: Utilitzat amb llenguatge C# en entorns Microsoft.
    - **Ruby on Rails**: Facilita el desenvolupament ràpid d'aplicacions.
- **Comparativa**:
    - PHP: Facilitat d'ús.
    - Node.js: Ràpid i lleuger.
    - ASP.NET: Integració robusta amb Windows.

---

# Eines i Frameworks de Desenvolupament

- **Frameworks per a Servidor**:
    - **Laravel**: Framework PHP amb arquitectura MVC.
    - **Express.js**: Minimalista per a aplicacions amb Node.js.
    - **Django**: Framework Python amb seguretat integrada.
- **Avantatges d'utilitzar frameworks**:
    - Estandardització de codi.
    - Millor organització i escalabilitat.
    - Funcionalitats de seguretat integrades.

---

# Integració de Llenguatges de Marques i Llenguatges del Servidor

- **HTML + Llenguatge de Programació del Servidor**:
    - Inclusió dinàmica de contingut dins de pàgines HTML.
    - **Exemple en PHP**:
      ```php
      <?php
        echo "<h1>Benvingut a la nostra web!</h1>";
      ?>
      ```
- **Eines per a la integració**:
    - **Blade**: Motor de plantilles en Laravel.
    - **Jinja**: Motor de plantilles en Django.
