 # 📘 Desenvolupament d'APIs amb Node.js  

## SA 6.1 – Introducció i conceptes previs
  
### 🧠 1. Què és Node.js?

**Node.js** és un entorn d’execució de JavaScript fora del navegador.  
En lloc d’executar-se al client (com en aplicacions web tradicionals), s’executa al **servidor**, permetent-nos construir aplicacions backend, APIs, serveis web i molt més utilitzant el mateix llenguatge que al frontend: **JavaScript**.

💡 **Per què és interessant per a 2DAW?**

- Permet treballar amb un únic llenguatge tant al client com al servidor.
- És lleuger, ràpid i molt eficient gràcies al motor V8 de Chrome.
- Té un ecosistema immens de paquets a través de `npm`.
- És ideal per crear **APIs REST**, **microserveis** o aplicacions temps real.

📦 Exemple bàsic:
```js
// hola.js
console.log('Hola món des de Node.js!');
```
Executa’l amb:
```bash
node hola.js
```

---

### 🚀 2. Què és Express?

**Express** és un framework minimalista per a Node.js que simplifica molt la creació de servidors web i APIs.  
Permet definir **rutes HTTP**, gestionar **paràmetres**, utilitzar **middlewares**, enviar respostes i molt més amb molt poques línies de codi.

✅ Funcions clau d’Express:

- Crear rutes per als diferents recursos (`/users`, `/products`, etc.)
- Gestionar peticions HTTP (`GET`, `POST`, `PUT`, `DELETE`, …)
- Analitzar dades del cos de la petició (`req.body`)
- Afegir funcionalitats amb *middlewares* (validació, logs, errors…)
- Organitzar lògica del servidor de manera clara i escalable

📦 Exemple mínim d’un servidor Express:

```js
import express from 'express';

const app = express();
const PORT = 3000;

app.get('/', (req, res) => {
  res.send('Hola món amb Express!');
});

app.listen(PORT, () => {
  console.log(`Servidor escoltant a http://localhost:${PORT}`);
});
```

---

### 🌐 3. Què és una API?

Una **API** (*Application Programming Interface*) és un conjunt de regles i punts d’entrada que permeten que un programa puga comunicar-se amb un altre.  
En el context web, una **API REST** és un servei que exposa dades o funcionalitats a través del protocol **HTTP**.

Per exemple, una API de productes pot oferir endpoints com:

| Mètode | Endpoint                 | Descripció                        |
|--------|--------------------------|----------------------------------|
| GET    | `/api/v1/products`       | Obté tots els productes          |
| GET    | `/api/v1/products/:id`   | Obté un producte per ID          |
| POST   | `/api/v1/products`       | Crea un nou producte            |
| PUT    | `/api/v1/products/:id`   | Actualitza un producte existent |
| DELETE | `/api/v1/products/:id`   | Elimina un producte             |

📌 Una **API RESTful** té unes característiques concretes:

- Usa els mètodes HTTP correctament (`GET`, `POST`, `PUT`, `DELETE`, `PATCH`…)
- Utilitza URLs clares i orientades a recursos (`/users`, `/orders`, `/products`)
- Retorna dades en format estàndard (normalment `JSON`)
- Fa ús dels codis d’estat HTTP (`200`, `201`, `404`, `422`, `500`…)

---

### 🏗️ 4. Arquitectura i estructura d’un projecte API

Una API professional sol tindre una estructura organitzada que facilite el manteniment i l’escalabilitat:

```
api-inventari/
├─ package.json
├─ .env
├─ src/
│  ├─ server.js          # Punt d'entrada: arranca el servidor
│  ├─ app.js             # Configura Express i middlewares
│  ├─ routes/            # Definició de rutes (endpoints)
│  ├─ controllers/       # Lògica de negoci per a cada ruta
│  ├─ models/            # Definició dels esquemes de dades (Mongo, etc.)
│  ├─ middlewares/       # Validació, errors, autenticació...
│  ├─ validation/        # Regles de validació d’entrada
│  └─ lib/               # Connexió a BD i utilitats
└─ openapi.json          # Especificació Swagger
```

💡 **Avantatge d’aquesta estructura:**

- Separa clarament responsabilitats  
- Facilita el testing i el manteniment  
- Permet escalar el projecte fàcilment

---

### 🔧 5. Flux de treball d’una API

Quan un client (p. ex. una aplicació web o mòbil) fa una petició a l’API:

1. 🛰️ El client envia una **petició HTTP** (`GET`, `POST`, etc.) a un endpoint.
2. 📬 El servidor Express rep la petició i comprova si la ruta existeix.
3. 🧰 Els **middlewares** processen la petició (validació, autenticació...).
4. 🧠 El **controlador** executa la lògica (consultar BD, crear recurs…).
5. 📦 El **model** interactua amb la base de dades si cal.
6. 📤 El servidor retorna una **resposta JSON** amb un codi d’estat adequat.

Exemple de resposta:

```json
{
  "id": "64d0c6f5b2e4f1",
  "name": "Cafè 1kg",
  "price": 12.50,
  "stock": 50,
  "active": true
}
```

---

### 🛠️ 6. Eines útils per al desenvolupament d’APIs

- **Postman / Thunder Client** → per provar endpoints manualment  
- **MongoDB Compass** → per gestionar dades si uses MongoDB  
- **Swagger UI** → per documentar i provar l’API  
- **ESLint + Prettier** → per mantenir un codi net i consistent  
- **dotenv** → per gestionar variables d’entorn

---

### 💡 Bones pràctiques des del principi

✅ **Nom de rutes RESTful**: utilitza noms de recursos en plural (`/products`, `/users`)  
✅ **Codis d’estat HTTP**: respon amb el codi correcte (`201` en creació, `404` si no trobat…)  
✅ **JSON net i clar**: evita informació innecessària i segueix un format consistent  
✅ **Middleware de validació**: mai confies en les dades d’entrada  
✅ **Control centralitzat d’errors**: un únic lloc per capturar i gestionar errors

## SA 6.2 Creació del projecte pas a pas (API en memòria)

En aquesta secció construirem una **API REST d’inventari** amb **Express** utilitzant **ES Modules (`import/export`)** i **emmagatzematge en memòria** (sense base de dades). L’objectiu és entendre **clarament** el flux: *rutes → middleware → controladors → respostes*. A la Secció 3 connectarem la mateixa API a **MongoDB** sense canviar la interfície pública.
 
### 1) Inicialització del projecte

1. Crea una carpeta i inicialitza `npm`:
   ```bash
   mkdir api-inventari && cd api-inventari
   npm init -y
   ```

2. Edita `package.json` per activar **ES Modules** i afegir scripts bàsics:
   ```json
   {
     "name": "api-inventari",
     "version": "1.0.0",
     "type": "module",
     "main": "src/server.js",
     "scripts": {
       "dev": "node --watch src/server.js",
       "start": "node src/server.js"
     }
   }
   ```

3. Instala dependències necessàries:
   ```bash
   npm i express cors helmet morgan express-validator swagger-ui-express dotenv
   npm i -D eslint
   ```

> ℹ️ `swagger-ui-express` el farem servir per mostrar la documentació en la Secció 4 (ara deixarem el “ganxo” posat).
 
### 2) Estructura del projecte

```
api-inventari/
├─ package.json
├─ .env                 # opcional (PORT, etc.)
├─ openapi.json         # la farem a la Secció 4
└─ src/
   ├─ server.js         # arrencada
   ├─ app.js            # configuració d’Express i rutes
   ├─ routes/
   │  └─ products.routes.js
   ├─ controllers/
   │  └─ products.controller.memory.js
   ├─ middlewares/
   │  ├─ not-found.js
   │  └─ error-handler.js
   └─ validation/
      └─ products.rules.js
