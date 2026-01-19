## SA 6 – Node.js + Express

Guia ràpida per introduir Node.js al backend, Express com a framework principal i una API REST persistent amb MongoDB.

### 🧠 Conceptes clau
- **Node.js**: JavaScript fora del navegador, motor V8, ideal per APIs.
- **Express**: capa mínima per definir rutes, middlewares i respostes JSON.
- **API REST**: recursos en plural, mètodes HTTP (`GET`, `POST`, `PUT`, `DELETE`, `PATCH`), codis d’estat correctes i respostes en `application/json`.
- **Estructura recomanada**:
  ```
  api-inventari/
  ├─ package.json        # "type": "module", scripts dev/start
  ├─ .env                # PORT, MONGO_URI, etc.
  └─ src/
     ├─ server.js        # arrencada + connexió a Mongo
     ├─ app.js           # Express, middlewares, rutes
     ├─ lib/db.js        # connexió mongoose
     ├─ routes/          # rutes per recurs
     ├─ controllers/     # lògica de negoci
     ├─ models/          # esquemes mongoose
     ├─ middlewares/     # 404, errors, validació...
     └─ validation/      # regles express-validator
  ```

### ⚙️ Projecte base amb MongoDB
En tres passos: inicialitza Node, instal·la dependències i crea l’esquelet mínim perquè Express servisca les rutes i es connecte a Mongo. Els fragments següents són “copiar i pegar” per arrancar de zero.

1) Inicialitza el projecte  
```bash
mkdir api-inventari && cd api-inventari
npm init -y
```

2) Estructura de directoris i fitxers
Crea totes les carpetes i fitxers necessaris de base:
```bash
mkdir -p src/{controllers,lib,middlewares,models,routes,validation}
touch src/server.js src/app.js \
  src/lib/db.js \
  src/controllers/products.controller.js \
  src/models/product.model.js \
  src/routes/products.routes.js \
  src/validation/products.rules.js \
  src/middlewares/not-found.js \
  src/middlewares/error-handler.js \
  .env
```

3) `package.json` mínim  
Defineix ES Modules, arrencada normal i mode watch per a dev.
```json
{
  "type": "module",
  "scripts": {
    "dev": "node --watch src/server.js",
    "start": "node src/server.js"
  }
}
```

4) Dependències  
Express + seguretat bàsica + validació + accés a Mongo i variables d’entorn.
```bash
npm i express mongoose cors helmet morgan express-validator dotenv
```

5) Connexió i arrencada  
Aquest punt consisteix en crear **3 fitxers** i omplir-los amb el codi mínim perquè l’app puga connectar a Mongo i escoltar peticions.

- **A) `.env`** (variables d’entorn del projecte)
  ```
  PORT=3000
  MONGO_URI=mongodb://127.0.0.1:27017/inventari
  ```

- **B) `src/lib/db.js`** (funció de connexió a Mongo)
  ```js
  import mongoose from 'mongoose';

  export async function connectDB(uri) {
    mongoose.set('strictQuery', true);
    await mongoose.connect(uri, { dbName: 'inventari' });
    console.log('Mongo connectada');
  }
  ```

- **C) `src/server.js`** (arrencada del servidor)
  ```js
  import 'dotenv/config';
  import app from './app.js';
  import { connectDB } from './lib/db.js';

  const PORT = process.env.PORT ?? 3000;
  const URI = process.env.MONGO_URI;

  (async () => {
    await connectDB(URI);
    app.listen(PORT, () => {
      console.log(`API a http://localhost:${PORT}`);
    });
  })();
  ```

 

5) App i rutes  
- `src/app.js`
Express amb middlewares de seguretat, logs i parseig de JSON. Ruta principal `/api/v1/products`.
  
```js
import cors from 'cors';
import helmet from 'helmet';
import morgan from 'morgan';
import express from 'express';

import productsRouter from './routes/products.routes.js';
import notFound from './middlewares/not-found.js';
import errorHandler from './middlewares/error-handler.js';

const app = express();

app.use(helmet());
app.use(cors());
app.use(morgan('dev'));
app.use(express.json());

