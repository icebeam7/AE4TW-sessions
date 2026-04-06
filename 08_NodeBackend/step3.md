# Step 3: Create a Basic Express Server Entrypoint

In this step, you will create a simple **Express server**.

> Review the references listed below to complete this step.

## Instructions

1. Create your server file (`src/index.js`) and add:
	- Express app initialization
	- JSON body parsing middleware
	- A basic route: `GET /health` that returns `{ status: "ok" }`
	- A port selected via environment variable (for example, `PORT=3000` in `.env`) that defaults to `3000` when not set.

> NOTE: Because you previously added `module` support in `package.json`, Node treats `.js` files as `ES Module`. As a result, you **must** use `import` instead of `require`.
> 	- Example: `import express from "express";` instead of `const express = require('express')`.

2. Start the server using `npm start`, then hit the `health` endpoint in your browser.

<img width="1082" height="374" alt="image" src="https://github.com/user-attachments/assets/175ef9c2-d935-446a-a676-bb683e2a4c21" />

<img width="722" height="368" alt="image" src="https://github.com/user-attachments/assets/549b1aae-3515-437f-97c2-6b8123810d43" />

3. Press `Ctrl-C` in the terminal to stop the application.

## References

- [Express "Hello World" Example](https://expressjs.com/en/starter/hello-world.html)
- [How to Use dotenv in Node.js](https://coreui.io/answers/how-to-use-dotenv-in-nodejs/)
- [Why Your Node.js App Needs express.json(): A Crucial Middleware Explained.](https://office10am.medium.com/why-your-node-js-app-needs-express-json-a-crucial-middleware-explained-a51ffdcc015d)
- [Add health checks to your application](https://developers.redhat.com/learning/learn:openshift:develop-cloud-native-nodejs-applications-expressjs/resource/resources:add-health-checks-your-application)
- [CommonJS vs. ES modules in Node.js](https://blog.logrocket.com/commonjs-vs-es-modules-node-js/)

[< Previous Step](step2.md) | Step 3 | [Next step >](step4.md)