```
 
### 3) App i servidor

**`src/app.js`**
```js
import express from 'express';
import morgan from 'morgan';
import helmet from 'helmet';
import cors from 'cors';

import productsRouter from './routes/products.routes.js';
import notFound from './middlewares/not-found.js';
import errorHandler from './middlewares/error-handler.js';

const app = express();

// Middlewares globals
app.use(helmet());
app.use(cors());
app.use(express.json());
app.use(morgan('dev'));

// Rutes
app.use('/api/v1/products', productsRouter);

// 404 i errors
app.use(notFound);
app.use(errorHandler);

export default app;
```

**`src/server.js`**
```js
import 'dotenv/config';
import app from './app.js';

const PORT = process.env.PORT ?? 3000;
app.listen(PORT, () => {
  console.log(`API Inventari escoltant a http://localhost:${PORT}`);
});
```
 
### 4) Middlewares de 404 i errors

**`src/middlewares/not-found.js`**
```js
export default function notFound(req, res, next) {
  res.status(404).json({ error: 'Ruta no trobada' });
}
```

**`src/middlewares/error-handler.js`**
```js
export default function errorHandler(err, req, res, next) {
  console.error(err);
  const status = err.status ?? 500;
  res.status(status).json({ error: err.message ?? 'Error intern del servidor' });
}
```
 
### 5) Validació d’entrada amb `express-validator`

**`src/validation/products.rules.js`**
```js
import { body, param, query } from 'express-validator';

export const listQueryRules = [
  query('q').optional().isString(),
  query('active').optional().isBoolean().toBoolean(),
  query('minPrice').optional().isFloat({ min: 0 }).toFloat(),
  query('maxPrice').optional().isFloat({ min: 0 }).toFloat()
];

export const productCreateRules = [
  body('name').isString().trim().notEmpty().withMessage('name requerit'),
  body('sku').optional().isString().trim(),
  body('price').isFloat({ min: 0 }).withMessage('price >= 0'),
  body('stock').isInt({ min: 0 }).withMessage('stock >= 0'),
  body('active').optional().isBoolean()
];

export const productUpdateRules = [
  param('id').isString().notEmpty(),
  body('name').optional().isString().trim().notEmpty(),
  body('sku').optional().isString().trim(),
  body('price').optional().isFloat({ min: 0 }),
  body('stock').optional().isInt({ min: 0 }),
  body('active').optional().isBoolean()
];

export const productStockRules = [
  param('id').isString().notEmpty(),
  body('delta').isInt().withMessage('delta integer (positiu o negatiu)')
];
```

> 💡 **Consell didàctic:** tracteu la **validació** com una “porta d’entrada” a la API. Tot passa per ací.

 
### 6) Rutes i CRUD en memòria

**`src/routes/products.routes.js`**
```js
import { Router } from 'express';
import * as controller from '../controllers/products.controller.memory.js';
import { listQueryRules, productCreateRules, productStockRules, productUpdateRules } from '../validation/products.rules.js';
import { validationResult } from 'express-validator';

const router = Router();

const validate = (rules) => [
  ...rules,
  (req, res, next) => {
    const result = validationResult(req);
    if (!result.isEmpty()) return res.status(422).json({ errors: result.array() });
    next();
  }
];

router.get('/', validate(listQueryRules), controller.list);
router.get('/:id', controller.getById);
router.post('/', validate(productCreateRules), controller.create);
router.put('/:id', validate(productUpdateRules), controller.update);
router.patch('/:id/stock', validate(productStockRules), controller.adjustStock);
router.delete('/:id', controller.remove);

export default router;
```

**`src/controllers/products.controller.memory.js`**
```js
// Almacenament en memòria (per a aprendre el flux)
let PRODUCTS = [];
let _id = 1;