app.get('/health', (_req, res) => {
  res.status(200).json({ status: 'ok' });
});

app.use('/api/v1/products', productsRouter);

app.use(notFound);
app.use(errorHandler);

export default app;

```

6) Model, validació i CRUD mínim  

- `src/models/product.model.js`
Esquema Mongoose amb validació bàsica i timestamps automàtics.
  ```js
  import mongoose from 'mongoose';
  const productSchema = new mongoose.Schema({
    name:   { type: String, required: true, trim: true, minlength: 2 },
    sku:    { type: String, unique: true, sparse: true, trim: true, match: /^[A-Z0-9-]+$/ },
    price:  { type: Number, required: true, min: 0 },
    stock:  { type: Number, required: true, min: 0 },
    active: { type: Boolean, default: true }
  }, { timestamps: true });
  export const Product = mongoose.model('Product', productSchema);
  ```

- `src/validation/products.rules.js`
Regles express-validator per a altes i modificacions.
  ```js
  import { body, param } from 'express-validator';
  export const productCreateRules = [
    body('name').isString().isLength({ min: 2 }),
    body('price').isFloat({ min: 0 }),
    body('stock').isInt({ min: 0 }),
    body('sku').optional().matches(/^[A-Z0-9-]+$/)
  ];
  export const productUpdateRules = [
    param('id').isMongoId(),
    body('name').optional().isString().isLength({ min: 2 }),
    body('price').optional().isFloat({ min: 0 }),
    body('stock').optional().isInt({ min: 0 }),
    body('sku').optional().matches(/^[A-Z0-9-]+$/),
    body('active').optional().isBoolean()
  ];
  ```

- `src/routes/products.routes.js`
Rutes REST i helper `validate` per a centralitzar la resposta 422.
  ```js
  import { Router } from 'express';
  import { validationResult } from 'express-validator';
  import * as controller from '../controllers/products.controller.js';
  import { productCreateRules, productUpdateRules } from '../validation/products.rules.js';

  const router = Router();
  const validate = (rules) => [
    ...rules,
    (req, res, next) => {
      const result = validationResult(req);
      if (!result.isEmpty()) return res.status(422).json({ errors: result.array() });
      next();
    }
  ];

  router.get('/', controller.list);
  router.get('/:id', controller.getById);
  router.post('/', validate(productCreateRules), controller.create);
  router.put('/:id', validate(productUpdateRules), controller.update);
  router.delete('/:id', controller.remove);
  export default router;
  ```

- `src/controllers/products.controller.js`
Controladors amb gestió d’errors d’SKU duplicat i validacions de Mongoose.
  ```js
  import { Product } from '../models/product.model.js';

  export async function list(req, res, next) {
    try {
      const { q, active } = req.query;
      const filter = {};
      if (q) filter.$or = [{ name: { $regex: q, $options: 'i' } }, { sku: { $regex: q, $options: 'i' } }];
      if (active !== undefined) filter.active = active === 'true';
      const data = await Product.find(filter).sort({ createdAt: -1 }).lean();
      res.json(data);
    } catch (err) { next(err); }
  }

  export async function getById(req, res, next) {
    try {
      const product = await Product.findById(req.params.id).lean();
      if (!product) return res.status(404).json({ error: 'No trobat' });
      res.json(product);
    } catch (err) { next(err); }
  }

  export async function create(req, res, next) {
    try {
      const created = await Product.create(req.body);
      res.status(201).json(created);
    } catch (err) {
      if (err?.code === 11000) return res.status(409).json({ error: 'SKU duplicat' });
      if (err?.name === 'ValidationError') return res.status(422).json({ error: err.message });
      next(err);
    }
  }

  export async function update(req, res, next) {
    try {
      const updated = await Product.findByIdAndUpdate(req.params.id, req.body, { new: true, runValidators: true }).lean();
      if (!updated) return res.status(404).json({ error: 'No trobat' });
      res.json(updated);
    } catch (err) {
      if (err?.code === 11000) return res.status(409).json({ error: 'SKU duplicat' });
      if (err?.name === 'ValidationError') return res.status(422).json({ error: err.message });
      next(err);
    }
  }

  export async function remove(req, res, next) {
    try {
      const out = await Product.findByIdAndDelete(req.params.id).lean();
      if (!out) return res.status(404).json({ error: 'No trobat' });
      res.status(204).send();
    } catch (err) { next(err); }
  }
  ```



- Middlewares bàsics  
  `src/middlewares/not-found.js`
  ```js
  export default function notFound(req, res) {
    res.status(404).json({ error: 'Ruta no trobada' });
  }
  ```
  `src/middlewares/error-handler.js`
  ```js
  export default function errorHandler(err, req, res, next) {
    console.error(err);
    res.status(err.status ?? 500).json({ error: err.message ?? 'Error intern' });
  }
  ```

### 🧭 Per a què serveix cada fitxer (resum ràpid)
- `package.json`: dependències i scripts (`dev`, `start`). Activa ES Modules amb `"type": "module"`.
- `.env`: configuració sensible (port, URI de Mongo, credencials). No pujar a Git.
- `src/server.js`: punt d’entrada; carrega variables, connecta a BD i inicia el servidor.
- `src/app.js`: configura Express (middlewares) i munta rutes i gestió d’errors.
- `src/lib/db.js`: funció única de connexió a Mongo amb Mongoose.
- `src/models/product.model.js`: esquema i regles de dades (validació i timestamps).
- `src/validation/products.rules.js`: validacions per entrada d’usuari (create/update).
- `src/routes/products.routes.js`: defineix endpoints i aplica validació abans de cridar el controlador.
- `src/controllers/products.controller.js`: lògica de negoci i consultes; tradueix errors a respostes HTTP.
- `src/middlewares/not-found.js`: resposta 404 quan no hi ha cap ruta.
- `src/middlewares/error-handler.js`: error global (500 o l’estat que corresponga).

### 🔄 Funcionament de tot plegat (flux complet)
1) **Client** fa una petició HTTP (ex. `POST /api/v1/products`).  
2) **Express** entra per `src/app.js`, aplica middlewares (seguretat, logs, JSON).  
3) **Rutes** (`src/routes/products.routes.js`) identifiquen l’endpoint i executen validacions.  
4) **Controlador** (`src/controllers/products.controller.js`) aplica lògica i consulta la BD.  
5) **Model** (`src/models/product.model.js`) valida i interactua amb Mongo via Mongoose.  
6) **Resposta** torna al client amb codi d’estat i JSON. Si hi ha error, el captura `error-handler`.

### ▶️ Posada en marxa

Nota: Arranca MongoDB  amb Docker:

```bash
docker run -d -p 27017:27017 --name mongo mongo
```


#### 🧪 Proves ràpides amb curl


```bash
# Arranca
npm run dev

