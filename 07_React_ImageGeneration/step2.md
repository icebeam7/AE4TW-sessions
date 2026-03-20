# Step 2: Set the Environment Variables

Environment variables are used to store app secrets and configuration data, which are retrieved by your running app when needed. The value of these environment variables is not hardcoded in your program. These are dynamic and can be changed based on the environment your program is running in.

1. Create a `.env` file in the project root (outside the `src` folder) and open it.

<img width="1072" height="608" alt="image" src="https://github.com/user-attachments/assets/5329484a-8ae7-4136-b039-629ec85df01d" />


2. Add the following 2 environment variables and replace their values with the information provided in Moodle:

```env
REACT_APP_AZURE_OPENAI_API_KEY="replace-value"
REACT_APP_AZURE_OPENAI_DEPLOYMENT_NAME="replace-value"
```

## Explanation

- An API key is required to authenticate requests to the OpenAI service.
- The deployment name is the name of the OpenAI model deployment that will be used. Deployments in OpenAI allow you to configure and manage specific models.

## Environment Variable Requirements

- The variable must be prefixed with `REACT_APP_`.
- You need to restart the server to reflect changes (if you update an environment variable while the app is running).
- Make sure the `.env` file is in your root folder (the same place as `package.json`), not in the `src` folder.
- You will access environment variables in your code like this: `process.env.REACT_APP_SOME_VARIABLE`.


[< Previous Step](step1.md) | Step 2 | [Next Step >](step3.md)
