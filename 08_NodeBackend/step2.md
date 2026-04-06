# Step 2: Project Initialization

In this step, you will create a **Node.js project** and install the required dependencies.

## Instructions

1. Initialize the project:

```bash
npm init -y
```

2. Install production dependencies:

```bash
npm install express sqlite3 jsonwebtoken bcryptjs dotenv cors
```

3. Install the development dependency:

```bash
npm install nodemon --save-dev
```

## Dependency Purpose

- **express**: HTTP server and routing.
- **sqlite3**: SQLite database driver.
- **dotenv**: Loads environment variables from a `.env` file.
- **bcryptjs**: Password hashing and verification.
- **jsonwebtoken**: JWT creation and validation.
- **cors**: Enables cross-origin requests.
- **nodemon** (dev dependency): Automatically restarts the server when files change during development.

## References

- Express: https://expressjs.com/
- sqlite3: https://www.npmjs.com/package/sqlite3
- dotenv: https://www.npmjs.com/package/dotenv
- bcryptjs: https://www.npmjs.com/package/bcryptjs
- jsonwebtoken: https://www.npmjs.com/package/jsonwebtoken
- cors: https://www.npmjs.com/package/cors
- nodemon: https://www.npmjs.com/package/nodemon

## Update package.json

4. Add or update the `scripts` section in `package.json`:

  ```json
  "scripts": {
    "start": "nodemon src/index.js"
  }
  ```

Purpose: This lets you run the backend in development mode with automatic reload using `npm run dev`.
> NOTE: If you want to keep the `test` script, add a comma at the end of the `start` script.

5. Add the type module to use the ES module:

  ```json
  "type": "module",
  ```

6. Finally, create the following folders: 

- `src` 
- `src/db`
- `src/routes`
- `src/middleware`

[< Previous Step](step1.md) | Step 2 | [Next step >](step3.md)
