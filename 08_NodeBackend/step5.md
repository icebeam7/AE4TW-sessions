# Step 5: Create and Initialize the SQLite Database

In this step, you will create a SQLite database file (`src/db/data.db`) by implementing a small initialization step (`src/db.js`) that creates tables if they don’t exist.

> Review the references listed below to complete this step.

## Create Tables
You will create two tables:

### Users Table (`users`)
- `id` (integer primary key)
- `email` (text unique, not null)
- `password_hash` (text, not null)
- `created_at` (timestamp)

### Items Table (`items`)
- `id` (integer primary key)
- `name` (text, not null)
- `description` (text)
- `created_at` (timestamp)
- `owner_user_id` (integer)

## Instructions

1. Implement a DB Module (`src/db.js`):
   - Open the database.
   - Run schema creation.
   - Exports helper functions to run queries.

> Define the helper functions like this:

```javascript
// ... rest of your code
import path from "path";

const __dirname = import.meta.dirname;
let db;

// initialize db and create tables
export const db_initialize_create = async () => {
  let filename = path.join(__dirname, "db", "data.db");
  // rest of your code...

  return db;
}

export const get_db = () => {
  if (!db) throw new Error("DB not initialized. Call db_initialize_create() first.");
  return db;
}
```

2. Call the Module in `src/index.js`:
   - Ensure the database connection is established.

```javascript
import { db_initialize_create } from "./db.js";
// rest of your code...

db_initialize_create().then(() => {
  console.log("DB initialized and tables created");
});
```

3. Start the Server and verify:
   - When the server starts, ensure the `.db` file appears in your `src/db` folder.
   - Confirm that the tables are created successfully (a new `data.db` file should appear in the `src/db` folder).

<img width="1574" height="534" alt="image" src="https://github.com/user-attachments/assets/e2bc68af-036d-44b7-983f-bae10fcf1704" />

4. Press `Ctrl-C` to stop the server.

5. You can connect to the database by entering the following command in the terminal:

```
sqlite3 src/db/data.db   
```

6. Once connected to the database, use the command `.tables` to list the database tables. 

7. You can also view the table schema with the `.schema` command (it requires the name of the table).

8. Disconnect from the database with the `.quit` command.

<img width="914" height="434" alt="image" src="https://github.com/user-attachments/assets/77f0e5b1-e747-4e6f-9d0d-db03b4f15abe" />

**References**:
- [SQLite tutorial with Node.js](https://www.sqlitetutorial.net/sqlite-nodejs/)
   - [SQLite Node.js: Connecting to a SQLite Database](https://www.sqlitetutorial.net/sqlite-nodejs/connect/)
   - [SQLite Node.js: Creating Tables](https://www.sqlitetutorial.net/sqlite-nodejs/create-tables/)

<details>

<summary>Solution</summary>

`src/db.js`:

```javascript
import sqlite3 from "sqlite3";
import path from "path";

const __dirname = import.meta.dirname;

let db;

// initialize db and create tables
export const db_initialize_create = async () => {
  let filename = path.join(__dirname, "db", "data.db");
  db = new sqlite3.Database(filename);

  await db.exec(`
    PRAGMA foreign_keys = ON;

    CREATE TABLE IF NOT EXISTS users (
      id INTEGER PRIMARY KEY AUTOINCREMENT,
      email TEXT NOT NULL UNIQUE,
      password_hash TEXT NOT NULL,
      created_at TEXT NOT NULL DEFAULT (datetime('now'))
    );

    CREATE TABLE IF NOT EXISTS items (
      id INTEGER PRIMARY KEY AUTOINCREMENT,
      name TEXT NOT NULL,
      description TEXT,
      owner_user_id INTEGER,
      created_at TEXT NOT NULL DEFAULT (datetime('now'))
    );
  `);

  return db;
}

export const get_db = () => {
  if (!db) throw new Error("DB not initialized. Call db_initialize_create() first.");
  return db;
}
```

`src/index.js`:

```javascript
import { db_initialize_create } from "./db.js";
import express from "express";
import dotenv from 'dotenv'
dotenv.config()

const app = express()
app.use(express.json());

const port = process.env.PORT || 3000
//const jwtSecret = process.env.JWT_SECRET;

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


[< Previous Step](step4.md) | Step 5 | [Next Step >](step6.md)