export async function list(req, res, next) {
  try {
    const { q, active, minPrice, maxPrice } = req.query;
    let data = [...PRODUCTS];

    if (q) {
      const needle = String(q).toLowerCase();
      data = data.filter(p => p.name.toLowerCase().includes(needle) || (p.sku ?? '').toLowerCase().includes(needle));
    }
    if (typeof active === 'boolean') data = data.filter(p => p.active === active);
    if (typeof minPrice === 'number') data = data.filter(p => p.price >= minPrice);
    if (typeof maxPrice === 'number') data = data.filter(p => p.price <= maxPrice);

    res.json(data);
  } catch (err) { next(err); }
}

export async function getById(req, res, next) {
  try {
    const product = PRODUCTS.find(p => String(p.id) === String(req.params.id));
    if (!product) return res.status(404).json({ error: 'No trobat' });
    res.json(product);
  } catch (err) { next(err); }
}

export async function create(req, res, next) {
  try {
    const { name, sku, price, stock, active = true } = req.body;
    if (sku && PRODUCTS.some(p => p.sku === sku)) return res.status(409).json({ error: 'SKU duplicat' });

    const now = new Date().toISOString();
    const created = { id: String(_id++), name, sku, price: Number(price), stock: Number(stock), active: Boolean(active), createdAt: now, updatedAt: now };
    PRODUCTS.push(created);
    res.status(201).json(created);
  } catch (err) { next(err); }
}

export async function update(req, res, next) {
  try {
    const idx = PRODUCTS.findIndex(p => String(p.id) === String(req.params.id));
    if (idx === -1) return res.status(404).json({ error: 'No trobat' });
    const prev = PRODUCTS[idx];
    const { name = prev.name, sku = prev.sku, price = prev.price, stock = prev.stock, active = prev.active } = req.body ?? {};

    if (sku && sku !== prev.sku && PRODUCTS.some(p => p.sku === sku)) return res.status(409).json({ error: 'SKU duplicat' });

    const updated = { ...prev, name, sku, price: Number(price), stock: Number(stock), active: Boolean(active), updatedAt: new Date().toISOString() };
    PRODUCTS[idx] = updated;
    res.json(updated);
  } catch (err) { next(err); }
}

export async function adjustStock(req, res, next) {
  try {
    const idx = PRODUCTS.findIndex(p => String(p.id) === String(req.params.id));
    if (idx === -1) return res.status(404).json({ error: 'No trobat' });
    const { delta } = req.body;
    const prev = PRODUCTS[idx];
    const newStock = Math.max(0, Number(prev.stock) + Number(delta));
    const updated = { ...prev, stock: newStock, updatedAt: new Date().toISOString() };
    PRODUCTS[idx] = updated;
    res.json(updated);
  } catch (err) { next(err); }
}

export async function remove(req, res, next) {
  try {
    const idx = PRODUCTS.findIndex(p => String(p.id) === String(req.params.id));
    if (idx === -1) return res.status(404).json({ error: 'No trobat' });
    PRODUCTS.splice(idx, 1);
    res.status(204).send();
  } catch (err) { next(err); }
}
```
 
### 7) Proves amb Postman / curl

1. **Arranca el servidor**:
   ```bash
   npm run dev
   ```

2. **Crea un producte**:
   ```bash
   curl -X POST http://localhost:3000/api/v1/products      -H "Content-Type: application/json"      -d '{"name":"Tassa ceràmica","sku":"TAS-001","price":4.5,"stock":20}'
   ```

3. **Llista productes**:
   ```bash
   curl http://localhost:3000/api/v1/products
   ```

4. **Obté per ID**:
   ```bash
   curl http://localhost:3000/api/v1/products/1
   ```

5. **Actualitza**:
   ```bash
   curl -X PUT http://localhost:3000/api/v1/products/1      -H "Content-Type: application/json"      -d '{"price":4.9,"stock":30}'
   ```

6. **Ajusta stock**:
   ```bash
   curl -X PATCH http://localhost:3000/api/v1/products/1/stock      -H "Content-Type: application/json"      -d '{"delta": -2}'
   ```

7. **Elimina**:
   ```bash
   curl -X DELETE http://localhost:3000/api/v1/products/1
   ```
 
### 8) Proves des del client (JavaScript `fetch()`)

> Pots provar-ho des de la consola del navegador o en un fitxer `.html` senzill amb `<script type="module">`.

```html
<script type="module">
  const API = 'http://localhost:3000/api/v1/products';

  // Crear
  const created = await fetch(API, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ name: 'Cafè 1kg', sku: 'CAF-1000', price: 12.5, stock: 50 })
  }).then(r => r.json());
  console.log('Creat:', created);

  // Llistar
  const list = await fetch(API).then(r => r.json());
  console.log('Llista:', list);

  // Obtenir per ID
  const one = await fetch(`${API}/${created.id}`).then(r => r.json());
  console.log('Un:', one);

  // Actualitzar
  const updated = await fetch(`${API}/${created.id}`, {
    method: 'PUT',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ price: 13.2, stock: 45 })
  }).then(r => r.json());
  console.log('Actualitzat:', updated);

  // Ajustar stock
  const stocked = await fetch(`${API}/${created.id}/stock`, {
    method: 'PATCH',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ delta: -5 })
  }).then(r => r.json());
  console.log('Stock:', stocked);

  // Eliminar
  const delRes = await fetch(`${API}/${created.id}`, { method: 'DELETE' });
  console.log('Eliminat, status =', delRes.status);
