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
  
[< Previous Step](step6.md) | Step 7 | [Next Step >](step8.md)