# Crear
curl -X POST http://localhost:3000/api/v1/products \
  -H "Content-Type: application/json" \
  -d '{"name":"Tassa","sku":"TAS-001","price":4.5,"stock":20}'

# Llistar
curl http://localhost:3000/api/v1/products


```

Partint de l’ID obtingut abans, pots provar un show, una  actualització i un esborrat:
```bash
# Obtenir per ID
curl http://localhost:3000/api/v1/products/<id>

# Actualitzar (PUT)
curl -X PUT http://localhost:3000/api/v1/products/<id> \
  -H "Content-Type: application/json" \
  -d '{"name":"Tassa XL","price":5.25,"stock":18,"active":true}'

# Esborrar (DELETE)
curl -X DELETE http://localhost:3000/api/v1/products/<id>
```

#### Exemples útils

##### 🧩 Una altra taula: categories 

Afegim una col·lecció `categories` i relacionem el producte amb `categoryId`.

- `src/models/category.model.js`

```js
import mongoose from 'mongoose';
const categorySchema = new mongoose.Schema({
  name: { type: String, required: true, trim: true, unique: true }
}, { timestamps: true });
export const Category = mongoose.model('Category', categorySchema);
```

- (Opcional) Al model de producte, afegeix la relació:
```js
// dins de productSchema
categoryId: { type: mongoose.Schema.Types.ObjectId, ref: 'Category' }
```

- `src/controllers/categories.controller.js` (mínim)
```js
import { Category } from '../models/category.model.js';
export async function list(req, res, next) {
  try { res.json(await Category.find().sort({ name: 1 }).lean()); }
  catch (err) { next(err); }
}
export async function create(req, res, next) {
  try { res.status(201).json(await Category.create(req.body)); }
  catch (err) { next(err); }
}
```

- `src/routes/categories.routes.js` (mínim)
```js
import { Router } from 'express';
import * as controller from '../controllers/categories.controller.js';
const router = Router();
router.get('/', controller.list);
router.post('/', controller.create);
export default router;
```

- `src/app.js`: munta les rutes
```js
import categoriesRouter from './routes/categories.routes.js';
app.use('/api/v1/categories', categoriesRouter);
```

Prova ràpida amb curl:
```bash
# Crear categoria
curl -X POST http://localhost:3000/api/v1/categories \
  -H "Content-Type: application/json" \
  -d '{"name":"Tasses"}'

