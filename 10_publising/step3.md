## Step 3. Configure your project with Vercel

1. Open any of your previous projects in Visual Studio Code.

<img width="778" height="1136" alt="image" src="https://github.com/user-attachments/assets/1c795352-8c26-4bb5-bef7-cd9dbfa4b215" />

2. Verify that your app works locally.

<img width="879" height="984" alt="Screenshot 2026-05-11 at 9 28 52" src="https://github.com/user-attachments/assets/cd70b790-2bd0-4d38-a2c6-9c177939d9b1" />


3. Launch a Terminal and run the command `vercel dev` in the root folder of your project. You will be required to visit [Vercel](https://vercel.com/device) and enter an authorization code.

<img width="1093" height="237" alt="Screenshot 2026-04-23 at 13 49 00" src="https://github.com/user-attachments/assets/e340fa96-40a3-4155-a263-3d11974367a9" />

4. Enter the code:

<img width="533" height="471" alt="Screenshot 2026-04-23 at 13 53 05" src="https://github.com/user-attachments/assets/5d256d4f-ece2-43da-bff7-44c74ae96f45" />

5. Now, you will be presented with a questionnaire:

- Set up and develop. Confirm the path with `Y`
- Scope. Press `Enter` to confirm the project (it usually mentions your GitHub account name)
- Link to existing project. Type `n`
- Project name. Press `Enter` to accept the default value or type the project name of your preference (this is the project name in Vercel website). 
- In which directory is your code located. Set the relative path where your `package.json` file is located. For example, `./` means current location.
- It should detect the type of application you are developing, for example, React.
- Want to modify these settings? Press `n` to confirm the settings.
- Do you want to change additional project settings? Press `n`

Please find below a sample screenshot with the answer of above questions:

<img width="845" height="543" alt="Screenshot 2026-05-11 at 9 47 17" src="https://github.com/user-attachments/assets/88fa6cb3-bb9a-4e32-a4a2-c7fe15f40dbf" />

6. The wizard links your local setup with a project in your Vercel account. Moreover, you will be able to test your application. Please check the app still works.

<img width="732" height="210" alt="Screenshot 2026-05-11 at 9 32 17" src="https://github.com/user-attachments/assets/c8b41ad3-0054-4fbb-a30f-a62acabe35d0" />

8. Press `Ctrl-C` to stop the server.



[< Previous Step](step2.md) | Step 3 | [Next Step >](step4.md)
