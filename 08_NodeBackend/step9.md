# Step 9 — Add JWT Middleware and Protect Routes

## Create Middleware: `requireAuth`

1. Functionality:
   - Reads the `Authorization` header in the format:
     ```http
     Authorization: Bearer <token>
     ```
   - Verifies the token using `JWT_SECRET`.
   - Adds the following object to the `req` object upon successful verification:
     ```javascript
     req.user = {
       id: "<user_id>",
       email: "<user_email>"
     };
     ```
   - Returns a `401 Unauthorized` response on failure.

2. Protect the Following Routes:

    - `POST /items`
    - `PUT /items/:id`
    - `DELETE /items/:id`

3. Test: Ensure that protected endpoints return a `401 Unauthorized` response when accessed without a valid token.

## References

- [Authorization Header (Bearer)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Authorization)
- [Express Middleware](https://expressjs.com/en/guide/using-middleware.html)

[< Previous Step](step8.md) | Step 9 | 