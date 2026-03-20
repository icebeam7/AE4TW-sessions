# Step 2: Set the Environment Variables

Environment variables are used to store app secrets and configuration data, which are retrieved by your running app when needed. The value of these environment variables is not hardcoded in your program. These are dynamic and can be changed based on the environment your program is running in.

1. Create a `.env` file in the project root (outside the `src` folder) and open it.

<img width="1072" height="608" alt="image" src="https://github.com/user-attachments/assets/5329484a-8ae7-4136-b039-629ec85df01d" />


2. Add the following 4 environment variables and replace their values with the information provided in Moodle:

```env
REACT_APP_AZURE_OPENAI_API_KEY="replace-value"
REACT_APP_AZURE_OPENAI_ENDPOINT="replace-value"
REACT_APP_AZURE_OPENAI_DEPLOYMENT_NAME="replace-value"
REACT_APP_AZURE_OPENAI_API_VERSION="replace-value"
```

## Explanation

- An API key is required to authenticate requests to the Azure OpenAI service.
- The Azure OpenAI endpoint is the base URL where API requests are sent.
- The deployment name is the name of the Azure OpenAI model deployment that will be used. Deployments in Azure OpenAI allow you to configure and manage specific models.
- The API version specifies the version of the Azure OpenAI API to be used. API versions ensure compatibility between the client and the service, allowing you to specify which version of the API your application is designed to work with.

## Environment Variable Requirements

- The variable must be prefixed with `REACT_APP_`.
- You need to restart the server to reflect changes (if you update an environment variable while the app is running).
- Make sure the `.env` file is in your root folder (the same place as `package.json`), not in the `src` folder.
- You will access environment variables in your code like this: `process.env.REACT_APP_SOME_VARIABLE`.


[< Previous Step](step1.md) | Step 2 | [Next Step >](step3.md)