</script>
```
 
### 9) Extres útils per a classe

- **CORS**: si tens un frontend en un altre port (p. ex. Vite a `5173`), CORS ja està habilitat globalment amb `app.use(cors())`. Pots restringir l’origen si cal:
  ```js
  app.use(cors({ origin: ['http://localhost:5173'] }));
  ```
- **Límit de mida del body** (per evitar abusos):
  ```js
  app.use(express.json({ limit: '100kb' }));
  ```
- **Logs**: `morgan('dev')` és ideal en dev. En prod, millor logs estructurats (p. ex. pino).
 

### 10) Exercicis (per entregar)

1. **Paginació i ordenació** a `GET /products` (`?page=1&limit=10&sort=price,-name`).
2. **Filtre per rang de stock** (`stockMin`, `stockMax`).
3. **Camp nou `category`** i filtre `?category=begudes`.
4. **Endpoint `GET /products/export.csv`** que retorne un CSV dels productes.
5. **Validacions extra** (nom mínim 3 caràcters, `sku` regex `[A-Z0-9-]+`).

> 💡 Avaluació formativa: valorar codi net, ús correcte d’HTTP, validacions, i que no es trenque davant d’inputs erronis.

 
### 11) Troubleshooting

- **`Error [ERR_MODULE_NOT_FOUND]`** → comprova rutes d’import i extensions `.js` en imports locals.
- **`Unexpected token 'export'`** → falta `"type": "module"` al `package.json`.
- **No parseja JSON** → assegura `app.use(express.json())` i header `Content-Type: application/json` a les peticions.
- **CORS** → si el navegador bloqueja, comprova `app.use(cors())` i l’o

## SA 6.3 Connexió a MongoDB (Mongoose) i CRUD persistent

En aquesta secció convertirem l’API en memòria de la Secció 2 en una **API amb persistència real** utilitzant **MongoDB** i **Mongoose**. Mantindrem els **endpoints** i el **contracte** (mateixa interfície pública), canviant només la **capa de dades**.
 
### 1) Requisits i configuració

#### 1.1 Instal·lació de dependències

Si no ho has fet encara:
```bash
npm i mongoose dotenv
```

#### 1.2 Variables d’entorn `.env`

Crea o edita `.env` a l’arrel del projecte:
```
PORT=3000
STORE=mongo
MONGO_URI=mongodb://127.0.0.1:27017/inventari
```

> 💡 Si utilitzes **MongoDB Atlas**, reemplaça `MONGO_URI` pel connection string del teu cluster.
 
### 2) Connexió a MongoDB

**`src/lib/db.js`**
```js
import mongoose from 'mongoose';

export async function connectDB(uri) {
  mongoose.set('strictQuery', true);
  await mongoose.connect(uri, { dbName: 'inventari' });
  console.log('MongoDB connectada');
}
```

**`src/server.js`** (arrencada amb connexió quan `STORE=mongo`)
```js
import 'dotenv/config';
import app from './app.js';
import { connectDB } from './lib/db.js';

const PORT = process.env.PORT ?? 3000;
const STORE = process.env.STORE ?? 'memory';

(async () => {
  try {
    if (STORE === 'mongo') {
      const URI = process.env.MONGO_URI;
      if (!URI) {
        console.error('Falta MONGO_URI en .env');
        process.exit(1);
      }
      await connectDB(URI);
    }
    app.listen(PORT, () => {
      console.log(`API Inventari escoltant a http://localhost:${PORT} (store=${STORE})`);
    });
  } catch (err) {
    console.error('Error arrencant:', err);
    process.exit(1);
  }
})();
```
 
### 3) Model de dades amb Mongoose

**`src/models/product.model.js`**
```js
import mongoose from 'mongoose';

const productSchema = new mongoose.Schema({
  name: { type: String, required: true, trim: true, minlength: 2 },
  sku:  { type: String, unique: true, sparse: true, trim: true, match: /^[A-Z0-9-]+$/ },
  price:{ type: Number, required: true, min: 0 },
  stock:{ type: Number, required: true, min: 0 },
  active:{ type: Boolean, default: true }
}, { timestamps: true });

// Índex útil per a cerques
productSchema.index({ name: 'text', sku: 'text' });

export const Product = mongoose.model('Product', productSchema);
```

> 🧠 **Notes**  
> - `unique: true` a `sku` crea un índex únic (evita duplicats).  
> - `sparse: true` permet documents sense `sku` sense violar l’únic.  
> - `match` valida el format: lletres majúscules, digits i guions.  
> - `timestamps: true` afegeix `createdAt` i `updatedAt` automàticament.

 
### 4) Reescriure controladors per a Mongo

**`src/controllers/products.controller.mongo.js`**
```js
import { Product } from '../models/product.model.js';

export async function list(req, res, next) {
  try {
    const { q, active, minPrice, maxPrice } = req.query;
    const filter = {};

    if (typeof active === 'boolean') filter.active = active;
    if (typeof minPrice === 'number' || typeof maxPrice === 'number') {
      filter.price = {};
      if (typeof minPrice === 'number') filter.price.$gte = minPrice;
      if (typeof maxPrice === 'number') filter.price.$lte = maxPrice;
    }
    if (q) {
      filter.$or = [
        { name: { $regex: q, $options: 'i' } },
        { sku:  { $regex: q, $options: 'i' } }
      ];
    }

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
    const { name, sku, price, stock, active = true } = req.body;
    const created = await Product.create({ name, sku, price, stock, active });
    res.status(201).json(created);
  } catch (err) {
    if (err?.code === 11000) return res.status(409).json({ error: 'SKU duplicat' });
    if (err?.name === 'ValidationError') return res.status(422).json({ error: err.message });
    next(err);
  }
}

export async function update(req, res, next) {
  try {
    const { id } = req.params;
    const update = req.body ?? {};
    const updated = await Product.findByIdAndUpdate(id, update, { new: true, runValidators: true }).lean();
    if (!updated) return res.status(404).json({ error: 'No trobat' });
    res.json(updated);
  } catch (err) {
    if (err?.code === 11000) return res.status(409).json({ error: 'SKU duplicat' });
    if (err?.name === 'ValidationError') return res.status(422).json({ error: err.message });
    next(err);
  }
}

export async function adjustStock(req, res, next) {
  try {
    const { id } = req.params;
    const { delta } = req.body;
    const product = await Product.findById(id);
    if (!product) return res.status(404).json({ error: 'No trobat' });
    product.stock = Math.max(0, product.stock + Number(delta));
    await product.save();
    res.json(product);
  } catch (err) { next(err); }
}

