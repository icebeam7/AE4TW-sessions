# Step 6: Implement CRUD for Items (Start Without Auth)

## Behaviors to Implement

### **GET /items**
- Return an array of items (possibly empty).

### **GET /items/:id**
- Return `404` if the item is missing.

### **POST /items**
- Validate the `name` field.

### **PUT /items/:id**
- Validate the `name` field.
- Return `404` if the item is missing.

### **DELETE /items/:id**
- Return `404` if the item is missing.
- Return `204` on success.

1. Implement these endpoints in `src/routes/items.js`:
    - You need a connection to the database to implement each behavior.

## Reference
- [Express Routing Guide](https://expressjs.com/en/guide/routing.html)

2. In `src/index.js`, mount the item routes under `/items`.

3. Test CRUD operations using `Postman` (temporarily without auth) or the `Thunder Client` VS Code extension.

[< Previous Step](step5.md) | Step 6 | [Next Step >](step7.md)