# Step 6: Implement the App.js Component

The project integrates OpenAI services to generate images based on user-provided prompts. The environment variables defined in the .env file are used to connect to the service, ensuring flexibility, security, and ease of configuration. The custom React components are also used.

Complete the following steps using `src/App.js` file:

1. Import the React library, along with the useState hook to maintain and update state variables dynamically.

2. Import the three custom components created in previous steps.

3. Import the `OpenAI` object from the `openai` package using CommonJS syntax (require). This object is used to make API calls to an OpenAI model (`gpt-image-1`).

```javascript
import OpenAI from 'openai';
```

4. Read environment variables: Define two constants that retrieve configuration values from environment variables.

```javascript
const apiKey = process.env.REACT_APP_AZURE_OPENAI_API_KEY;
const deploymentName = process.env.REACT_APP_AZURE_OPENAI_DEPLOYMENT_NAME;
```

These values are essential for securely connecting to the OpenAI service and are used later for API requests.

5. Create a function named `getClient`, which returns a configured `OpenAI` client instance.

```javascript
function getClient() {
  return new OpenAI({
    apiKey: apiKey,
    dangerouslyAllowBrowser: true
  });
}
```

The constants holding environment variable values are passed to the `OpenAI` client. The `dangerouslyAllowBrowser` value is set to `true`, enabling use in a browser environment.

By default, **this is normally disabled to prevent exposing sensitive credentials**. It is explicitly enabled here because the app is intended to run in a private testing browser environment.

**Remember: using dangerouslyAllowBrowser: true must be carefully considered, as it can expose sensitive credentials if not handled securely.**

6. Clear the App return content: Delete only the current content inside the App function (the return value), leaving the function itself.

```javascript
function App() {

}
```

7. Add state variables: Inside `App`, define three state variables using the `useState` hook. Here are the variables and functions that you can use:

- `prompt` holds user input describing the image to generate. By default, it is set to an **empty string**.
- `setPrompt` updates prompt when the user types in the form.
- `imageUrl` stores the generated image URL returned by the API. By default, it is set to an **empty string**.
- `setImageUrl` updates imageUrl so the UI can display the generated image.
- `loading` tracks whether image generation is currently in progress. By default, it is set to `false`
- `setLoading` sets loading back to false when processing is complete.

> Hint:

```javascript
  const [prompt, setPrompt] = useState('');
```

8. Add the generateImage async callback

Define a generateImage function that validates input, calls the OpenAI API, and updates state.

```javascript
  const generateImage = async () => {
    if (!prompt) return;

    setLoading(true);
    setImageUrl('');

    try {
      const client = getClient();
      console.log('Generating image with prompt:', prompt);

      const results = await client.images.generate({
        prompt: prompt,
        model: deploymentName,
        size: '1024x1024',
        n: 1,
        quality: 'low'
      });
      
      const image_base64 = results.data[0].b64_json;
      console.log('Received image data (base64):', image_base64);

      const mime = "image/png";

      const image_src = image_base64.startsWith("data:") 
                    ? image_base64 
                    : `data:${mime};base64,${image_base64}`;
      
      setImageUrl(image_src);
    } catch (err) {
      console.error(err);
      alert('Failed to generate image.');
    }

    setLoading(false);
  };
```

Function behavior summary:

- Input validation: exits early if `prompt` is empty.
- State initialization: sets `loading` to true and clears the previous image URL.
- Client setup: creates a new `OpenAI` client by calling `getClient`.
- API request: calls `client.images.generate` with `prompt`, `model`, `size`, `n`, and `quality` settings. Read more about it [https://learn.microsoft.com/en-us/azure/foundry/openai/how-to/dall-e?tabs=command-line%2Capi-key%2Ctypescript-keyless&pivots=programming-language-javascript#call-the-image-generation-api](here).
- Response processing: reads `results.data` and extracts the generated base 64 string.
- The base64 string (`b64_json`) contains the image data, which is converted to a valid URI format.
- State update: stores the URL in `imageUrl` to render the image.
- Error handling: logs errors and shows a failure alert.
- Final reset: sets `loading` to false after completion.

## 9. Return the UI structure from App

Return the following JSX as the App component UI:

```javascript
  return (
    <div className="min-vh-100 bg-light text-center py-4 px-2">
      <h1 className="h2 fw-bold mb-4">AI Image Generator with OpenAI</h1>
      <ImageGeneratorForm
        prompt={prompt}
        setPrompt={setPrompt}
        onGenerate={generateImage}
      />
      {loading && <Loader />}
      {imageUrl && <ImageDisplay url={imageUrl} />}
    </div>
  );
```

UI details:

- The outer container uses `Bootstrap` utility classes to fill `viewport height`, apply a `light background`, `center content`, and `add padding`.
- The heading displays the app title with `Bootstrap` typography and spacing classes.
- `ImageGeneratorForm` renders the `prompt` input and `generate` button, receiving `prompt`, `setPrompt`, and `onGenerate` properties.
- The `Loader` component is conditionally rendered when `loading` is true to show progress.
- `ImageDisplay` is conditionally rendered when `imageUrl` exists to show the generated image.

[< Previous Step](step5.md) | Step 6 | [Next Step >](step7.md)
