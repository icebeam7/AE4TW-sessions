# Step 7: Implement Signup (Store Hashed Passwords)

> Review the references listed below to complete this step.

1. Implement `POST /auth/signup` endpoint in a new file: `src/routes/auth.js`.
  - Validate input `{ email, password }`.
  - Hash the password using `bcryptjs`.
  - Insert the user into the `users` table.
  - If the email already exists, return HTTP `409`.

2. In `src/index.js`, mount the auth routes under `/auth`.

3. Test the Endpoint: Ensure signing up returns a new user ID.

<img width="1094" height="1548" alt="image" src="https://github.com/user-attachments/assets/bf06d6ea-e53d-4c2c-a526-2593c6258335" />

4. Verify the database: Open the database and check that the password is stored as a hash value rather than plaintext.

<img width="1514" height="340" alt="image" src="https://github.com/user-attachments/assets/6def30b1-85b2-4a87-9d36-07d55ce44f79" />

## References
- [bcryptjs npm package](https://www.npmjs.com/package/bcryptjs)
- [How to Handle Passwords Safely with BcryptsJS in JavaScript](https://www.digitalocean.com/community/tutorials/how-to-handle-passwords-safely-with-bcryptsjs-in-javascript)
- [Building a Secure Login System with Node.js, bcrypt, and JWT Authentication](https://medium.com/@svk19998/building-a-secure-login-system-with-node-js-bcrypt-and-jwt-authentication-b3e5b25de218)


<details>

<summary>Solution</summary>

`src/routes/auth.js`:

```javascript
import express from "express";
import { get_db } from "../db.js";
import bcryptjs from "bcryptjs";
import jwt from "jsonwebtoken";
import dotenv from 'dotenv'
dotenv.config()

const error_email_exists = "Email already exists";

async function create_user(db, email, password) {
    return new Promise((resolve, reject) => {
        const query_check_email = "SELECT id FROM users WHERE email = ?";

        db.get(query_check_email, email, async (err, existing) => {
            if (err) {
                console.error(err);
                return reject(new Error(`Database error while checking existing email: ${err.message}`));
            }
            
            if (existing) {
                return reject(new Error(error_email_exists));
            }

            const password_hash = await bcryptjs.hash(password, 10);
            const query_insert = "INSERT INTO users (email, password_hash) VALUES (?, ?)";
            
            db.run(query_insert, [email, password_hash], function(err) {
                if (err) {
                    console.error(err);
                    return reject(new Error(`Database error while inserting user: ${err.message}`));
                }

                console.log(`Inserted user with ID ${this.lastID}`);

                const created_user = {
                    id: this.lastID,
                    email
                };

                resolve(created_user);
            });
        });
    });
}

const router = express.Router();

router.post("/signup", async (req, res) => {
    const { email, password } = req.body || {};
    
    if (!email || !password) {
        return res.status(400).json({ error: "email and password required" });
    }

    const db = get_db();

    try {
        const user = await create_user(db, email, password);
        return res.status(201).json({ id: user.id, email: user.email });
    } catch (err) {
        if (err.message === error_email_exists) {
            return res.status(409).json({ error: err.message });
        }

        return res.status(500).json({ error: err.message });
    }
});

export default router;
```

`src/index.js`:

```javascript
import { db_initialize_create } from "./db.js";
import itemRoutes from "./routes/items.js";
import authRoutes from "./routes/auth.js";
import express from "express";
import dotenv from 'dotenv'
dotenv.config()

const app = express()
app.use(express.json());


const port = process.env.PORT || 3000
//const jwtSecret = process.env.JWT_SECRET;

app.use("/items", itemRoutes);
app.use("/auth", authRoutes);

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

  
[< Previous Step](step6.md) | Step 7 | [Next Step >](step8.md)
