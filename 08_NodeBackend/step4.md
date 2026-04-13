# Step 4: Configure Environment Variables

In this step, you will set up environment variables for the port used by the app and the secret key that will be used later by the encryption/decryption processes.

> Review the references listed below to complete this step.

1. Create a `.env` file in the main folder (`node-express-api`) and store:

   ```
   PORT=...
   JWT_SECRET=... (a long random string)
   ```

> NOTE: Later, before you commit your changes in your git repository, make sure to create a `.gitignore` file that includes `.env`.

2. Print the port and secret using `console.log` in `index.js`.

3. Start the server again and validate that you can read (see) both values.

<img width="1240" height="392" alt="image" src="https://github.com/user-attachments/assets/29c69423-259a-4af7-bf00-640058df7e81" />

4. Without stopping the server, comment out the line where you print the secret value so it is no longer displayed in the console. Save the file. Please notice how the server is automatically restarted when a new version of the file is detected.

<img width="1094" height="520" alt="image" src="https://github.com/user-attachments/assets/fe5daf66-987d-43aa-89e0-af273ceca6b3" />

5. Optionally, comment out also the line where you read the secret value. Press `Ctrl-C` to stop the server.

## References
- [dotenv usage](https://www.npmjs.com/package/dotenv)
- [env variables: gitignore](https://calmcode.io/course/env-variables/gitignore)

<details>

<summary>Solution</summary>

```javascript
import express from "express";
import dotenv from 'dotenv'
dotenv.config()

const app = express()
app.use(express.json());

const port = process.env.PORT || 3000
//const jwtSecret = process.env.JWT_SECRET;

app.get("/health", (req, res) => res.json({ status: "ok" }));

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
  //console.log(`Using JWT secret: ${jwtSecret}`);
})
```

</details>


[< Previous Step](step3.md) | Step 4 | [Next step >](step5.md)
