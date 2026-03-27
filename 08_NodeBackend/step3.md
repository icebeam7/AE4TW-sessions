# Step 3: Create a Basic Express Server Entrypoint

In this step, you will create a simple **Express server**.

## Instructions

1. Create your server file (`src/index.js`) and add:
	- Express app initialization
	- JSON body parsing middleware
	- A basic route: `GET /health` that returns `{ status: "ok" }`
	- A port selected via environment variable (for example, `PORT=3000` in `.env`) that defaults to `3000` when not set

2. Start the server using `npm start`, then hit the `health` endpoint.

## References

- [Express "Hello World" Example](https://expressjs.com/en/starter/hello-world.html)
- [How to: dotenv in Express.js](https://www.newline.co/@goatandsheep/how-to-dotenv-in-expressjs--34b20eb8)
- [Add health checks to your application](https://developers.redhat.com/learning/learn:openshift:develop-cloud-native-nodejs-applications-expressjs/resource/resources:add-health-checks-your-application)
- [CommonJS vs. ES modules in Node.js](https://blog.logrocket.com/commonjs-vs-es-modules-node-js/)

[< Previous Step](step2.md) | Step 3 | [Next step >](step4.md)