export async function remove(req, res, next) {
  try {
    const { id } = req.params;
    const out = await Product.findByIdAndDelete(id).lean();
    if (!out) return res.status(404).json({ error: 'No trobat' });
    res.status(204).send();
  } catch (err) { next(err); }
}
```

**`src/routes/products.routes.mongo.js`**
```js
import { Router } from 'express';
import * as controller from '../controllers/products.controller.mongo.js';
import { listQueryRules, productCreateRules, productStockRules, productUpdateRules } from '../validation/products.rules.js';
import { validationResult } from 'express-validator';

const router = Router();

const validate = (rules) => [
  ...rules,
  (req, res, next) => {
    const result = validationResult(req);
    if (!result.isEmpty()) return res.status(422).json({ errors: result.array() });
    next();
  }
];

router.get('/', validate(listQueryRules), controller.list);
router.get('/:id', controller.getById);
router.post('/', validate(productCreateRules), controller.create);
router.put('/:id', validate(productUpdateRules), controller.update);
router.patch('/:id/stock', validate(productStockRules), controller.adjustStock);
router.delete('/:id', controller.remove);

export default router;
```

**`src/app.js`** (selecció de router per `STORE`)
```js
import express from 'express';
import morgan from 'morgan';
import helmet from 'helmet';
import cors from 'cors';

import productsRouterMemory from './routes/products.routes.js';       // memòria
import productsRouterMongo from './routes/products.routes.mongo.js';  // Mongo

import notFound from './middlewares/not-found.js';
import errorHandler from './middlewares/error-handler.js';

const app = express();
app.use(helmet());
app.use(cors());
app.use(express.json());
app.use(morgan('dev'));

const STORE = process.env.STORE ?? 'memory';
const productsRouter = STORE === 'mongo' ? productsRouterMongo : productsRouterMemory;

app.use('/api/v1/products', productsRouter);

app.use(notFound);
app.use(errorHandler);

export default app;
```
 
### 5) Seed de dades (opc.)

**`scripts/seed.js`**
```js
import 'dotenv/config';
import { connectDB } from '../src/lib/db.js';
import { Product } from '../src/models/product.model.js';

const URI = process.env.MONGO_URI;

(async () => {
  try {
    if (!URI) throw new Error('Defineix MONGO_URI en .env');
    await connectDB(URI);
    await Product.deleteMany({});
    await Product.insertMany([
      { name: 'Cafè gra 1kg', sku: 'CAF-1000', price: 12.5, stock: 50, active: true },
      { name: 'Te verd 200g', sku: 'TE-0200', price: 6.2, stock: 120, active: true },
      { name: 'Llet ametla 1L', sku: 'LLE-ALM-1', price: 1.95, stock: 80, active: true }
    ]);
    console.log('Seed complet!');
    process.exit(0);
  } catch (err) {
    console.error(err);
    process.exit(1);
  }
})();
```

Executa:
```bash
npm run seed
```
 
### 6) Proves ràpides

```bash
# Crear
curl -X POST http://localhost:3000/api/v1/products   -H "Content-Type: application/json"   -d '{"name":"Tassa ceràmica","sku":"TAS-001","price":4.5,"stock":20}'

# Llistar (amb filtre)
curl "http://localhost:3000/api/v1/products?q=tassa&minPrice=3&maxPrice=10"

# Per ID (usa _id de Mongo)
curl http://localhost:3000/api/v1/products/<id>

# Actualitzar
curl -X PUT http://localhost:3000/api/v1/products/<id>   -H "Content-Type: application/json"   -d '{"price":4.9,"stock":30}'

# Ajust stock
curl -X PATCH http://localhost:3000/api/v1/products/<id>/stock   -H "Content-Type: application/json"   -d '{"delta": -2}'

