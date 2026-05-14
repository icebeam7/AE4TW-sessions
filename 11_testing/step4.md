## Writing our test suite function and initial tests

Let's start a Jest test suite (a group of related tests). We will create a parent container for all tests that validate the Items endpoints. Its purpose is to:

- Organize related tests under one label in test output.
- Share setup/teardown logic (like `beforeAll` and `afterAll`) across that group.
- Make reports readable, so all CRUD behavior appears under one section.
- This is not a test by itself, it is the wrapper that structures the full CRUD test suite.

1. Add the following content in `items.test.js`:

```javascript
describe("Items CRUD", () => {
  let app;
  let ownerToken;
  let ownerId;
  let otherToken;

  // we will add more code in the next step


});
```

- We have defined an **Items CRUD** test suite.
- We also define an `ownerToken`, a JWT token belonging to the item owner.
- `ownerId` is the user identifier of the owner in the database.
- `otherToken` this is the token that belongs to a different user.
- `app` is the reference to the application, each test will use it, as mentioned in previous steps.
- We will use these elements across several tests (for example, for testing if the item belongs to the right user).

2. Below the variables you just defined, we will define two blocks: `beforeAll` and `afterAll`:
   - `beforeAll` performs a one-time test setup for the entire suite (before the tests happen)
   - `afterAll` runs once at the end, after all tests have been executed.

Here is the code for both blocks, put this code just inside the `describe` block, below the variables:

```javascript
  beforeAll(async () => {
    await db_initialize_create(":memory:");
    app = buildApp();

    const signupOwner = await signupUser(app, "owner@example.com");
    expect(signupOwner.status).toBe(201);
    ownerId = signupOwner.body.id;

    const loginOwner = await loginUser(app, "owner@example.com");
    expect(loginOwner.status).toBe(200);
    ownerToken = loginOwner.body.token;

    const signupOther = await signupUser(app, "other@example.com");
    expect(signupOther.status).toBe(201);

    const loginOther = await loginUser(app, "other@example.com");
    expect(loginOther.status).toBe(200);
    otherToken = loginOther.body.token;
  });

  afterAll(() => {
    return close_db();
  });
```

Before tests happen:
- We are initializing the database in memory in order to keep tests isolated and fast.
- Then we build an `Express app` instance through `buildApp()`, so all requests in the tests run against the same configured routes and middleware.
- After the app is ready, the setup creates two users and logs both in.
  - The first user (`owner@example.com`) is the resource owner used for successful authorized operations; its `id` and `JWT token` are saved in `ownerId` and `ownerToken`.
  - The second user (`other@example.com`) exists to validate authorization and ownership rules (for example, cases where a non-owner should receive `403`).
- Each step asserts expected status codes (`201` for signup, `200` for login), so setup failures stop the suite early with a clear signal.

An assertion in software testing is a boolean expression (true/false) that validates if the actual outcome of a test matches the expected outcome (the `toBe` part). 

** This means that if, for some reason, creating the user does not return success (`200`), there is no need to continue testing, as tests which require a valid user will all fail.

We have not created a test yet (but we will in the next step!), we have just defined what will happen **before**, it's like we are preparing the test suite.

After tests happen, we release the database connection cleanly to prevent open handles that can make `Jest` hang and ensures predictable teardown.
  
3. Let's now create our first TWO Jest tests. Add the following code just before the `afterAll` block:

```javascript
  describe("GET /items", () => {
    it("returns 200 with an array", async () => {
      const res = await request(app).get("/items");
      expect(res.status).toBe(200);
      expect(Array.isArray(res.body)).toBe(true);
    });

    it("includes newly created items in the list", async () => {
      await createItem(app, ownerToken, { name: "Listed Item" });

      const res = await request(app).get("/items");
      expect(res.status).toBe(200);
      expect(res.body.some((i) => i.name === "Listed Item")).toBe(true);
    });
  });
```

- This block defines a Jest test suite for the `GET /items` endpoint.
- The first test verifies the basic contract of the route: when the client requests `/items`, the API should respond with `HTTP 200` and return a `JSON array`.
  - This confirms both availability and response shape, which is a common baseline assertion for list endpoints.
  - Please note the `it()` block, we are simply describing the test, this is how it will appear in the report.
  - Inside the test code, we send a `GET` request to the `items` endpoint.
  - With `expect` we valide if the `status` of the response is `200` (with `toBe`).
  - Similar validation is done with `expect` and `toBe`, we check if the response returns an array.
- The second test checks functional behavior. It first creates an item using the `createItem` helper we created before (check the arguments). Then, it calls `GET /items` again and asserts that the returned array contains the new item with `.some((i) => i.name === "Listed Item"`, proving that created data is visible in the listing endpoint.

4. Let's run the tests! Open a Terminal in VS Code and execute the command `npm test`. Check the logs and see how the operations defined in `beforeAll` are executed first.

<img width="1782" height="1526" alt="image" src="https://github.com/user-attachments/assets/719e16d9-81f6-43fd-8521-3f291c9bd9c3" />

You can see that two users are added to the in-memory database (we are not using our production db) and a JWT token is obtained for both users. 

Here is the rest of the information returned by the test command:

<img width="1782" height="1094" alt="image" src="https://github.com/user-attachments/assets/e3eb1927-3be0-4b5e-b144-cc53b5cb4040" />

- The `Items CRUD` is the main test suite (collection of tests) that include a sub-suite: `GET /items` with two tests:
  - a test that returns 200 with an array
  - another test that includes newly created items in the list
 
- Please note that those are the descriptions included in the `it` function.
- We can also see that both tests were successful (expectations were met)

- We can also see a report, 1 test suite, 2 tests, they all passed.
- The report also includes the amount of time it took.

5. Finally, let's make a test fail. Modify the second test, in the `createItem` set the item name to `New item`:

```javascript
    it("includes newly created items in the list", async () => {
      await createItem(app, ownerToken, { name: "New Item" });

      const res = await request(app).get("/items");
      expect(res.status).toBe(200);
      expect(res.body.some((i) => i.name === "Listed Item")).toBe(true);
    });
```

The test will fail because we expect `Listed Item`, however the item that is inserted has a different name. Let's see it in action!

6. Run the `npm test` command again (don't forget to save the file before):

<img width="1782" height="998" alt="image" src="https://github.com/user-attachments/assets/2f598b49-f4df-4606-8e9d-8e602079d2a7" />

You can see that the second test has failed, it points to the line of code which produced the error (the expected result). The report also mentions the number of failing/successful tests in the statistics.
   
7. Revert the changes by settting the item name back to `Listed Item` and ensure the tests are successful again.

<img width="1782" height="1080" alt="image" src="https://github.com/user-attachments/assets/ec552d88-30fd-43ee-8bc3-6217375c2d73" />

[< Previous Step](step3.md) | Step 4 | [Next Step >](step5.md)
