# Projecte Integrador Bloc 1.

??? abstract "Duració i criteris d'avaluació"

    Duració estimada: 16 hores

    <hr />

    | Resultat d'aprenentatge | Criteris d'avaluació |
    | --------                | --------             |
    | 3. Escriu blocs de sentències embeguts en llenguatges de marques, seleccionant i utilitzant les estructures de programació.| |
    | 4. Desenvolupa aplicacions web embegudes en llenguatges de marques analitzant i incorporant funcionalitats segons especificacions.| |
    | 5. Desenvolupa aplicacions web identificant i aplicant mecanismes per a separar el codi de presentació de la lògica de negoci.| |
    | 6. Desenvolupa aplicacions web d'accés a magatzems de dades, aplicant mesures per a mantindre la seguretat i la integritat de la informació| |



# Enunciat del Projecte: Backend de BatoiBooks

## Objectiu del Projecte

Desenvolupar el backend per a l’aplicació **BatoiBooks** en PHP, proporcionant:

- Autenticació per token JWT.
- Gestió completa de les dades de l'aplicació (operacions CRUD).
- Interfície d’administració amb funcionalitats avançades, com la generació de factures en PDF.

---

## Funcionalitats del Backend

### 1. BBDD

Crear la BBDD i les taules utilitzant el següent [sql](./recursos/sql/batoi_books.sql) 

### 2. Autenticació per al frontEnd

1. **Registre**: Endpoint per registrar nous usuaris. Rebrà dades com `email`, `nick` i `password`, i retornarà un token JWT per a la sessió de l’usuari.

2. **Login**: Endpoint per a l'inici de sessió, on es validarà `email` i `password`. En cas d'èxit, es generarà un token JWT amb la informació d'identificació de l'usuari.

3. **Validació de Token**: Cada controlador (excepte el de `login` i `register`) requerirà un token JWT vàlid per accedir a qualsevol dada, la qual cosa permetrà una gestió segura de la sessió.

---

### 3. Controladors d’Entitats (CRUD)

Es crearà un fitxer PHP específic per a cada entitat, que atendrà les operacions CRUD bàsiques. Les taules que es gestionaran són:

- **Books**
- **Users**
- **Modules**
- **Courses**

Per a cada taula es permetran operacions:

- **GET**: Per obtenir dades (llistat o element per ID).
- **POST**: Per inserir nous elements.
- **PUT**: Per modificar elements existents.
- **DELETE**: Per eliminar elements.

Cada operació validarà les dades abans de ser processades i respondrà amb els estats corresponents.

---

#### Exemples de peticions

* Tornar un llibre

```http     
GET /api/books.php?userId=2
``` 

* Tornar tots els llibres

```http 
GET /api/books.php
```

* Afegir un llibre

```http
POST /api/books.php
Contingut JSON: {
"userId": 2,
"moduleCode": "0011",
"publisher": "Apunts",
"price": 15.00,
"pages": 100,
"status": "new",
"photo": "ruta_foto.jpg",
"comments": "En bon estat"
}
```


### 4. Interfície d’Administrador

1. **Autenticació de l'usuari**: L'usuari s'autenticarà amb un usuari i es comprovarà que és l'administrador.
2. **Accés al CRUD de Mòduls i Cursos**: L’usuari administrador podrà gestionar completament les taules `modules` i `courses`.
3. **Generació de Factures en PDF**:
    - Permetre la selecció de dates i usuaris.
    - Calcular un 10% de l’import total de les vendes per generar la factura.
    - Incloure el logotip de l'aplicació, data de generació, import total i desglossament de vendes.

---

## Exigències Tècniques

- Utilitzar PHP com a llenguatge del servidor.
- Estructurar el projecte amb fitxers separats per a cada entitat dins de la carpeta `api/` i `backend`
- Utilitzar el format JSON per a la comunicació entre el client i el servidor.
- Garantir la seguretat en les peticions autenticades mitjançant el token JWT.
- Utilitzar en la mesura de lo possible el MVC en el backend i els control·ladors per a respondre a les peticions de l'API.
- Cal fer proves a un model o control·lador de l'aplicatiu.
- Cal guardar en un fitxer de log les peticions que es fan a l'api en forma de: Usuari, IP client i Mètode utilitzat.   
- Utilitzar exempcions per al maneig d'errors de l'usuari.
 
---

 