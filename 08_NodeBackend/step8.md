# Step 8 — Implement Login (Issue JWT)

## Create `POST /auth/login`

1. Validate Input:
   - Ensure the request contains:
     ```json
     {
       "email": "string",
       "password": "string"
     }
     ```

2. Look Up the User by Email:
   - Query the database to find the user associated with the provided email.

3. Compare Password to Stored Hash:
   - Use a password hashing library (`bcrypt`) to compare the provided password with the stored hash.

4. Sign a JWT and Return:
   - If the password is correct, generate a JSON Web Token (JWT) and return it in the response:
     ```json
     {
       "token": "<JWT_TOKEN_STRING>"
     }
     ```

## Use `jsonwebtoken` Library

5. Sign Tokens:
  - Include the user ID in the JWT `sub` (subject) claim.
  - Add an expiration time (e.g., `1h`).

6. Test: Ensure the login endpoint returns a JWT token string.

## Reference

- [jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken)

[< Previous Step](step7.md) | Step 8 | [Next Step >](step9.md)