# Step 4: Configure Environment Variables

In this step, you will set up environment variables for the port used by the app and the secret key that will be used later by the encryption/decryption processes.

1. Create a `.env` file in the main folder (`node-express-api`) and store:

   ```
   PORT=...
   JWT_SECRET=... (a long random string)
   ```

   Ensure `.env` is included in `.gitignore`.

2. **Reference**:
   - [dotenv usage](https://www.npmjs.com/package/dotenv)
   - [env variables: gitignore](https://calmcode.io/course/env-variables/gitignore)

3. Print the port and secret using `console.log` in `index.js`.

4. Start the server again and validate that you can read (see) both values.

5. Comment out the line where you print the secret value so it is no longer displayed in the console.

[< Previous Step](step3.md) | Step 4 | [Next step >](step5.md)