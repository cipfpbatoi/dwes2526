# 1. Arquitectures Web

??? abstract "Duració i criteris d'avaluació"

    Duració estimada: 4 hores

    <hr />

    | Resultat d'aprenentatge | Criteris d'avaluació|
    | -------                 | -------             |
    | 1. Selecciona les arquitectures i tecnologies de programació web en entorn servidor, analitzant les seves capacitats i característiques pròpies. | a) S'han caracteritzat i diferenciat els models d'execució de codi en el servidor i en el client Web. <br/> b) S'han reconegut els avantatges que proporciona la generació dinàmica de pàgines Web i les seues diferències amb la inclusió de sentències de guions a l'interior de les pàgines Web. <br/> c) S'han identificat els mecanismes d'execució de codi en els servidors Web. <br/> d) S'han reconegut les funcionalitats que aporten els servidors d'aplicacions i la seua integració amb els servidors Web. <br/> e) S'han identificat i caracteritzat els principals llenguatges i tecnologies relacionats amb la programació Web en entorn servidor. <br/> f) S'han verificat els mecanismes d'integració dels llenguatges de marques amb els llenguatges de programació en entorn servidor. <br/> g) S'han reconegut i avaluat les eines de programació en entorn servidor. <br/> |


Una arquitectura web defineix l'estructura i el comportament dels components d'una aplicació web, incloent com es comuniquen entre ells i amb els usuaris finals. Aquesta arquitectura pot abastar des de la interfície d'usuari en el client fins als serveis de backend i bases de dades en el servidor.

Les arquitectures web són fonamentals en el desenvolupament d'aplicacions web modernes per diverses raons:

- **Escalabilitat**:Les arquitectures ben dissenyades permeten que les aplicacions web gestionin un nombre creixent d'usuaris i dades sense sacrificar el rendiment. Per exemple, una arquitectura de microserveis facilita l'escalabilitat horitzontal, ja que cada servei es pot escalar independentment.
- **Mantenibilitat**:Una bona arquitectura facilita el manteniment i l'actualització de les aplicacions. Mitjançant la separació de preocupacions (per exemple, en una arquitectura de tres capes), es poden fer canvis en una part del sistema sense afectar altres parts.
- **Seguretat**:Les arquitectures web poden incorporar diverses capes de seguretat per protegir les dades i les comunicacions. Això inclou mesures com l'autenticació, l'autorització, la xifratge de dades, i la protecció contra atacs comuns com les injeccions SQL i el cross-site scripting (XSS).
- **Rendiment**:L'arquitectura de l'aplicació web afecta directament el seu rendiment. Una arquitectura ben dissenyada optimitza el temps de resposta i la gestió de recursos, millorant l'experiència de l'usuari. L'ús de tècniques com la caché, el balanç de càrrega, i la compressió de contingut són exemples d'estratègies per millorar el rendiment.
- **Flexibilitat i Adaptabilitat**:Les arquitectures modernes permeten l'ús de diverses tecnologies i eines per a diferents parts del sistema, proporcionant flexibilitat i permetent una adaptació ràpida als canvis tecnològics. Això és especialment rellevant amb l'adopció de pràctiques DevOps i l'ús de contenidors i orquestradors com Docker i Kubernetes.
- **Col·laboració i Desplegament**:Un bon disseny arquitectònic facilita la col·laboració entre equips de desenvolupament, ja que clarifica les responsabilitats i els punts d'integració. També permet un desplegament més eficient i automatitzat, reduint els riscos d'errors i millorant el temps de lliurament.

## Tipus d'Arquitectures Web

A continuació, es descriuen alguns dels principals tipus d'arquitectures web, cadascun amb les seves pròpies característiques, avantatges i desavantatges:

### Arquitectura Client-Servidor
En aquest model, el client (generalment un navegador web) envia sol·licituds al servidor, que processa aquestes sol·licituds i envia les respostes corresponents.

**Diagrama:**

<figure>
  <img src="imagenes/01/clienteservidor.png" />
  <figcaption>Arquitectura Client Servidor</figcaption>
</figure>

**Característiques:**

- El client és responsable de la interfície d'usuari.
- El servidor maneja la lògica d'aplicació i l'accés a les dades.

**Avantatges:**

- Separació de responsabilitats.
- Facilita el manteniment i la seguretat.

**Desavantatges:**

- Pot tenir problemes de rendiment amb moltes sol·licituds simultànies.


### Arquitectura de Tres Capes
Aquesta arquitectura divideix l'aplicació en tres nivells: la capa de presentació, la capa de lògica d'aplicació, i la capa de dades.

**Diagrama:**

<figure>
  <img src="imagenes/01/model3capes.png" />
  <figcaption>Arquitectura 3 capes</figcaption>
</figure>


**Característiques:**

- La capa de presentació gestiona la interfície d'usuari.
- La capa de lògica d'aplicació processa les dades i executa la lògica de negoci.
- La capa de dades emmagatzema i recupera la informació.

**Avantatges:**

- Facilita l'escalabilitat.
- Millora la seguretat, ja que les dades no són directament accessibles des del client.

**Desavantatges:**

- Pot ser més complexa de desenvolupar i mantenir.

### Arquitectura de Microserveis
Els microserveis descomponen una aplicació en una sèrie de serveis petits i independents, cadascun executant una funció específica.

**Diagrama:**