# Eliminar
curl -X DELETE http://localhost:3000/api/v1/products/<id>
```
 
### 7) Bones pràctiques de persistència

- **Índexs**: assegura índex únic per a `sku` i text per a cerques.  
- **Validació a BD** (Mongoose) + **validació a API** (express-validator).  
- **Lean queries** (`.lean()`) per rendiment quan no necessites documents mutables.  
- **Paginació**: evita retornar milers de documents, usa `limit`/`skip`.  
- **DTOs**: controla camps retornats (`_id`, `__v`, etc.).  
- **Errors Mongo**: captura `code 11000` (duplicats) i `ValidationError`.

 
### 8) Exercicis (per entregar)

1. **Paginació**: `GET /products?page=1&limit=10` amb metadades (`total`, `pages`, `page`).
2. **Ordenació**: afegir `?sort=price,-name`.
3. **Camp nou `category`** amb índex i filtre `?category=...`.
4. **Esquema amb `minlength`/`maxlength`** i proves de validació 422.
5. **Endpoint `GET /products/export.csv`** generant CSV des de Mongo.
6. **Soft delete**: afegeix `deletedAt` i filtra per defecte elements no eliminats.
 
### 9) Troubleshooting

- **`MongoServerError: E11000 duplicate key error`** → `sku` duplicat. Respon `409`.
- **`CastError: Cast to ObjectId failed`** → ID no vàlid. Valida el format abans de la query.
- **`ValidationError`** → algun camp no compleix l’esquema. Respon `422` amb el missatge.
- **Sense connexió** → revisa `MONGO_URI`, firewall, i que el servei de Mongo estiga actiu.
 
 ## SA 6.4  Documentació amb Swagger / OpenAPI

En aquesta secció afegirem **documentació formal** a la nostra API amb **OpenAPI 3.0** i la servirem amb **Swagger UI** perquè siga navegable i executable des del navegador.
 

### 1) Arxiu `openapi.json` bàsic

A l’arrel del projecte crea `openapi.json`. A continuació tens una plantilla completa per al nostre recurs **Producte** amb esquemes, validacions i exemples.

> Pots copiar-ho tal qual i adaptar camps/operacions segons el teu projecte.

```json
{
  "openapi": "3.0.3",
  "info": {
    "title": "API Inventari 2DAW",
    "version": "1.0.0",
    "description": "API REST de Productes/Inventari documentada amb OpenAPI 3.0"
  },
  "servers": [
    { "url": "http://localhost:3000", "description": "Dev local" }
  ],
  "tags": [
    { "name": "Products", "description": "Gestió del catàleg de productes" }
  ],
  "paths": {
    "/api/v1/products": {
      "get": {
        "tags": ["Products"],
        "summary": "Llistar productes",
        "parameters": [
          { "name": "q", "in": "query", "schema": { "type": "string" }, "description": "Text de cerca a name o sku" },
          { "name": "active", "in": "query", "schema": { "type": "boolean" } },
          { "name": "minPrice", "in": "query", "schema": { "type": "number", "minimum": 0 } },
          { "name": "maxPrice", "in": "query", "schema": { "type": "number", "minimum": 0 } }
        ],
        "responses": {
          "200": {
            "description": "Llista de productes",
            "content": {
              "application/json": {
                "schema": { "type": "array", "items": { "$ref": "#/components/schemas/Product" } }
              }
            }
          }
        }
      },
      "post": {
        "tags": ["Products"],
        "summary": "Crear producte",
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": { "$ref": "#/components/schemas/ProductCreate" },
              "examples": {
                "basic": {
                  "summary": "Exemple bàsic",
                  "value": { "name": "Tassa ceràmica", "sku": "TAS-001", "price": 4.5, "stock": 20, "active": true }
                }
              }
            }
          }
        },
        "responses": {
          "201": { "description": "Creat", "content": { "application/json": { "schema": { "$ref": "#/components/schemas/Product" } } } },
          "409": { "description": "SKU duplicat" },
          "422": { "description": "Validació incorrecta" }
        }
      }
    },
    "/api/v1/products/{id}": {
      "get": {
        "tags": ["Products"],
        "summary": "Obtenir producte per ID",
        "parameters": [
          { "name": "id", "in": "path", "required": true, "schema": { "type": "string" } }
        ],
        "responses": {
          "200": { "description": "OK", "content": { "application/json": { "schema": { "$ref": "#/components/schemas/Product" } } } },
          "404": { "description": "No trobat" }
        }
      },
      "put": {
        "tags": ["Products"],
        "summary": "Actualitzar producte",
        "parameters": [
          { "name": "id", "in": "path", "required": true, "schema": { "type": "string" } }
        ],
        "requestBody": {
          "required": true,
          "content": { "application/json": { "schema": { "$ref": "#/components/schemas/ProductUpdate" } } }
        },
        "responses": {
          "200": { "description": "Actualitzat", "content": { "application/json": { "schema": { "$ref": "#/components/schemas/Product" } } } },
          "404": { "description": "No trobat" },
          "409": { "description": "SKU duplicat" }
        }
      },
      "delete": {
        "tags": ["Products"],
        "summary": "Eliminar producte",
        "parameters": [
          { "name": "id", "in": "path", "required": true, "schema": { "type": "string" } }
        ],
        "responses": {
          "204": { "description": "Eliminat" },
          "404": { "description": "No trobat" }
        }
      }
    },
    "/api/v1/products/{id}/stock": {
      "patch": {
        "tags": ["Products"],
        "summary": "Ajustar stock d'un producte",
        "parameters": [
          { "name": "id", "in": "path", "required": true, "schema": { "type": "string" } }
        ],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": { "schema": { "$ref": "#/components/schemas/StockPatch" } }
          }
        },
        "responses": {
          "200": { "description": "OK", "content": { "application/json": { "schema": { "$ref": "#/components/schemas/Product" } } } },
          "404": { "description": "No trobat" },
          "422": { "description": "Validació incorrecta" }
        }
      }
    }
  },
  "components": {
    "schemas": {
      "Product": {
        "type": "object",
        "properties": {
          "id":       { "type": "string", "description": "ID intern (o _id de Mongo)" },
          "name":     { "type": "string", "minLength": 2 },
          "sku":      { "type": "string", "pattern": "^[A-Z0-9-]+$" },
          "price":    { "type": "number", "minimum": 0 },
          "stock":    { "type": "integer", "minimum": 0 },
          "active":   { "type": "boolean", "default": true },
          "createdAt":{ "type": "string", "format": "date-time" },
          "updatedAt":{ "type": "string", "format": "date-time" }
        },
        "required": ["id", "name", "price", "stock", "active"]
      },
      "ProductCreate": {
        "type": "object",
        "properties": {
          "name":   { "type": "string", "minLength": 2 },
          "sku":    { "type": "string", "pattern": "^[A-Z0-9-]+$" },
          "price":  { "type": "number", "minimum": 0 },
          "stock":  { "type": "integer", "minimum": 0 },
          "active": { "type": "boolean" }
        },
        "required": ["name", "price", "stock"]
      },
      "ProductUpdate": {
        "allOf": [{ "$ref": "#/components/schemas/ProductCreate" }]
      },
      "StockPatch": {
        "type": "object",
        "properties": { "delta": { "type": "integer", "description": "Pot ser positiu o negatiu" } },
        "required": ["delta"]
      }
    }
  }
}
```

> 🔎 **Consell**: guarda aquest fitxer a l’arrel del projecte perquè siga fàcil de trobar i versionar.

 
### 2) Servir Swagger UI

Afegim Swagger UI a `app.js` (després de configurar les rutes).

```js
import swaggerUi from 'swagger-ui-express';
import { readFileSync } from 'node:fs';
import path from 'node:path';
import { fileURLToPath } from 'node:url';

const __filename = fileURLToPath(import.meta.url);
const __dirname = path.dirname(__filename);

