# Image Generation using React and Azure OpenAI

In this tutorial, you will create a React app where users enter a text prompt (for example, "a futuristic city at sunset"), click a button, and view an AI-generated image based on that prompt.

- [OpenAI's gpt-image-1](https://developers.openai.com/api/docs/guides/image-generation) model will be used to generate images from the user prompt.
- Bootstrap will be used for styling.

## Step 1: Set Up the Project

1. Launch a new terminal (Command Prompt) and set the current directory to your working directory, for example, the `AE4TW` folder.

2. Create a new React app named `ai-image-generator` using `create-react-app`:

3. Move to the newly created folder using `cd`.

4. Install `bootstrap` and `react-bootstrap` packages:

```bash
npm install bootstrap react-bootstrap
```

<img width="1708" height="584" alt="image" src="https://github.com/user-attachments/assets/5c8e3596-9b5f-47fe-8e26-db3660a26bd7" />


5. Install the Azure OpenAI client library for JavaScript:

```bash
npm install openai
```

<img width="1708" height="584" alt="image" src="https://github.com/user-attachments/assets/b1b5878e-7a57-4f48-82f5-271efe0cdcfb" />

6. Make sure to run `npm install --save-dev ajv` if you got an error about a missing module in the first React tutorial. Another useful command is `npm install` to install all dependencies.

7. Open the `ai-image-generator` folder in VS Code.

8. Delete the following files from the `src` folder (they will not be used):

- `App.test.js`
- `reportWebVitals.js`
- `setupTests.js`

9. Edit `index.js`:

- Remove (or comment out) the unused import for `reportWebVitals`.
- Remove (or comment out) the line that calls `reportWebVitals()`.
- Import Bootstrap CSS by adding:

```js
import 'bootstrap/dist/css/bootstrap.min.css';
```

10. Save the file.

[Next Step](step2.md)