<figure>
  <img src="imagenes/01/microserveis.png" />
  <figcaption>Arquitectura Microserveis</figcaption>
</figure>


**Característiques:**

- Cada microservei es pot desplegar, actualitzar, i escalar independentment.
- Utilitzen protocols lleugers com HTTP/REST o gRPC per comunicar-se.

**Avantatges:**

- Millora l'escalabilitat i la flexibilitat.
- Facilita l'ús de diferents tecnologies per a diferents serveis.

**Desavantatges:**

- Pot ser complexa de gestionar i coordinar.
- Requereix una infraestructura de desplegament i monitorització més robusta.

## Recursos Addicionals
- **Documentació sobre Arquitectures de Software:** [Software Architecture Guide](https://martinfowler.com/architecture/)
- **Tutorial de Microserveis:** [Microservices Tutorial](https://www.tutorialspoint.com/microservice_architecture/index.htm)

## Resum
Les arquitectures web són fonamentals per al desenvolupament d'aplicacions eficients i escalables. La selecció de l'arquitectura adequada depèn de les necessitats específiques del projecte, incloent-hi consideracions de rendiment, escalabilitat, seguretat i mantenibilitat.


## 2. Pàgines Web Estàtiques vs. Dinàmiques

Les pàgines web estàtiques són aquelles en què el contingut no canvia en funció de les accions de l'usuari. Estan construïdes amb HTML i CSS, i cada pàgina es carrega de manera independent des del servidor.

### Avantatges
- **Senzillesa:** Fàcils de crear i mantenir.
- **Rendiment:** Temps de càrrega ràpid perquè no requereixen processament addicional.
- **Seguretat:** Menys vulnerabilitats, ja que no hi ha lògica de servidor ni bases de dades.

### Desavantatges
- **Flexibilitat:** Difícils de modificar a gran escala sense eines automatitzades.
- **Interactivitat:** Limitada, ja que no poden respondre a les accions de l'usuari de manera dinàmica.

Exemple Pràctic

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pàgina Estàtica</title>
    <style>
        body { font-family: Arial, sans-serif; }
        .content { margin: 20px; }
    </style>
</head>
<body>
<div class="content">
    <h1>Benvingut!</h1>
    <p>Aquesta és una pàgina web estàtica.</p>
</div>
</body>
</html>
```

Les pàgines web dinàmiques són aquelles en què el contingut pot canviar en funció de les accions de l'usuari o altres factors. Utilitzen HTML, CSS, i JavaScript per al costat del client, i poden utilitzar llenguatges de servidor com PHP, Python, Node.js, entre altres, per generar contingut dinàmicament.

### Avantatges
- **Interactivitat:** Poden respondre a les accions de l'usuari i proporcionar una experiència més rica.
- **Personalització:** El contingut es pot adaptar en funció de les necessitats de l'usuari.
- **Actualització:** El contingut es pot actualitzar fàcilment sense canviar la pàgina completa.

### Desavantatges
- **Complexitat:** Més difícils de crear i mantenir, ja que requereixen programació tant al client com al servidor.
- **Rendiment:** Poden ser més lentes a causa de la necessitat de processament al servidor.
- **Seguretat:** Exposades a més vulnerabilitats, com injeccions SQL, si no es prenen les precaucions adequades.

Exemple Pràctic (PHP)

```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pàgina Dinàmica</title>
    <style>
        body { font-family: Arial, sans-serif; }
        .content { margin: 20px; }
    </style>
</head>
<body>
    <div class="content">
        <h1>Benvingut!</h1>
        <p>Aquesta pàgina ha estat generada a les <?php echo date('H:i:s'); ?>.</p>
    </div>
</body>
</html>
```
### Comparativa entre Pàgines Web Estàtiques i Dinàmiques
| Característica              | Pàgines Web Estàtiques             | Pàgines Web Dinàmiques               |
|-----------------------------|------------------------------------|--------------------------------------|
| **Contingut**               | Fix, no canvia                     | Variable, pot canviar                |
| **Complexitat**             | Baixa                              | Alta                                 |
| **Interactivitat**          | Limitada                           | Alta                                 |
| **Rendiment**               | Alt                                | Pot ser baix                         |
| **Seguretat**               | Alta                               | Depèn de la implementació            |
| **Flexibilitat**            | Baixa                              | Alta                                 |
| **SEO**                     | Bona                               | Depèn de la implementació            |
| **Temps de Desenvolupament**| Curt                               | Llarg                                |
| **Actualització del Contingut** | Manual                         | Automàtica                           |
| **Cost de Manteniment**     | Baix                               | Alt                                  |

### Avantatges de la Generació Dinàmica de Pàgines
- **Actualització en Temps Real:** Les pàgines dinàmiques poden mostrar contingut actualitzat en temps real, com notícies o resultats esportius.
- **Personalització:** Permet personalitzar el contingut per a cada usuari basat en les seves preferències i dades.
- **Interactivitat:** Les pàgines dinàmiques poden respondre a les accions dels usuaris, millorant l'experiència de l'usuari.


<figure>
  <img src="imagenes/01/paginadinamica.png" />
  <figcaption>Pàgina web dinàmica</figcaption>
</figure>

#### Recursos Addicionals
- **Documentació de HTML:** [MDN HTML Guide](https://developer.mozilla.org/en-US/docs/Web/HTML)
- **Documentació de CSS:** [MDN CSS Guide](https://developer.mozilla.org/en-US/docs/Web/CSS)
- **Documentació de PHP:** [PHP Documentation](https://www.php.net/docs.php)
- **Documentació de JavaScript (MDN):** [MDN JavaScript Guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide)
- **Documentació de Node.js:** [Node.js Documentation](https://nodejs.org/en/docs/)
- **Documentació de React:** [React Documentation](https://reactjs.org/docs/getting-started.html)

#### Resum
Les pàgines web estàtiques són adequades per a llocs web senzills amb contingut fix, mentre que les pàgines web dinàmiques són necessàries per a aplicacions més complexes que requereixen interactivitat i contingut variable. La decisió entre utilitzar una pàgina estàtica o dinàmica dependrà de les necessitats específiques del projecte i dels recursos disponibles. Les SPA ofereixen una experiència d'usuari molt rica però poden tenir desavantatges en termes de SEO i temps de càrrega inicial.

## 3. Models d'Execució de Codi en el Client i en el Servidor

Els models d'execució de codi en el desenvolupament web es poden dividir principalment en dos tipus: execució al client i execució al servidor. Cada model té les seves pròpies característiques, avantatges i desavantatges que cal considerar a l'hora de dissenyar una aplicació web.


### Execució de Codi al Client (FrontEnd)

L'execució de codi al client es realitza al navegador web de l'usuari. Els llenguatges utilitzats principalment per a l'execució al client són HTML, CSS i JavaScript.

#### Avantatges
- **Interactivitat:** Permet la creació d'experiències d'usuari riques i interactives.
- **Reducció de la càrrega del servidor:** El processament es fa al dispositiu de l'usuari, disminuint la càrrega del servidor.
- **Actualització instantània:** Canvis en l'UI poden ser reflectits immediatament sense necessitat de recarregar la pàgina.

#### Desavantatges
- **Seguretat:** El codi del client és visible i modificable pels usuaris, la qual cosa pot representar un risc de seguretat.
- **Compatibilitat:** Pot haver-hi diferències en la manera com diferents navegadors interpreten el codi.

Exemple de codi

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Exemple Client</title>
    <style>
        body { font-family: Arial, sans-serif; }
        .content { margin: 20px; }
    </style>
</head>
<body>
    <div class="content">
        <h1>Hola, món!</h1>
        <button onclick="mostrarMissatge()">Fes clic aquí</button>
        <p id="missatge"></p>
    </div>

    <script>
        function mostrarMissatge() {
            document.getElementById('missatge').innerText = 'Has fet clic al botó!';
        }
    </script>
</body>
</html>
```

### Execució de Codi al Servidor

L'execució de codi al servidor es realitza al servidor web abans que els resultats es retornin al navegador del client. Els llenguatges habituals inclouen PHP, Python, Ruby, Node.js, entre altres.

#### Avantatges
- **Seguretat:** El codi del servidor no és accessible pels usuaris finals, la qual cosa augmenta la seguretat.
- **Potència:** Els servidors solen ser més potents que els dispositius dels usuaris, permetent processar operacions més complexes.

#### Desavantatges
- **Latència:** Les sol·licituds al servidor poden ser lentes a causa de la distància física i la càrrega del servidor.
- **Escalabilitat:** Pot ser necessari més esforç per escalar una aplicació a mesura que augmenta el nombre d'usuaris.    

Exemple de codi
``` node.js
// server.js
const http = require('http');

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
res.statusCode = 200;
res.setHeader('Content-Type', 'text/plain');
res.end('Hola, món!\n');
});

server.listen(port, hostname, () => {
console.log(`El servidor s'està executant a http://${hostname}:${port}/`);
});
```

### Single Page Application (SPA)

Una Single Page Application (SPA) és un tipus d'aplicació web que carrega una única pàgina HTML i dinàmicament actualitza el contingut a mesura que l'usuari interactua amb l'aplicació, utilitzant JavaScript per a gestionar la lògica i les actualitzacions de la interfície d'usuari.

#### Avantatges
- **Experiència d'usuari millorada:** Les SPA ofereixen una navegació més ràpida i fluida, similar a una aplicació d'escriptori.
- **Menys càrrega del servidor:** Menys sol·licituds al servidor ja que només es carrega una pàgina inicialment.
- **Desenvolupament modular:** Facilita la creació de components reutilitzables.

#### Desavantatges
- **SEO:** Les SPA poden ser menys amigables amb els motors de cerca.
- **Carregada inicial:** Pot requerir una major càrrega inicial de recursos, afectant el temps de càrrega inicial.
- **Gestió de l'estat complexa:** Pot ser més complicat gestionar l'estat de l'aplicació.

Exemple Pràctic (React)

```jsx
// index.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Exemple SPA</title>
    <script defer src="bundle.js"></script>