// ...
const openapiPath = path.join(__dirname, '..', 'openapi.json');
const openapi = JSON.parse(readFileSync(openapiPath, 'utf-8'));
app.use('/api-docs', swaggerUi.serve, swaggerUi.setup(openapi));
```

Ara obri: **http://localhost:3000/api-docs**

 

### 3) Afegir exemples i respostes detallades

Els **exemples** ajuden l’alumnat a saber què enviar i què esperar:

```json
"requestBody": {
  "required": true,
  "content": {
    "application/json": {
      "schema": { "$ref": "#/components/schemas/ProductCreate" },
      "examples": {
        "valid": { "value": { "name":"Cafè gra 1kg", "sku":"CAF-1000", "price":12.5, "stock":50 } },
        "invalid": { "value": { "name":"", "price": -3, "stock": -1 } }
      }
    }
  }
}
```

També pots descriure **errors** amb esquemes (p. ex. per a 422):

```json
"422": {
  "description": "Validació incorrecta",
  "content": {
    "application/json": {
      "schema": {
        "type": "object",
        "properties": {
          "errors": { "type": "array", "items": { "type": "object" } }
        }
      }
    }
  }
}
```

 
### 4) Bones pràctiques de documentació

- **Mantín sincronitzat** el que diu `openapi.json` amb la realitat del codi.
- **Descripcions clares**: explica què fa cada endpoint i quins casos d’ús té.
- **Nomena** correctament (recursos en plural, verbs en mètodes, `id` al path).
- **Exemples** reals i útils (no genèrics).
- **Versiona** l’API: `/api/v1/...` i reflecteix-ho a `servers`.
- **DRY amb `components`**: posa esquemes reutilitzables allí.
- **Respostes**: documenta les principals (`200`, `201`, `204`, `400/404/409/422`, `500`).

 
### 5) Exercicis (per entregar)

1. **Completa `openapi.json`** amb:  
   a) Resposta `400` per `id` mal format.  
   b) `examples` detallats per `PUT` i `PATCH /stock`.  
   c) Descripció de paràmetres de filtrat a `GET /products`.

2. **Afig `category`** al `schema Product` i actualitza `ProductCreate` i `ProductUpdate`.

3. **Camps de resposta**: crea un `schema Error` comú i reutilitza’l en respostes 4xx/5xx.

4. **Endpoint nou**: documenta `GET /api/v1/products/export.csv` (tipus `text/csv`).

5. **Autenticació (bonus)**: afegeix `securitySchemes` (Bearer JWT) i marca `POST/PUT/PATCH/DELETE` com a protegits.

 
### 6) Troubleshooting Swagger

- **Pantalla en blanc** a `/api-docs` → JSON mal format (valida’l en un JSON linter).  
- **No carrega `openapi.json`** → rutes relatives: comprova la ruta `path.join(__dirname, '..', 'openapi.json')`.  
- **Errors CORS** provant des de Swagger → assegura `app.use(cors())`.  
- **Exemples no apareixen** → han d’estar dins de `content -> application/json -> examples`.

### 7) Swagger automàtic amb swagger-jsdoc  

Anem també a mostrar com **generar la documentació OpenAPI automàticament** a partir de **comentaris JSDoc** en les rutes d’Express, utilitzant **swagger-jsdoc** + **swagger-ui-express**.

#### 1) Instal·lació
```bash
npm i swagger-jsdoc swagger-ui-express
```

#### 2) Configuració base
**`src/swagger.js`**
```js
import swaggerJSDoc from 'swagger-jsdoc';

const options = {
  definition: {
    openapi: '3.0.3',
    info: {
      title: 'API Inventari 2DAW',
      version: '1.1.0',
      description: 'Documentació automàtica des de JSDoc'
    },
    servers: [{ url: 'http://localhost:3000' }],
  },
  apis: ['./src/routes/*.js'], // fitxers amb comentaris JSDoc
};

export const swaggerSpec = swaggerJSDoc(options);
```

**`src/app.js`**
```js
import swaggerUi from 'swagger-ui-express';
import { swaggerSpec } from './swagger.js';

app.use('/api-docs', swaggerUi.serve, swaggerUi.setup(swaggerSpec));
```

#### 3) Comentaris JSDoc a les rutes
**`src/routes/products.routes.js`**
```js
/**
 * @openapi
 * /api/v1/products:
 *   get:
 *     tags: [Products]
 *     summary: Llistar productes
 *     parameters:
 *       - in: query
 *         name: q
 *         schema: { type: string }
 *       - in: query
 *         name: active
 *         schema: { type: boolean }
 *     responses:
 *       200: { description: Llista de productes }
 */
