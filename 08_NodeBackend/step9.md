# Step 9 — Add JWT Middleware and Protect Routes

> Review the references listed below to complete this step. 

1. Create Middleware: `requireAuth` in `src/routes/auth.js`.
- Read the `Authorization` header in the format:
```http
Authorization: Bearer <token>
```

- Verify the token using `JWT_SECRET`.

- Add the following object to the `req` object upon successful verification:
```javascript
req.user = {
 id: "<user_id>",
 email: "<user_email>"
};
```

- Return a `401 Unauthorized` response on failure.

2. Protect the Following Routes:
- `POST /items` (and make sure to pass `req.user.id` instead of `1` as argument for `owner_user_id` when running the query).
- `PUT /items/:id` 
- `DELETE /items/:id` 

3. Test the protected endpoints without a valid token: Ensure that protected endpoints return a `401 Unauthorized` response when accessed without a valid token.

<img width="1058" height="830" alt="image" src="https://github.com/user-attachments/assets/782c99ec-0aec-49e6-8c99-39483d780e29" />

4. Test the protected endpoints using a valid token: Ensure that protected endpoints work as expected and provide a valid response when accessed using a valid token.
- First, you need to sign in using the `login` endpoint. This way, you get a valid token.
<img width="1088" height="862" alt="image" src="https://github.com/user-attachments/assets/0cf67462-1e95-440a-a1e8-68e0aa10ade6" />

- Then, copy the token value and paste it using the `Bearer` token authentication. 

<img width="1088" height="994" alt="image" src="https://github.com/user-attachments/assets/82a99d7d-9543-473b-b6ef-f294a5628636" />


## References

- [Authorization Header (Bearer)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Authorization)
- [Express Middleware](https://expressjs.com/en/guide/using-middleware.html)
- [Protecting Routes with JWT Middleware in Node.js](https://www.guvi.in/blog/protecting-routes-with-jwt-middleware-in-node-js/)

<details>

<summary>Solution</summary>

`src/routes/auth.js`:

```javascript
// add this before export default router;

export function requireAuth(req, res, next) {
    const authHeader = req.headers.authorization;
    if (!authHeader || !authHeader.startsWith("Bearer ")) {
        return res.status(401).json({ error: "Authorization header missing or malformed" });
    }

    const token = authHeader.split(" ")[1];
    try {
        const decoded = jwt.verify(token, process.env.JWT_SECRET);
        console.log(`JWT verified successfully for user ID ${decoded.sub}`);
        req.user = { id: decoded.sub, email: decoded.email };
        next();
    } catch (err) {
        console.error("JWT verification failed:", err);
        return res.status(401).json({ error: "Invalid or expired token" });
    }
}

// rest of your code
```

`src/routes/items.js`:

```javascript
// add this at the beginning
import { requireAuth } from "./auth.js";

// rest of your code

// modify this to include requireAuth and use req.user.id for db.run command
router.post("/", requireAuth, async (req, res) => {
  const { name, description } = req.body || {};
  if (!name) return res.status(400).json({ error: "name required" });

  const db = get_db();
  const query = "INSERT INTO items (name, description, owner_user_id) VALUES (?, ?, ?)";
  
  await db.run(query, 
    [name, description || null, req.user.id], 
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

// modify this to include requireAuth 
router.put("/:id", requireAuth, async (req, res) => {
  const { name, description } = req.body || {};
  if (!name) return res.status(400).json({ error: "name required" });

  const db = get_db();

  const existing = await get_by_id(db, req.params.id);

  if (!existing) 
    return res.status(404).json({ error: "Not found" });

  if (existing.owner_user_id && existing.owner_user_id !== req.user.id) {
    return res.status(403).json({ error: "Forbidden" });
  }
  
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

// modify this to include requireAuth 
router.delete("/:id", requireAuth, async (req, res) => {
  const db = get_db();
  const existing = await get_by_id(db, req.params.id);

  if (!existing) 
    return res.status(404).json({ error: "Not found" });

  if (existing.owner_user_id && existing.owner_user_id !== req.user.id) {
    return res.status(403).json({ error: "Forbidden" });
  }

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

</details>


[< Previous Step](step8.md) | Step 9 | 