</head>
<body>
    <div id="root"></div>
</body>
</html>

// index.js
import React, { useState } from 'react';
import ReactDOM from 'react-dom';

function App() {
    const [message, setMessage] = useState('');

    const handleClick = () => {
        setMessage('Has fet clic al botó!');
    };

    return (
        <div>
            <h1>Hola, món!</h1>
            <button onClick={handleClick}>Fes clic aquí</button>
            <p>{message}</p>
        </div>
    );
}

ReactDOM.render(<App />, document.getElementById('root'));
```

#### Comparativa entre Execució de Codi al Client,al Servidor i el SPA


| Característica              | Execució al Client                 | Execució al Servidor                 | Single Page Application (SPA)        |
|-----------------------------|------------------------------------|--------------------------------------|--------------------------------------|
| **Interactivitat**          | Alta                               | Mitjana                              | Molt Alta                            |
| **Seguretat**               | Baixa                              | Alta                                 | Mitjana                              |
| **Carrega del servidor**    | Baixa                              | Alta                                 | Baixa                                |
| **Latència**                | Baixa                              | Pot ser alta                         | Baixa (després de la càrrega inicial)|
| **Accés a recursos locals** | Limitat al navegador               | Complet accés al sistema del servidor| Limitat al navegador                 |
| **SEO**                     | Mitjana                            | Alta                                 | Baixa                                |
| **Temps de càrrega inicial**| Ràpid                              | Depèn de la complexitat              | Pot ser lent                         |



#### Comparativa entre desenvolupadors

| Perfil                   | Ferramenta          | Tecnologia
| ---                       |---------------------| ---
| *Front-end* / client     | Navegador Web       | HTML + CSS + JavaScript
| *Back-end* / servidor    | Servidor Web + BBDD | PHP, Python, Ruby, Java / JSP, .Net / .asp



!!! tip "Perfil *Full-stack*"
    En les ofertes de treball quan fan referència a un **Full-stack developer**, estan buscant un perfil que domina tant el **front-end** com el **back-end**.

#### Models d'Execució de Codi
- **Model Client-Side:** El codi s'executa en el navegador del client, normalment utilitzant JavaScript. Exemple: Un formulari que valida les dades d'entrada abans de ser enviat.
- **Model Server-Side:** El codi s'executa en el servidor, com ara PHP, Python o Node.js, i el servidor envia les pàgines generades al navegador del client. Exemple: Una pàgina que mostra els resultats d'una consulta a la base de dades.


#### Recursos addicionals

- **Documentació de JavaScript (MDN):** [MDN JavaScript Guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide)
- **Guia de Node.js:** [Node.js Documentation](https://nodejs.org/en/docs/)
- **Documentació de React:** [React Documentation](https://reactjs.org/docs/getting-started.html)


#### Resum
La decisió sobre si utilitzar l'execució de codi al client, al servidor o una SPA depèn de les necessitats específiques de l'aplicació i els recursos disponibles. Comprendre les diferències clau i els avantatges de cada model ajudarà a prendre decisions informades i a desenvolupar aplicacions web eficients i segures.

## 4. Mecanismes d'Execució de Codi en Servidors Web

### Interpreted Languages: PHP, Python

  El codi es processa línia per línia en temps real, permetent una major flexibilitat durant el desenvolupament, ja que els canvis poden ser implementats i testats immediatament sense necessitat de recompilar tot el projecte.

  ```php
      <html>
      <body>
          <h1><?php echo "Hola, món!"; ?></h1>
      </body>
      </html>
  ```
  
### Compiled Languages: Java

  El codi es compila abans de ser executat, el que significa que és transformat en un format executable per la màquina abans de la seva execució. Això sol millorar el rendiment, ja que el codi compilat s'executa més ràpidament que el codi interpretat.

  ```java
    // Exemple simplificat d'un servlet Java
    import java.io.*;
    import javax.servlet.*;
    import javax.servlet.http.*;
    
    public class HelloWorldServlet extends HttpServlet {
    public void doGet(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
        response.setContentType("text/html");
        PrintWriter out = response.getWriter();
        out.println("<h1>Hola, món!</h1>");
        }
    }
  ```
### Middleware: Node.js

  Permet la programació asíncrona i escalable amb JavaScript, oferint la capacitat de gestionar moltes connexions simultànies de manera eficient. Això és especialment útil per a aplicacions que necessiten alta concurrència, com aplicacions en temps real.

```javascript
    const express = require('express');
    const app = express();
    
    app.get('/', (req, res) => {
    res.send('Hola, món!');
    });
    
    app.listen(3000, () => {
    console.log('Servidor escoltant a http://localhost:3000');
});
```

## Servidors Web

Un servidor web és un programa que serveix contingut web estàtic com HTML, CSS, JavaScript, imatges i altres fitxers als clients a través del protocol HTTP o HTTPS. El servidor web gestiona les sol·licituds entrants dels clients (navegadors web) i retorna les respostes adequades.

### Principals Funcionalitats dels Servidors Web

#### Servei de Contingut Estàtic
- **Descripció:** Proporciona fitxers estàtics com HTML, CSS, JavaScript, imatges i altres recursos directament als clients.
- **Exemple:** Quan un usuari sol·licita una pàgina HTML, el servidor web envia el fitxer HTML corresponent al navegador de l'usuari.

#### Gestió de Peticions HTTP
- **Descripció:** Maneja sol·licituds HTTP de clients, com GET, POST, PUT, DELETE, i retorna les respostes adequades amb els codis d'estat corresponents.
- **Exemple:** Un servidor web processa una sol·licitud GET per una pàgina web i retorna el contingut de la pàgina amb un codi d'estat 200 (OK).

#### Redirecció i Reescriptura d'URLs
- **Descripció:** Permet la redirecció de peticions a diferents URLs i la reescriptura d'URLs per millorar l'accessibilitat i la SEO.
- **Exemple:** Reescriptura d'URLs amigables per als usuaris, com convertir `example.com/page?id=123` a `example.com/page/123`.

#### Suport per a HTTPS
- **Descripció:** Proporciona connexions segures utilitzant el protocol HTTPS, que xifra les dades entre el client i el servidor.
- **Exemple:** Un servidor web configurat amb un certificat SSL/TLS que permet connexions segures a través de HTTPS.

### Exemples de Servidors Web

#### Apache HTTP Server
- **Descripció:** Un servidor web de codi obert molt utilitzat, conegut per la seva flexibilitat i extensibilitat.
- **Funcionalitats:** Suport per a mòduls que afegeixen funcionalitats com l'autenticació, la reescriptura d'URLs i la compressió de contingut.

#### Nginx
- **Descripció:** Un servidor web i servidor intermediari de codi obert, dissenyat per gestionar moltes connexions simultànies amb un ús eficient dels recursos.
- **Funcionalitats:** Actua com a servidor proxy invers, equilibrador de càrrega i servidor de fitxers estàtics.

#### Microsoft Internet Information Services (IIS)
- **Descripció:** Un servidor web i d'aplicacions de Microsoft per a plataformes Windows.
- **Funcionalitats:** Suport per a aplicacions ASP.NET, autenticació integrada i eines de gestió robustes.



## 6. Funcionalitats dels Servidors d'Aplicacions

Un servidor d'aplicacions és un tipus de servidor dissenyat per executar aplicacions web dinàmiques i gestionar la lògica de negoci d'una aplicació. Aquest servidor actua com una capa intermèdia entre el client (navegador web) i les bases de dades o altres serveis de backend, proporcionant un entorn d'execució per a aplicacions web.

### Principals Funcionalitats dels Servidors d'Aplicacions

#### Gestió de Sessions
- **Descripció:** Manteniment de l'estat de l'usuari durant la seva interacció amb l'aplicació.
- **Exemple:** Sessions PHP que emmagatzemen informació de l'usuari.

#### Concurrència
- **Descripció:** Capacitat per gestionar múltiples peticions simultànies de manera eficient.
- **Exemple:** Node.js gestiona peticions de manera asíncrona.

#### Seguretat
- **Descripció:** Autenticació i autorització dels usuaris per accedir a diferents parts de l'aplicació.
- **Exemple:** Utilització de JWT (JSON Web Tokens) per autenticar usuaris en una aplicació Node.js.

### Relació entre Servidors Web i Servidors d'Aplicacions

#### Integració i Col·laboració
Els servidors web treballen conjuntament amb els servidors d'aplicacions per gestionar les sol·licituds de manera eficient. Mentre que el servidor web maneja les sol·licituds HTTP i serveix contingut estàtic, el servidor d'aplicacions processa la lògica de negoci i genera contingut dinàmic.

#### Exemple de Configuració
- **Servidor Web (Nginx):** Actua com a proxy invers, encaminant les sol·licituds dinàmiques al servidor d'aplicacions.
- **Servidor d'Aplicacions (Node.js):** Gestiona les sol·licituds dinàmiques, executa la lògica de negoci i retorna les respostes al servidor web.

Aquesta col·laboració permet una gestió eficient de les sol·licituds i una millor distribució de la càrrega, millorant el rendiment i l'escalabilitat de les aplicacions web.

### Exemples de Servidors d'Aplicacions

#### Apache Tomcat
- **Descripció:** Un servidor d'aplicacions de codi obert per a aplicacions web Java.
- **Funcionalitats:** Suporta servlets Java i JavaServer Pages (JSP), facilitant l'execució d'aplicacions Java.

#### Microsoft Internet Information Services (IIS)
- **Descripció:** Un servidor web i d'aplicacions de Microsoft per a plataformes Windows.
- **Funcionalitats:** Suporta aplicacions ASP.NET, autenticació integrada, i eines de gestió robustes.

#### JBoss EAP (Enterprise Application Platform)
- **Descripció:** Un servidor d'aplicacions Java EE de codi obert desenvolupat per Red Hat.
- **Funcionalitats:** Proporciona un entorn robust per a la implementació d'aplicacions empresarials amb suport per a diversos frameworks Java.

#### Node.js
- **Descripció:** Una plataforma per a l'execució de codi JavaScript en el servidor.
- **Funcionalitats:** Permet la programació asíncrona, ideal per a aplicacions en temps real i escalables com xats i jocs multijugador.

## 7. Llenguatges i Tecnologies de Programació Web en Entorn Servidor

## PHP
- **Descripció:** Popular per la seva facilitat d'ús i integració amb MySQL.
- **Exemple:** Utilització de PHP per crear pàgines dinàmiques i accedir a bases de dades MySQL.

## Node.js
- **Descripció:** Utilitza JavaScript en el servidor, permetent una programació asíncrona i escalable.
- **Exemple:** Aplicacions web en temps real utilitzant Socket.io.

## Python (Django/Flask)
- **Descripció:** Conegut per la seva sintaxi clara i biblioteques extensives.
- **Exemple:** Desenvolupament d'aplicacions web amb Django, utilitzant el seu ORM per accedir a bases de dades.



## 4. MVC

![MVC](imagenes/01/mvc.png){align=right & width=500}

*Model-View-Controller* o Model-Vista-Controlador és un model d'arquitectura que separa les dades i la lògica de negoci respecte a la interfície d'usuari i el component encarregat de gestionar els esdeveniments i les comunicacions.

En separar els components en elements conceptuals permet reutilitzar el codi i millorar la seua organització i manteniment. Els seus elements són:

* Model: representa la informació i gestiona tots els accessos a aquesta, tant consultes com actualitzacions provinents, normalment, d'una base de dades. S'accedeix via el controlador.
* Controlador: Respon a les accions de l'usuari, i realitza peticions al model per a sol·licitar informació. Després de rebre la resposta del model, li envia les dades a la vista.
* Vista: Presenta a l'usuari de manera visual el model i les dades preparades pel controlador. L'usuari interactua amb la vista i realitza noves peticions al controlador.

L'estudiarem en més detall en aprofundir en l'ús dels **frameworks PHP**.

## Decisions de disseny

* Quina grandària té el projecte?
* Quins llenguatges de programació conec? Val la pena l'esforç d'aprendre un nou?
* Usaré eines de codi obert o eines propietàries? Quin és el cost d'utilitzar solucions comercials?
* Programaré l'aplicació jo només o formaré part d'un grup de programadors?
* Conte amb algun servidor web o gestor de base de dades disponible o puc decidir lliurement utilitzar el que crega necessari?
* Quin tipus de llicència aplicaré a l'aplicació que desenvolupe?

## Ferramentes

### Servidor Web

Programari que rep peticions HTTP (GET, POST, DELETE, ...). Retorna el recurs sol·licitat (HTML, CSS, JS, JSON, imatges, etc...)

El producte més implantant és **Apatxe Web Server** (<https://httpd.apache.org/>), creat en 1995.

* Programari lliure i multiplataforma
* Sistema de mòduls dinàmics → PHP, Python, Perl
* Utilitza l'arxiu `.*htaccess` per a la seua configuració

En l'actualitat, Apatxe està perdent mercat respecte a **Nginx** (<https://www.nginx.com>). Es tracta d'un producte més modern (2004) i que en determinats escenaris té millor rendiment que Apatxe.

* Comparativa servidors web: <https://w3techs.com/technologies/history_overview/web_server/ms/q>

### Servidor d'Aplicacions

* Programari que ofereix serveis addicionals als d'un servidor web:
  * Clustering
  * Balanceig de càrrega
  * Tolerància a fallades
  * **Tomcat** (<http://tomcat.apache.org/>) és el servidor d'aplicacions **open source** i multiplataforma de referència per a una arquitectura Java.
  * Contén un contenidor Web Java que interpreta **Servlets** i **JSP**.

!!! info
    Tant els servidors web com els servidors d'aplicacions s'estudien en el mòdul de "Desplegament d'Aplicacions Web".

### Llenguatges en el servidor

Les aplicacions que generen les pàgines web es programen en algun dels següents llenguatges:

* PHP: El més estés. Normalment s'executa com un mòdul al servidor. Es fàcil i barat trobar allotjaments que l'oferisquen.
* JSP: La versió de Java per a la web. Li cal un contenidor web.
* ASP.NET: Integrada en la plataforma de microsoft .NET
* Ruby: Molt apreciat per els desenvolupadors web.
* GO: La versió de google de phyton.
* Phyton: El més popular.
* NodeJS: Utilitza Javascript.

[Comparació de llenguatges](https://www.codementor.io/@iliawebdev/top-programming-languages-for-web-development-in-2021-1hzczfuoei)

[Criteris per apendre un llenguatge de programació](https://blog.educacionit.com/2018/04/10/4-criterios-para-elegir-tu-primer-lenguaje-de-programacion/)

#### JavaEE

**Java Enterprise Edition** és la solució Java per al desenvolupament d'aplicacions *enterprise*. Ofereix una arquitectura molt completa i complexa, escalable i tolerant a fallades. Plantejada per a aplicacions per a grans sistemes.

![JavaEE](imagenes/01/javaee.png)

#### PHP

* Llenguatge de propòsit general dissenyat per al desenvolupament de pàgines web dinàmiques
* Al principi, llenguatge no tipat.
* Actualment en la versió 8. Es recomana almenys utilitzar una versió superior a la 7.0.
* Codi embegut en l'HTML
* Instruccions entre etiquetes `<?php` y `?>`
* Multitud de llibreries i frameworks:
  
      * Laravel, Symfony, Codeigniter, Zend

La seua documentació és bastant completa: <https://www.php.net/manual/es/index.php>

El següent mapa mental mostra un resum dels seus elements:

<figure>
  <img src="imagenes/01/php.jpg" />
  <figcaption>Elements del llenguatge PHP</figcaption>
</figure>

Durant les següents unitats estudiarem PHP en profunditat.

## Posada en funcionament

Pera fer correr les aplicacions de servidor ens cal, com a mínim, un **servidor web**, l'interpret de **php** i un **motor de base de dades**. Hem de distinguir l'**entorn de desenvolupament**, on anem a programar i mantindre la nostra aplicació, de l'**entorn de producció**, on anem a executar-la.
Normalment el primer depén de nosaltres mentre que el segon pot dependre de l'empresa on s'allotjarà la nostra web. Per a preparar el nostre entorn de desenvolupament podem optar per:

* Qualsevol solució **LAMP** (Linux, Apache, Mysql, PHP). Als que haurem d'afegir, una vegada els projectes es facen grans **composer, git i les opcions de la part de client**.
* Una màquina virtual ja configurada.
* Una solució docker.

La primera solució és senzilla d'implementar però no hauria de ser la nostra primera opció per:

* Estem possant en funcionament en la nostra màquina una sèrie de serveis que normalment no fariem, baixant el rendiment de la màquina i obrint vulnerabilitats.
* Si treballem en grup, les instal·lacions i el funcionament no són iguals, depenen del sistema operatiu que té instal·lat cadascú. Allò que li funciona a ú  pot ser no li funciona a un altre. Això és inevitable quan el projecte es complica i es perd molt de temps.
* Passa el mateix quan passem a l'entorn de producció.

La segona solució soluciona els dos primers problemes, doncs tots els desenvolupadors poden tindre virtualitzada, la mateixa màquina. Encara que si la màquina no la fem nosaltres sinó que utilitzem alguna ja configurada (**vagrant**) o si ens cal instal·lar alguna cosa més, ho hauria de fer tot l'equip.

Així i tot, tindriem les següents desaventatges:

* A l'instal·lar una maquina virtual sencera ocupa recursos del sistema.
* La màquina instal·la més coses de les necessàries habitualment.
* No reprodueix l'entorn de producció.

Pot ser molt útil, per exemple, quan la fem servir per desenvolupar en un framework, que ja ve configurat per fer-lo funcionar inmediatament i amb totes les característiques instal·lades.

La tercera opció té les següents característiques:

* Al principi és més difícil de possar en funcionamet ja que calen coneixements de docker.
* Tots els desenvolupadors comparteixen entorn encara que utilitzen màquines o sistemes operatius diferents.
* Si hi ha algun canvi de configuració de l'entorn és fácilment transladable a tots els desenvolupadors.
* Es poden crear tants entorns  de desenvolupament com projectes diferents hi hajen.
* Els contenidors ocupen pocs recursos.
* Els projectes es poden possar en producció utilitzan una solució docker de manera inmediata.

### XAMPP

XAMPP (https://www.apachefriends.org/es/index.html) és una distribució composta amb el programari necessari per a desenvolupar en entorn servidor. Es compon de les següents eines sobre la base de les seues sigles:

* X per al sistema operatiu (d'aquí ve que es conega altrament com LAMP o WAMP).
* A per a Apatxe.
* M per a MySQL / MariaDB. També inclou phpMyAdmin per a l'administració de la base de dades des d'una interfície web.
* P per a PHP.
* l'última P per a Perl.

Des de la pròpia pàgina es pot descarregar l'arxiu executable per al sistema operatiu del nostre ordinador. Es recomana llegir la FAQ de cada sistema operatiu amb instruccions per a la seua posada en marxa.

!!! note "XAMPP en Windows"
    Si treballes amb el teu propi ordinador, XAMPP és una solució més senzilla que Docker, sobretot si treballes amb Windows com a sistema operatiu.

### Docker

Docker (<https://www.docker.com>) és un gestor de contenidors, considerant un contenidor com un mètode de virtualització del sistema operatiu.

L'ús de contenidors requereix menys recursos que una màquina virtual, per tant, el seu llançament i detenció són més ràpids que les màquines virtuals.

Així doncs, *Docker* permet crear, provar i implementar aplicacions ràpidament, a partir d'una sèrie de plantilles que es coneixen com a **imatges** de *Docker*.

Per a això és necessari tindre instal·lat **Docker Desktop** (<https://www.docker.com/products/docker-desktop>) en els nostres entorns de desenvolupament (el qual ja inclou en **nucli** de *Docker* i l'eina **docker compose**). Per a instal·lar-ho en Windows, és necessari instal·lar prèviament **WSL 2**, el qual és un subsistema de *Linux* dins de *Windows*.

Al llarg del curs anirem creant diferents contenidors amb els serveis necessaris, de manera que cada vegada només treballem amb el programari mínim.

!!! caution "Versions"
    Al llarg del curs usarem PHP `8.1`. Respecte a *Docker*, per a escriure les anotacions hem utilitzat la versio `20.10` i la versio `2.19` de **docker compose**. Finalment, la versió de *Docker Desktop* que hem utilitzat és la `4.0`.

#### Instal·lació de docker


La instal·lació de docker dependrà del sistema operatiu que estem utilitzant. Ací anem a vore la que efecturan els que utilitzen linux, amb el sistema operatiu linux-mint o ubuntu , que és el que ve instal·lat en les imatges suministrades. Per a mac o windows s'haurà de mirar la pàgina web de [docker](https://www.docker.com/get-started)

Ens donem privilegis

~~~
sudo su
~~~

Utilitzant els repositoris de docker l'instal·lem:

~~~
echo "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable" | tee /etc/apt/sources.list.d/docker.list

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -

apt update

apt install docker-ce docker-ce-cli containerd.io pigz
~~~

Donem permisos a l'usuari afegint-lo al grup de docker

~~~
usermod -aG docker $USER
~~~
On $USER és el teu usuari.

També haurem d'instal·lar el docker-compose
~~~
curl -SL "https://github.com/docker/compose/releases/download/v2.10.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

chmod +x /usr/local/bin/docker-compose
~~~

I provem

~~~
docker --version
~~~

Faltarà engegar el servei de docker per a poder executar contenidors

~~~
sudo systemctl start docker.service
~~~

#### Plantilla Servidor Web + PHP

**Docker** es basa en l'ús d'imatges per a crear contenidors. *Docker Compose* simplifica el treball amb múltiples contenidors, i per això, per a facilitar l'arranc, ens centrarem en *Docker Compose* utilitzant una plantilla que únicament contindrà com a serveis Nginx i PHP.
Per a facilitar la posada en marxa, us facilite un repositori en [github classroom](#GitHub-Classroom) [Nginx/PHP](https://classroom.github.com/a/hrZehkpi) disponible per a la seua descàrrega. **L'haureu de possar en un directori fàcilment localitzable i amb un nom significatiu, ja que serà el vostre directori de treball**.

Dins d'este repositori, el fitxer **'docker-compose.yaml'** indica quines màquines ha de montar i té el següent aspecte

=== "Nginx i PHP"

    ``` yaml
    # Services
    services:

    # Nginx Service
    nginx:
    image: nginx:1.19
    ports:
      - 80:80
    volumes:
      - ./src:/var/www/php
      - ./.docker/nginx/conf.d:/etc/nginx/conf.d
    depends_on:
      - php

    # PHP Service
    php: 
    build: ./.docker/php/
    working_dir: /var/www/php
    expose:
      - 9000
    volumes:
      - ./src:/var/www/php
      - ./.docker/php/conf.d/Xdebug.ini:/usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
      - ./.docker/php/conf.d/error_reporting.ini:/usr/local/etc/php/conf.d/error_reporting.ini

    # Más info en
    # https://tech.osteel.med/posts/docker-for-local-web-development-part-1-a-basic-lemp-stack

    # Lanzar con
    # docker-compose up -d

    # Ver los logs con
    # docker-compose logs -f
    
    ```
Per arrencar les màquines o podem fer des de la consola amb

``` console
docker compose up -d
```

Si volem accedir a un terminal interactiu dins del contenidor:

``` console
docker exec -it nombreContenedor bash
```

Altres comandos que podem arribar a utilitzar són:

* `docker ps`: Veure els contenidors que es estan executant
* `docker ps -a`: Veure tots els contenidors
* `docker start nombreContenedor`: Arrancar un contenidor
* `docker images`: Veure les imatges que tenim descarregades

Una altra forma més senzilla per a llançar de nou els contenidors i gestionar-los una vegada creats és utilitzar la interfície gràfica que ofereix Docker Desktop:

<figure>
  <img src="imagenes/01/dockerdesktop.png" />
  <figcaption>Arranc de contenidor mitjançant Docker Desktop</figcaption>
</figure>

!!! tip "Docker stack"
    Existeixen diverses opcions mitjançant Docker que ofereixen solucions completes i empaquetes per a tot el stack de desenvolupament. En posteriors sessions utilitzarem tant *Devilbox* (<http://devilbox.org>) com *Laradock* (<https://laradock.io>)

!!! question "Però vull saver com funciona..."
    En el mòdul de Desplegament d'aplicacions estudiareu en profunditat, a més de Docker, Apatxe i altres serveis que ens serviran d'ajuda per al desenvolupament en entorn servidor.

### Tot funciona

Heu de comprovar que a l'accedir a `http://localhost` en el vostre navegador se us obre una pàgina de salutació.