router.get('/', validate(listQueryRules), controller.list);
```

#### 4) Components reutilitzables
Pots definir **components** (schemas) en `swaggerSpec` (via `options.definition.components = {...}`) o incloure’ls en un fitxer `.yml` separat i combinar-los amb `swagger-jsdoc`.

#### 5) Bones pràctiques
- Posa **tags** per agrupar endpoints.
- Escriu **exemples** a `requestBody` i `responses`.
- Mantín el **contracte** sincronitzat. Si canvies una ruta, actualitza el JSDoc.
- Valida amb un **validator OpenAPI** (ex. Swagger Editor) si afegeixes elements avançats.

#### 6) Enllaç a la UI
Amb el servidor en marxa:  
**http://localhost:3000/api-docs**

## SA 6.5 – Pràctiques guiades, reptes oberts i rúbrica d’avaluació

Aquesta secció recull una sèrie d’activitats perquè l’alumnat consolide els coneixements adquirits i demostre la seua competència en el desenvolupament d’APIs amb Node.js, Express, MongoDB i Swagger.

 
### 🧪 1. Pràctiques guiades  

 
#### 🧪 Pràctica 1 – Afegir paginació i ordenació

- Endpoint: `GET /api/v1/products`
- Objectiu: implementar `?page`, `?limit` i `?sort` (acceptant `price`, `name`, `-price`...).
- Ex.: `GET /api/v1/products?page=2&limit=5&sort=-price`

**Criteris clau:**
- Retornar metadades (`total`, `page`, `pages`, `limit`)
- Ordenació ascendent i descendent
- Validació d’entrada (`limit` > 0, etc.)
 

#### 🧪 Pràctica 2 – Exportació de dades

- Endpoint: `GET /api/v1/products/export.csv`
- Objectiu: generar un fitxer CSV amb tots els productes (nom, sku, preu, stock, actiu).

**Criteris clau:**
- Capçalera `Content-Type: text/csv`
- Nom de fitxer amb data (`products-2025-10-15.csv`)
- Compatibilitat amb Excel / LibreOffice
 

#### 🧪 Pràctica 3 – Camp nou i filtrat avançat

- Afig un camp `category` al model de producte.  
- Permet filtrar per `?category=bebidas` en el `GET /products`.

**Criteris clau:**
- Actualitzar `ProductCreate` i `ProductUpdate`
- Validar categories vàlides (`alimentació`, `begudes`, `altres`)
- Índex de cerca per `category`

 
#### 🧪 Pràctica 4 – Soft delete

- Objectiu: implementar un sistema de *soft delete* amb un camp `deletedAt`.  
- Els productes eliminats **no s’esborren**, només s’oculten per defecte.

**Criteris clau:**
- `DELETE /products/:id` → afegeix `deletedAt`
- `GET /products` → exclou elements amb `deletedAt`
- `GET /products?includeDeleted=true` → inclou tots

 
#### 🧪 Pràctica 5 – Validacions avançades i missatges personalitzats

- Objectiu: reforçar la seguretat i robustesa de l’API.
- Requisits:
  - Nom mínim 3 caràcters i màxim 50
  - SKU únic i format `[A-Z0-9-]+`
  - Stock ≤ 10.000
  - Missatges de validació personalitzats

 
### 💡 2. Reptes oberts  

 
#### 💡 Repte 1 – API de biblioteca

- Recursos: `Books`, `Authors`
- Operacions: CRUD complet, filtrat per autor, gènere, any.
- Extres: endpoint per a llibres disponibles / prestats.

**Objectius:** relacions entre col·leccions, validació, rutes RESTful.

 
#### 💡 Repte 2 – API de comandes d’una botiga

- Recursos: `Products`, `Orders`, `Customers`
- Requisits: crear comandes amb productes, calcular total automàticament.
- Extres: endpoint `GET /orders/stats` amb vendes totals per mes.

**Objectius:** relacions 1:N i N:M, agregacions, validacions complexes.
 
#### 💡 Repte 3 – API de notes d’alumnes

- Recursos: `Students`, `Grades`, `Subjects`
- Funcions: CRUD, càlcul mitjanes automàtiques, filtrat per curs.
- Extres: `GET /students/honor-roll` → alumnes amb mitjana > 9.

**Objectius:** càlculs dinàmics i endpoints derivats.

 

#### 💡 Repte 4 – API de tasques i projectes

- Recursos: `Projects`, `Tasks`, `Users`
- Funcions: assignar tasques a usuaris, canviar estat (`pending`, `done`...).
- Extres: endpoint per a percentatge de completat.

**Objectius:** disseny d’estructura, lògica de negoci i documentació.
 
#### 💡 Repte 5 – API d’esdeveniments culturals

- Recursos: `Events`, `Venues`, `Tickets`
- Funcions: CRUD complet, consulta d’entrades disponibles, aforament.
- Extres: `GET /events/next` → pròxims 10 esdeveniments.

**Objectius:** combinar múltiples recursos i treballar amb dates.
 

### 📊 3. Rúbrica d’avaluació de projecte final

| Criteri | Insuficient (0-4) | Bé (5-6) | Notable (7-8) | Excel·lent (9-10) |
|--------|--------------------|----------|---------------|--------------------|
| **Estructura del projecte** | Desorganitzada o incompleta | Correcta però poc modular | Bona organització, separació clara de capes | Excel·lent arquitectura, escalable i neta |
| **Rutes i mètodes REST** | Incomplets o incorrectes | Complets però amb errors | Complets i ben implementats | Complets, correctes i amb bones pràctiques REST |
| **Validacions i errors** | Inexistents o incorrectes | Presenten algunes mancances | Completes i adequades | Exhaustives, missatges clars i validacions avançades |
| **Lògica i funcionalitat** | Errors greus o incompliment de requisits | Funcionalitat bàsica | Funcionalitat completa i correcta | Lògica avançada, càlculs i relacions complexes |
| **Persistència i dades** | No persistent o mal implementada | Persistència funcional però limitada | Persistència completa i correcta | Persistència òptima amb índexs, agregacions i rendiment |
| **Documentació Swagger** | Inexistent o incompleta | Present però amb mancances | Completa i actualitzada | Excel·lent, detallada, amb exemples i components reutilitzats |
| **Proves i robustesa** | No s’han fet proves | Proves mínimes | Proves completes i correctes | Proves exhaustives i cobertura de casos límit |
| **Originalitat i creativitat** | Poc treball o còpia literal | Adaptació bàsica del projecte guia | Adaptació creativa amb millores | Projecte original, amb funcionalitats pròpies i innovadores |

 
### 📁 4. Recomanacions finals per al projecte

- 🧠 **Planificació**: defineix recursos, endpoints i esquemes abans de començar a programar.  
- 📚 **Documentació**: escriu `openapi.json` a mesura que avances, no al final.  
- 🧪 **Proves constants**: utilitza Postman o Thunder Client per validar cada endpoint.  
- 📦 **Commits freqüents**: versiona els canvis i escriu missatges clars.  
- 🚀 **Millora contínua**: afegeix funcionalitats addicionals si el projecte base ja funciona.

 