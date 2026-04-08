# Step 8 — Implement Login (Issue JWT)

> Review the references listed below to complete this step. 

1. Implement `POST /auth/login` endpoint in `src/routes/auth.js`.

   - Validate the input. The request contains `email` and `password`.
   - Look Up the User by Email: Query the database to find the user associated with the provided `email`.
   - Compare Password to Stored Hash: Use `bcryptjs` library to compare the provided `password` with the stored hash value.
   - Sign a JWT and Return: If the password is correct, generate a **JSON Web Token (JWT)** using `jsonwebtoken` library and return it in the response:
     ```json
     {
       "token": "<JWT_TOKEN_STRING>"
     }
     ```

   - Sign Tokens:
      - Include the user ID in the JWT `sub` (subject) claim.
      - Add an expiration time (e.g., `1h`).

2. Test the endpoint: Ensure signing in using the endpoint with valid credentials returns a JWT token string.

<img width="1692" height="1550" alt="image" src="https://github.com/user-attachments/assets/730a2edc-0162-484f-80ac-ecb0e9b27be8" />

3. Also test the endpoint for `Unauthorized` response when invalid credentials are provided:

<img width="1092" height="790" alt="image" src="https://github.com/user-attachments/assets/11dd95a0-5ba8-4955-b5fb-298b46e2fa57" />

## References

- [jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken)
- [How to Handle Passwords Safely with BcryptsJS in JavaScript](https://www.digitalocean.com/community/tutorials/how-to-handle-passwords-safely-with-bcryptsjs-in-javascript)

[< Previous Step](step7.md) | Step 8 | [Next Step >](step9.md)
