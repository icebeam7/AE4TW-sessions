# Step 6: Implement CRUD for Items (Start Without Auth)

> Review the references listed below to complete this step.

## Behaviors to Implement

### **GET /items**
- Return an array of items (possibly empty).

### **GET /items/:id**
- Return `404` if the item does not exist.

### **POST /items**
- Validate the `name` field.
- Return `201` on success.

### **PUT /items/:id**
- Validate the `name` field.
- Return `404` if the item does not exist.

### **DELETE /items/:id**
- Return `404` if the item does not exist.
- Return `204` on success.

1. Implement these endpoints in `src/routes/items.js`:
    - You need a connection to the database to implement each behavior.
    - Create an `express.Router`, define each behavior using the `http` methods (`get`, `post`, etc.)
    - Export the object as a module using `export default`.

> Sample code for `get` all items and `post` for creating an item:

```javascript
router.get("/", async (req, res) => {
  const db = get_db();

  const query = "SELECT id, name, description, owner_user_id, created_at FROM items ORDER BY id DESC";

  await db.all(query, 
    function(err, items) {
        if (err) {
            console.error(err);
            return res.status(500).json({ error: `Database error ${err.message}` });
        }

        console.log(`Retrieved ${items.length} items`);
        return res.status(200).json(items);
    });
});

router.post("/", async (req, res) => {
  const { name, description } = req.body || {};
  if (!name) return res.status(400).json({ error: "name required" });

  const db = get_db();
  const query = "INSERT INTO items (name, description, owner_user_id) VALUES (?, ?, ?)";

  await db.run(query, 
    [name, description || null, 1 /*req.user.id*/], 
    async function(err) {
        if (err) {
            console.error(err);
            return res.status(500).json({ error: `Database error ${err.message}` });
        }

        console.log(`Inserted item with ID ${this.lastID}`);

        const created = await get_by_id(db, req.params.id);
        return res.status(201).json(created);
    });
});
```

> `get_by_id` is a function that allows you to get an item by its id. Here is its code:

```javascript
const query_get_item_by_id = "SELECT id, name, description, owner_user_id, created_at FROM items WHERE id = ?"; 

function get_by_id(db, id) {
    return new Promise((resolve, reject) => {
        db.get(query_get_item_by_id, id, (err, item) => {
            if (err) {
                console.error(err);
                return reject(new Error(`Database error ${err.message}`));
            }
            resolve(item);
        });
    });
}
```

2. In `src/index.js`, load the router module in the app. Mount the item routes under `/items`.

3. Test CRUD operations using `Postman` (temporarily without auth) or the `Thunder Client` VS Code extension. Click on each element below to see the demonstration of the corresponding endpoint.

<details>
    <summary>Add an item</summary>
    <img width="1036" height="1628" alt="image" src="https://github.com/user-attachments/assets/61f4ca0d-7042-4026-98ff-5b22a1e3c53e" />
</details>

<details>
    <summary>Get all items</summary>
    <img width="1036" height="1628" alt="image" src="https://github.com/user-attachments/assets/c0664aae-41d6-4156-9e40-3ffac2340e8f" />
</details>

<details>
    <summary>Update an item</summary>
    <img width="1122" height="1628" alt="image" src="https://github.com/user-attachments/assets/41da8f72-ca97-466e-87df-89e4da5f1d79" />
</details>

<details>
    <summary>Get an item by ID</summary>
    <img width="1122" height="1628" alt="image" src="https://github.com/user-attachments/assets/9d557ca0-5828-4ef5-8f66-62df990d0e14" />
</details>

<details>
    <summary>Delete an item</summary>
    <img width="1122" height="1628" alt="image" src="https://github.com/user-attachments/assets/5b2d8952-f1c7-4f45-b16c-3bd3773daa80" />
</details>