# Crear producte referenciat (usa l’ID de la categoria)
curl -X POST http://localhost:3000/api/v1/products \
  -H "Content-Type: application/json" \
  -d '{"name":"Tassa Negra","sku":"TAS-010","price":6.5,"stock":10,"categoryId":"<categoryId>"}'

# Llistar productes amb la categoria
curl http://localhost:3000/api/v1/products
```

 

##### Retornar el nom de la categoria en un producte
Si tens `categoryId` al model, pots fer `populate` per traure el nom en la mateixa resposta.

- `src/controllers/products.controller.js` (exemple en `getById`)
  ```js
  export async function getById(req, res, next) {
    try {
      const product = await Product.findById(req.params.id)
        .populate('categoryId', 'name')
        .lean();
      if (!product) return res.status(404).json({ error: 'No trobat' });
      res.json(product);
    } catch (err) { next(err); }
  }
  ```

Resposta esperada (resum):
```json
{
  "_id": "64f...",
  "name": "Tassa Negra",
  "categoryId": { "_id": "64a...", "name": "Tasses" }
}
```

##### Consultes filtrades per preu i categoria
Amplia el `list` perquè accepte `minPrice`, `maxPrice` i `category`.

- `src/controllers/products.controller.js` (exemple en `list`)
  ```js
  export async function list(req, res, next) {
    try {
      const { q, active, minPrice, maxPrice, category } = req.query;
      const filter = {};
      if (q) filter.$or = [{ name: { $regex: q, $options: 'i' } }, { sku: { $regex: q, $options: 'i' } }];
      if (active !== undefined) filter.active = active === 'true';
      if (minPrice) filter.price = { ...filter.price, $gte: Number(minPrice) };
      if (maxPrice) filter.price = { ...filter.price, $lte: Number(maxPrice) };
      if (category) filter.categoryId = category; // id de categoria
      const data = await Product.find(filter)
        .populate('categoryId', 'name')
        .sort({ createdAt: -1 })
        .lean();
      res.json(data);
    } catch (err) { next(err); }
  }
  ```

Prova ràpida amb curl:
```bash
# Productes entre 5 i 20, actius i d'una categoria concreta
curl "http://localhost:3000/api/v1/products?minPrice=5&maxPrice=20&active=true&category=<categoryId>"

