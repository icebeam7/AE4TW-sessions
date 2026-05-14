## Configuring the field for testing

1. In your root path, create a new file, `jest.config.js`. This file is a Jest configuration module written in JavaScript using ESM syntax (export default). It tells Jest how to run tests in the project.
  
2. Add the following content to the file:

```javascript
export default {
  testEnvironment: "node",
  testMatch: ["**/test/**/*.test.js"],
};
```

The `testEnvironment: "node"` setting makes Jest execute tests in a Node.js runtime instead of a browser-like environment. This is appropriate for backend/API projects because Node globals and server-side behavior are expected.

The `testMatch: ["**/test/**/*.test.js"]` pattern defines which files Jest should treat as tests. It means Jest will look for any `.test.js` file inside the test folder (and its subfolders) anywhere in the project. This keeps test discovery explicit and organized around a dedicated test directory.

3. In your root path, create a new folder `test` and add a new file, `items.test.js`. When we run the test, Jest will identify it because of the configuration pattern that we have just defined.

4. Import the following elements in `items.test.js`:

```javascript
import { describe, it, expect, beforeAll, afterAll } from "@jest/globals";
import request from "supertest";
import express from "express";
import { db_initialize_create, close_db } from "../src/db.js";
import itemRoutes from "../src/routes/items.js";
import authRoutes from "../src/routes/auth.js";
```

- We are importing Jest’s global test functions (`describe, it, expect, beforeAll, afterAll`) from `@jest/globals`, which is common in ESM projects so test structure and assertions are explicitly available without relying on implicit globals.
- We also import `supertest` and `express` to build and test an HTTP server in memory.
- We also bring the database helpers and the route modules we created in another tutorial.

5. Next, add the following code to define a stable test runtime by building an Express app instance that uses the `PORT` and `JWT_SECRET` environment variables: 

```javascript
process.env.JWT_SECRET = process.env.JWT_SECRET ?? "test-jwt-secret";
process.env.PORT = process.env.PORT ?? 3000;

function buildApp() {
  const app = express();
  app.set("port", process.env.PORT);
  app.use(express.json());
  app.use("/items", itemRoutes);
  app.use("/auth", authRoutes);
  return app;
}
```

The `buildApp()` function is an app factory. It creates a new `Express` application, stores the port setting, enables JSON request parsing with `express.json()`, and mounts two route groups: 
- `/items` for CRUD endpoints
- `/auth` for authentication endpoints.

Returning the `app` from a function makes tests cleaner and more isolated, because each test setup can construct the same API surface in a controlled way without starting a real network server.

6. Define the following **test helpers**:

```javascript
async function signupUser(app, email, password = "password123") {
  return request(app).post("/auth/signup").send({ email, password });
}

async function loginUser(app, email, password = "password123") {
  return request(app).post("/auth/login").send({ email, password });
}

function authHeader(token) {
  return { Authorization: `Bearer ${token}` };
}

async function createItem(app, token, payload) {
  return request(app).post("/items").set(authHeader(token)).send(payload);
}
```

Explanation:
- The test helpers will reduce repetition when calling authentication-protected endpoints. Instead of rebuilding request details in every test case, each helper centralizes one common action (signup, login, auth header creation, or item creation). This makes tests easier to read and maintain.

- `request` is a `Supertest` function that accepts an Express app instance in order to send later an **HTTP request** (such as `post`, as can be seen in 3 out of 4 above methods).

- All methods except `authHeader(token)` return a `supertest` request promise, so tests can await it and assert status codes or response body data.

- `authHeader(token)` builds the `Authorization` header object expected by bearer-token auth middleware. 

[< Previous Step](step1.md) | Step 2 | [Next Step >](step3.md)