### Entorn de desenvolupament

En este curso utilitzarem [**PHP Storm**](<https://www.jetbrains.com/phpstorm/>) com a entorn de desenvolupament. Existixen altres alternatives, com [**Visual Studio Code**](<https://code.visualstudio.com>).

#### Instal·lació
Podem fer-ho de manera automàtica utilitzant snap. Per fer-ho amb linux-mint

``` console
sudo rm /etc/apt/preferences.d/nosnap.pref
sudo apt update
sudo apt install snapd
sudo snap install phpstorm --classic
```
També es pot instal·lar baixant-se el paquet de la pàgina web.

##### Llicència
Podeu sol·licitar una llicència a i.gomismullor@edu.gva.es


### Entorn de proves

La màquina docker ve configurada amb **[codeception](https://codeception.com/)** i una col·leció de proves per als exercicis que desenvoluparem al llarg de les primeres unitats.
S'ha creat un shell per executar totes les proves

``` console
sh test.sh
```
### GitHub Classroom

Us podeu [registrar](https://classroom.github.com/)

**Metodologia de treball amb el github classroom**

* Se proporcionarà a l'alumnat un enllaç amb la invitació.
* Accedint a l'enllaç a cada alumne se li crearà un repositori individual en l'organització.
* L'alumnat treballa en el seu repositori assignat. Se'l pot baixar per treballar en local.
* Inicialment, l'alumne crea una branca nova sobre la que va a treballar.
* Quan vullga sol.licitar ajuda o revisió del professor, l'alumne genera una pull request a la branca principal del seu repositori en la que cita al professor per tal que reba una notificació.
* El profesor proporciona retroalimentació mitjançant comentaris en la pull request o en un determinat commit individual.
* Opcionalment es poden utilitzar els issues y les cites d'usuari per sol·licitar la intervenció del profesor.
* Quan l'alumne finalitza la tasca, genera una últim pull request
* El profesor revisa la pull request i opcionalment fa comentaris.


## Referències

* Curs de introducció a Docker, per *Sergi García Barea* : <https://sergarb1.github.io/CursoIntroduccionADocker/>
* Article [Arquitectures Web i sa evolució](https://www.arquitecturajava.com/arquitecturas-web-y-su-evolucion/)

## Videos

* [Triar un llenguatge de programació](https://laracasts.com/series/php-for-beginners-2023-edition/episodes/1)

* [Instal.Lació entorn de desenvolupament](https://laracasts.com/series/php-for-beginners-2023-edition/episodes/2)
