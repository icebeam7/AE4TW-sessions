## Add more tests

In this final step, you will add include more tests to validate the other endpoints. For each endpoint, run `npm test` to check if they are successful.

The primary goal of testing an app is to ensure that it functions correctly, performs reliably, and provides a seamless user experience before it is released to the public. It is a critical QA (quality assurance) process that validates the application against technical and business requirements, helping to prevent user attrition and protect our (organization's) reputation.

In all these tests, you essentially invoke an endpoint (send a request) and evaluate the response with assumptions.

1. To validate the `POST` endpoint, we will add 5 tests:

- Unauthenticated user (should return 401)
- Invalid token = 401 status code
- Client providing incomplete information (name) returns Bad Request
- Successful item creation when all data is provided
- Successful item creation even if the description is not included (the field is optional)

Add the code inside `describe("Items CRUD", () => {` just below the `describe("GET /items", () => {` test suite.

```javascript
  describe("POST /items", () => {
    it("returns 401 when no Authorization header is provided", async () => {
      const res = await request(app).post("/items").send({ name: "Unauthorized" });
      expect(res.status).toBe(401);
    });

    it("returns 401 when the token is invalid", async () => {
      const res = await request(app)
        .post("/items")
        .set("Authorization", "Bearer not.a.valid.token")
        .send({ name: "Bad Token" });
      expect(res.status).toBe(401);
    });

    it("returns 400 when name is missing", async () => {
      const res = await createItem(app, ownerToken, {
        description: "No name field",
      });
      expect(res.status).toBe(400);
      expect(res.body.error).toBeDefined();
    });

    it("creates an item and returns 201 with the created object", async () => {
      const res = await createItem(app, ownerToken, {
        name: "My Item",
        description: "A fine item",
      });

      expect(res.status).toBe(201);
      expect(res.body.id).toBeDefined();
      expect(res.body.name).toBe("My Item");
      expect(res.body.description).toBe("A fine item");
      expect(res.body.owner_user_id).toBe(ownerId);
    });

    it("creates an item without an optional description", async () => {
      const res = await createItem(app, ownerToken, {
        name: "No Description Item",
      });

      expect(res.status).toBe(201);
      expect(res.body.description).toBeNull();
    });
  });
```

Please note that we can set header for the requests with `set`. We send the request to the server with `send`. We also check for null with `toBeNull`.

Save the file and run the test with `npm test`. Expected output:

<img width="1276" height="756" alt="image" src="https://github.com/user-attachments/assets/c83e29e8-fcb9-4ade-b996-42fb8b607dff" />

  
2. To validate the `GET item/id` endpoint we will add 2 tests for:

- Checking the response of an item that does not exist.
- Evaluating if an item exists. Before running the test, we create the item (using `beforeAll`).

Place this code below the test suite for the POST operation.

```javascript
  describe("GET /items/:id", () => {
    let itemId;

    beforeAll(async () => {
      const res = await createItem(app, ownerToken, { name: "New Item" });
      itemId = res.body.id;
    });

    it("returns 404 for a non-existent item", async () => {
      const res = await request(app).get("/items/99999");
      expect(res.status).toBe(404);
    });

    it("returns 200 with the correct item for a valid id", async () => {
      const res = await request(app).get(`/items/${itemId}`);
      expect(res.status).toBe(200);
      expect(res.body.id).toBe(itemId);
      expect(res.body.name).toBe("New Item");
    });
  });  
```

Save the file and run the test with `npm test`. Expected output:

<img width="1276" height="756" alt="image" src="https://github.com/user-attachments/assets/e7ab0146-bd40-4d6e-a276-b92508945c18" />


3. To validate the `PUT` endpoint we test for 6 cases:

- Trying to update an item without a JWT token (unauthenticated user)
- The user did not provide an item name (bad request) in the update
- Trying to update a non-existing item
- Trying to update an item created by different user (we are using a valid JWT token, but from another user)
- A valid update
- Use the `GET items/id` endpoint to validate the data was inserted in the database
- Same as the previous test, we insert an item first.

```javascript
  describe("PUT /items/:id", () => {
    let itemId;

    beforeAll(async () => {
      const res = await createItem(app, ownerToken, {
        name: "Updatable Item",
        description: "Original desc",
      });
      itemId = res.body.id;
    });

    it("returns 401 when no Authorization header is provided", async () => {
      const res = await request(app)
        .put(`/items/${itemId}`)
        .send({ name: "New Name" });
      expect(res.status).toBe(401);
    });

    it("returns 400 when name is missing", async () => {
      const res = await request(app)
        .put(`/items/${itemId}`)
        .set(authHeader(ownerToken))
        .send({ description: "Name is missing" });
      expect(res.status).toBe(400);
    });

    it("returns 404 for a non-existent item", async () => {
      const res = await request(app)
        .put("/items/99999")
        .set(authHeader(ownerToken))
        .send({ name: "Ghost Update" });
      expect(res.status).toBe(404);
    });

    it("returns 403 when the authenticated user is not the owner", async () => {
      const res = await request(app)
        .put(`/items/${itemId}`)
        .set(authHeader(otherToken))
        .send({ name: "Hijacked Name" });
      expect(res.status).toBe(403);
    });

    it("updates the item and returns 204", async () => {
      const res = await request(app)
        .put(`/items/${itemId}`)
        .set(authHeader(ownerToken))
        .send({ name: "Updated Name", description: "Updated desc" });
      expect(res.status).toBe(204);
    });

    it("persists the updated values", async () => {
      const res = await request(app).get(`/items/${itemId}`);
      expect(res.body.name).toBe("Updated Name");
      expect(res.body.description).toBe("Updated desc");
    });
  });

```

Please note that we can use `authHeader` to set the Authorization header of a request, we provide the JWT token for that.

Save the file and run the test with `npm test`. Expected output:

<img width="1276" height="1062" alt="image" src="https://github.com/user-attachments/assets/2b160a92-f8e0-4497-a597-4853495ee1ea" />


4. To validate the `DELETE` endpoint we add 4 tests:

- First, we insert an item before all tests happen.
- Then we validate for unauthorized user (no token)
- We try to delete a non-existent item
- A different user (not the owner) tries to delete the item
- A valid item deletion
- Checking the deleted item does not exist anymore

```javascript
  describe("DELETE /items/:id", () => {
    let itemId;

    beforeAll(async () => {
      const res = await createItem(app, ownerToken, { name: "Deletable Item" });
      itemId = res.body.id;
    });

    it("returns 401 when no Authorization header is provided", async () => {
      const res = await request(app).delete(`/items/${itemId}`);
      expect(res.status).toBe(401);
    });

    it("returns 404 for a non-existent item", async () => {
      const res = await request(app)
        .delete("/items/99999")
        .set(authHeader(ownerToken));
      expect(res.status).toBe(404);
    });

    it("returns 403 when the authenticated user is not the owner", async () => {
      const res = await request(app)
        .delete(`/items/${itemId}`)
        .set(authHeader(otherToken));
      expect(res.status).toBe(403);
    });

    it("deletes the item and returns 204", async () => {
      const res = await request(app)
        .delete(`/items/${itemId}`)
        .set(authHeader(ownerToken));
      expect(res.status).toBe(204);
    });

    it("item is no longer accessible after deletion", async () => {
      const res = await request(app).get(`/items/${itemId}`);
      expect(res.status).toBe(404);
    });
  });
```

Save the file and run the test with `npm test`. Expected output:

<img width="1276" height="1272" alt="image" src="https://github.com/user-attachments/assets/f10e1cb9-53de-4929-9c93-f09385b50a04" />


You now have gained experience with testing a `Node.js` backend application with `Jest` and `Supertest`. You created up to 20 tests!

[< Previous Step](step4.md) | Step 5 
