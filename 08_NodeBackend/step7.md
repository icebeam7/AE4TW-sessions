# Step 7: Implement Signup (Store Hashed Passwords)

1. Implement `POST /auth/signup` endpoint in a new file: `src/routes/auth.js`.
  - Validate input `{ email, password }`.
  - Hash the password using `bcrypt`.
  - Insert the user into the `users` table.
  - If the email already exists, return HTTP `409`.

2. In `src/index.js`, mount the auth routes under `/auth`.

3. Test the Endpoint: Ensure signing up returns a new user ID.

4. Verify the database: Open the database and check that the password is stored as a hash value rather than plaintext.

## Reference
- [bcrypt npm package](https://www.npmjs.com/package/bcrypt)
- [Building a Secure Login System with Node.js, bcrypt, and JWT Authentication](https://medium.com/@svk19998/building-a-secure-login-system-with-node-js-bcrypt-and-jwt-authentication-b3e5b25de218)

[< Previous Step](step6.md) | Step 7 | [Next Step >](step8.md)