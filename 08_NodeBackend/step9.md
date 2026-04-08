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

[< Previous Step](step8.md) | Step 9 | 