# Cerca per text (nom o sku) i filtra per preu mínim
curl "http://localhost:3000/api/v1/products?q=tassa&minPrice=3"
```

##### ✅ Exemple de paginació 
Afegim `page` i `limit` com a query params i retornem també `total` i `pages`.

```js
// products.controller.js (versio de list amb paginacio)
export async function list(req, res, next) {
  try {
    const { q, active } = req.query;
    const page = Math.max(parseInt(req.query.page ?? '1', 10), 1);
    const limit = Math.min(Math.max(parseInt(req.query.limit ?? '10', 10), 1), 100);
    const skip = (page - 1) * limit;

    const filter = {};
    if (q) filter.$or = [{ name: { $regex: q, $options: 'i' } }, { sku: { $regex: q, $options: 'i' } }];
    if (active !== undefined) filter.active = active === 'true';

    const [total, data] = await Promise.all([
      Product.countDocuments(filter),
      Product.find(filter).sort({ createdAt: -1 }).skip(skip).limit(limit).lean()
    ]);

    res.json({
      data,
      page,
      limit,
      total,
      pages: Math.ceil(total / limit)
    });
  } catch (err) { next(err); }
}
```

Exemple de crida:
```bash
curl "http://localhost:3000/api/v1/products?page=2&limit=5&q=tassa"
```


### 📄 Swagger / OpenAPI

- Què és: OpenAPI és l’estàndard per descriure APIs HTTP de forma formal (endpoints, paràmetres, esquemes, codis d’estat). Swagger UI és el visualitzador interactiu d’aquest contracte.
- Per què documentar: 

    - Contracte clar entre backend i frontend (evita malentesos).
    - Autogenera una “prova” manual amb botons Try it out.
    - Serveix com a font única de veritat; facilita QA i onboarding.
    - Permet generar SDKs/clients i validació automàtica si s’integra amb linters.

- On guardar la documentació:

    - Fitxer `openapi.json` o `openapi.yml` a l’arrel (fàcil de versionar i consultar).
    - O bé comentaris JSDoc a les rutes amb `swagger-jsdoc` que generen l’esquema en temps d’arrencada.

- Paquets típics:

    - `swagger-ui-express`: serveix la UI a `/api-docs`.
    - `swagger-jsdoc`: genera OpenAPI a partir de comentaris JSDoc en els fitxers de rutes/controladors.

- “Documentar” no és un Word, sinó descriure formalment paths, requestBody, responses i schemas.

- Passos ràpids per veure la UI (amb `swagger-jsdoc`):
  ```bash
  npm i swagger-ui-express swagger-jsdoc
  ```
  1. Escriu comentaris JSDoc a les rutes.
  2. Crea el fitxer de config `src/swagger.js`.
  3. A `app.js`, munta `/api-docs` amb `swagger-ui-express`.
  4. Obri `http://localhost:3000/api-docs`.

- Nota: també pots mantindre un `openapi.json` o `openapi.yml` versionat a l’arrel del projecte, però ací no en posem cap exemple per evitar duplicitats.

- JSDoc (swagger-jsdoc) en rutes:
  Escriu l’especificació al costat del codi per evitar desincronitzacions.
  ```js
  /**
   * @openapi
   * /api/v1/products:
   *   get:
   *     summary: Llistar productes
   *     responses:
   *       200: { description: OK }
   */
  ```
- `src/swagger.js` (config base amb `swagger-jsdoc`):
  ```js
  import swaggerJSDoc from 'swagger-jsdoc';

  export const swaggerSpec = swaggerJSDoc({
    definition: {
      openapi: '3.0.3',
      info: { title: 'API Inventari', version: '1.0.0' },
      servers: [{ url: 'http://localhost:3000' }]
    },
    apis: ['./src/routes/*.js']
  });
  ```
- Muntar `/api-docs` en `src/app.js`:
  ```js
  import swaggerUi from 'swagger-ui-express';
  import { swaggerSpec } from './swagger.js';

  app.use('/api-docs', swaggerUi.serve, swaggerUi.setup(swaggerSpec));
  ```
- Exemple JSDoc complet per a POST amb esquemes reutilitzats:
  Inclou exemples bons i roïns perquè entenguen la validació.
  ```js
  /**
   * @openapi
   * /api/v1/products:
   *   post:
   *     summary: Crear producte
   *     tags: [Products]
   *     requestBody:
   *       required: true
   *       content:
   *         application/json:
   *           schema: { $ref: '#/components/schemas/ProductCreate' }
   *           examples:
   *             ok: { value: { name: "Tassa", sku: "TAS-001", price: 4.5, stock: 20 } }
   *             invalid: { value: { name: "", price: -1 } }
   *     responses:
   *       201: { description: Creat }
   *       409: { description: SKU duplicat }
   *       422:
   *         description: Validació incorrecta
   *         content:
   *           application/json:
   *             schema: { $ref: '#/components/schemas/Error' }
  */
  ```
