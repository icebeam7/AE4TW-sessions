## Preparing the Tests

We have manually evaluated that some of the endpoints work. This is time-consuming, especially if you have lots of endpoints and want to evaluate several cases, such as edge case scenarios (non-existing users, no JWT token) or successful ones (user creation, etc).

1. Add two new dependencies: `test` and `supertest` by running `npm install --save-dev jest supertest @jest/globals` command:

<img width="670" height="227" alt="Screenshot 2026-05-14 at 6 02 56" src="https://github.com/user-attachments/assets/edb75ac5-42bb-4c56-8a61-ecafc70dd0d6" />

**Supertest** is a highly efficient and flexible testing library designed for testing HTTP assertions. Working hand in hand with frameworks like **Express.js**, Supertest makes it easy to write assertions for your APIs, ensuring they respond as expected. 

Coupled with **Jest**, a JavaScript Testing Framework with a focus on simplicity, you can ensure that your APIs are robust and reliable.

2. Before we actually write our first test, refactor the `src/db.js` script by defining constants for the database name, directory and schema (strings). Replace the content of `src/db.js` with the following content:

```javascript
import sqlite3 from "sqlite3";
import path from "path";

const __dirname = import.meta.dirname;
const default_db_filename = path.join(__dirname, "db", "data.db");

let db;

const schema_sql = `
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
    created_at TEXT NOT NULL DEFAULT (datetime('now')),
    FOREIGN KEY (owner_user_id) REFERENCES users(id) ON DELETE SET NULL
  );
`;


// initialize db and create tables
export const db_initialize_create = async (filename = default_db_filename) => {
  if (db) {
    await close_db();
  }

  return new Promise((resolve, reject) => {
    const created_db = new sqlite3.Database(filename, (open_err) => {
      if (open_err) {
        return reject(new Error(`Database open error: ${open_err.message}`));
      }

      created_db.exec(schema_sql, (schema_err) => {
        if (schema_err) {
          return reject(new Error(`Database schema initialization error: ${schema_err.message}`));
        }

        db = created_db;
        resolve(db);
      });
    });
  });
};

export const close_db = async () => {
  if (!db) return;

  const current_db = db;
  db = null;

  return new Promise((resolve, reject) => {
    current_db.close((err) => {
      if (err) {
        return reject(new Error(`Database close error: ${err.message}`));
      }
      resolve();
    });
  });
};

export const get_db = () => {
  if (!db) throw new Error("DB not initialized. Call db_initialize_create() first.");
  return db;
};
```

[< Previous Step](step1.md) | Step 2 | [Next Step >](step3.md)