## References
- [Express Routing Guide](https://expressjs.com/en/guide/routing.html)
- [SQLite Node.js: Querying Data](https://www.sqlitetutorial.net/sqlite-nodejs/query/)
- [SQLite Node.js: Inserting Data Into a Table](https://www.sqlitetutorial.net/sqlite-nodejs/insert/)
- [SQLite Node.js: Updating Data](https://www.sqlitetutorial.net/sqlite-nodejs/update/)
- [SQLite Node.js: Deleting Data](https://www.sqlitetutorial.net/sqlite-nodejs/delete/)

<details>

<summary>Solution</summary>

`src/routes/items.js`:

```javascript
import express from "express";
import { get_db } from "../db.js";

const query_get_item_by_id = "SELECT id, name, description, owner_user_id, created_at FROM items WHERE id = ?"; 

function get_by_id(db, id) {
    return new Promise((resolve, reject) => {
        db.get(query_get_item_by_id, id, (err, item) => {
            if (err) {
                console.error(err);
                return reject(new Error(`Database error while retrieving item by ID ${id}: ${err.message}`));
            }
            resolve(item);
        });
    });
}

const router = express.Router();

router.get("/", async (req, res) => {
  const db = get_db();

  const query = "SELECT id, name, description, owner_user_id, created_at FROM items ORDER BY id DESC";

  await db.all(query, 
    function(err, items) {
        if (err) {
            console.error(err);
            return res.status(500).json({ error: `Database error while retrieving items: ${err.message}` });
        }

        console.log(`Retrieved ${items.length} items`);
        return res.status(200).json(items);
    });
});

router.get("/:id", async (req, res) => {
  const db = get_db();

  const item = await get_by_id(db, req.params.id);
  if (!item) return res.status(404).json({ error: "Not found" });
  return res.json(item);        
});

router.post("/", async (req, res) => {
  const { name, description } = req.body || {};
  if (!name) return res.status(400).json({ error: "name required" });

  const db = get_db();
  const query = "INSERT INTO items (name, description, owner_user_id) VALUES (?, ?, ?)";
  
  await db.run(query, 
    [name, description || null, 1 /*req.user.id*/], 
    async function(err) {
        if (err) {
            console.error(err);
            return res.status(500).json({ error: `Database error while inserting item: ${err.message}` });
        }

        console.log(`Inserted item with ID ${this.lastID}`);

        const created = await get_by_id(db, this.lastID);
        return res.status(201).json(created);
    });
});

router.put("/:id", async (req, res) => {
  const { name, description } = req.body || {};
  if (!name) return res.status(400).json({ error: "name required" });

  const db = get_db();

  const existing = await get_by_id(db, req.params.id);

  if (!existing) 
    return res.status(404).json({ error: "Not found" });
  
  const query_update = "UPDATE items SET name = ?, description = ? WHERE id = ?";

  await db.run(query_update, 
    [name, description || null, req.params.id], 
    function(err) {
        if (err) {
            console.error(err);
            return res.status(500).json({ error: `Database error while updating item with ID ${req.params.id}: ${err.message}` });
        }

        console.log(`Updated item with ID ${req.params.id}`);
        return res.status(204).send();
  });
});

router.delete("/:id", async (req, res) => {
  const db = get_db();
  const existing = await get_by_id(db, req.params.id);

  if (!existing) 
    return res.status(404).json({ error: "Not found" });

  const query_delete = "DELETE FROM items WHERE id = ?";

  await db.run(query_delete, 
    [req.params.id], 
    function(err) {
        if (err) {
            console.error(err);
            return res.status(500).json({ error: `Database error while deleting item with ID ${req.params.id}: ${err.message}` });
        }

        console.log(`Deleted item with ID ${req.params.id}`);
        return res.status(204).send();
  });
});

export default router;
```

`src/index.js`:

```javascript
import { db_initialize_create } from "./db.js";
import itemRoutes from "./routes/items.js";
import express from "express";
import dotenv from 'dotenv'
dotenv.config()

const app = express()
app.use(express.json());

const port = process.env.PORT || 3000
//const jwtSecret = process.env.JWT_SECRET;

app.use("/items", itemRoutes);

app.get("/health", (req, res) => res.json({ status: "ok" }));

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
  //console.log(`Using JWT secret: ${jwtSecret}`);
})

db_initialize_create().then(() => {
  console.log("DB initialized and tables created");
});
```

</details>


[< Previous Step](step5.md) | Step 6 | [Next Step >](step7.md)