- Bones pràctiques: descriu paràmetres (`page`, `limit`, `sort`, filtres), codis d’error (`400`, `404`, `409`, `422`, `500`), i revisa l’especificació amb Swagger UI abans de lliurar. Posa `examples` en request/response perquè l’usuari puga provar amb un clic.



### 📝 Exercici únic per a classe
> Explica breument el flux `client → ruta → middleware → controlador → Mongo`.

Implementa les millores següents sobre el projecte base:

1. **Paginació i ordenació** a `GET /products` (`page`, `limit`, `sort`).
2. **Endpoint CSV**: `GET /products/export.csv` amb capçalera `text/csv`.
3. **Validacions millorades**: nom min 3 caràcters, `sku` `[A-Z0-9-]+`, resposta `422` detallada.
4. **Nova col·lecció relacionada (proveïdors o vendes)**: model, controlador i rutes CRUD mínimes.
5. **Relació amb productes**: afegeix el camp corresponent (ex. `supplierId` o `saleId`) i retorna dades relacionades amb `populate`.
6. **Documentació completa**: actualitza els JSDoc amb tots els endpoints (products i nova col·lecció) i els esquemes corresponents.

Rubrica curta: codi net, rutes correctes, validacions completes, errors gestionats, proves amb curl/Postman i documentació al dia.

### 🛢️ Introducció ràpida a MySQL amb Node
Objectiu: mateix CRUD però amb base de dades relacional. Servix com a plantilla mínima per fer proves sense ORM pesat.

- Instal·lació: `npm i mysql2`. Si vols un query builder lleuger, afegeix `npm i knex`.
- Connexió bàsica (`src/lib/db-mysql.js`): crea un pool reutilitzable per a totes les peticions.
  ```js
  import mysql from 'mysql2/promise';
  export const pool = mysql.createPool({
    host: process.env.DB_HOST ?? 'localhost',
    user: process.env.DB_USER ?? 'root',
    password: process.env.DB_PASS ?? '',
    database: process.env.DB_NAME ?? 'inventari',
    waitForConnections: true,
    connectionLimit: 10
  });
  ```
- `.env` example (per no deixar credencials al codi):
  ```
  DB_HOST=127.0.0.1
  DB_USER=root
  DB_PASS=secret
  DB_NAME=inventari
  ```
- Taula mínima (DDL): defineix tipus i restriccions clares.
  ```sql
  CREATE TABLE products (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    sku VARCHAR(50) UNIQUE,
    price DECIMAL(10,2) NOT NULL,
    stock INT NOT NULL DEFAULT 0,
    active TINYINT(1) NOT NULL DEFAULT 1,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
  );
  ```
- CRUD resumit (`src/controllers/products.controller.mysql.js`): usa consultes preparades (`?`) per evitar SQL injection.
  ```js
  import { pool } from '../lib/db-mysql.js';

  export async function list(req, res, next) {
    try {
      const [rows] = await pool.query('SELECT * FROM products ORDER BY created_at DESC');
      res.json(rows);
    } catch (err) { next(err); }
  }

  export async function create(req, res, next) {
    try {
      const { name, sku, price, stock, active = 1 } = req.body;
      const [result] = await pool.query(
        'INSERT INTO products (name, sku, price, stock, active) VALUES (?, ?, ?, ?, ?)',
        [name, sku, price, stock, active]
      );
      const [rows] = await pool.query('SELECT * FROM products WHERE id = ?', [result.insertId]);
      res.status(201).json(rows[0]);
    } catch (err) {
      if (err?.code === 'ER_DUP_ENTRY') return res.status(409).json({ error: 'SKU duplicat' });
      next(err);
    }
  }
  ```
- Integració: al router, selecciona controlador segons `STORE=mysql|mongo` en `app.js` per reutilitzar les mateixes rutes.
- Bones pràctiques MySQL: prepared statements sempre, defineix charset/timezone al pool si cal, usa transaccions per operacions multi-query (com crear ordre + línies).
