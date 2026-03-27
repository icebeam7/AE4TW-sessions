# Step 5: Create and Initialize the SQLite Database

In this step, you will create a SQLite database file (`src/db/data.db`) by implementing a small initialization step (`src/db.js`) that creates tables if they don’t exist.

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

   **References**:
   - [SQLite tutorial with Node.js](https://www.sqlitetutorial.net/sqlite-nodejs/)

2. Call the Module in `src/index.js`:
   - Ensure the database connection is established.

3. Start the Server and Verify:
   - When the server starts, ensure the `.db` file appears in your `src/db` folder.
   - Confirm that the tables are created successfully.

[< Previous Step](step4.md) | Step 5 | [Next Step >](step6.md)