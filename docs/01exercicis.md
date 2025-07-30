# Exercicis

### SA1 – Comparativa d’Arquitectures Web en Entorn Servidor (Grups de 3 persones) 

#### 🎯 Objectiu (RA1)
Reconéixer les arquitectures web més habituals en entorn servidor, identificant els seus components, característiques i escenaris d’ús.
 
+---------------------+   +----------------------+   +---------------------------+
|    Monolítica       |   |        MVC           |   |       Microserveis        |
+---------------------+   +----------------------+   +---------------------------+
| [ Client ]          |   | [ Client ]           |   | [ Client ]                |
|        |            |   |      |               |   |       |                  |
|     [Servidor]      |   |   [Servidor]         |   |   [API Gateway]           |
|  (Tot en un fitxer) |   | ┌──Controller──┐     |   |   ┌────┬────┐             |
|                     |   | │  Model        │     |   |   │User│Product│          |
|                     |   | │  View         │     |   |   │Srv │Srv    │          |
+---------------------+   +----------------------+   +---------------------------+


##### 1. Explora el següents repositoris

* [Arquitectura monolítica](https://github.com/Curs-2025-26/SA1.Arquitectura_monolitica)
* [Arquitectura MCV](https://github.com/Curs-2025-26/SA1.Arquitectura_MVC)
* [Arquitectura microserveis](https://github.com/Curs-2025-26/SA1.Arquitectura_microserveis)

##### 2. Fes un fork de cadascú d'ells

##### 3. Utilitza codespaces per generar un entorn de prova

##### 4. Envia peticions i prova l'arquitectura

##### 5. Completa la següent taula

  🧾 Fitxa comparativa d'arquitectures web

| Arquitectura      | Components visibles | Separació de responsabilitats | Avantatges | Inconvenients | Casos d’ús recomanats |
|------------------|---------------------|-------------------------------|------------|---------------|-----------------------|
| **Monolítica**    |                     |                               |            |               |                       |
| **MVC**           | `                   |                               |            |               |                       |
| **Microserveis**  |                     |                               |            |               |                       |


##### 6. Reflexió final

Tria un escenari (ex. botiga online, sistema de reserves...) i explica:

* Quina arquitectura faries servir?
* Per què és la més adequada en aquest cas?

#### ✅ Rúbrica d’avaluació – SA1: Arquitectures web

| Criteri                                                        | Puntuació màxima |
|----------------------------------------------------------------|------------------|
| Obri correctament el repositori a GitHub Codespaces            | 2 punts          |
| Identifica i descriu components bàsics de l'arquitectura       | 3 punts          |
| Relaciona cada projecte amb els conceptes teòrics corresponents| 3 punts          |
| Reflexiona i compara arquitectures segons escenari proposat    | 2 punts          |
| **Puntuació total**                                            | **10 punts**     |

