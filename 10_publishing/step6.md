## Step 6. Test your application

1. Check that your application works. As you can see, it will actually fail. This is because of environment variables. You need to add them in Vercel, as our `.env` file is not part of the repository (check the `.gitignore` file, in general, we do not commit secrets/credentials/sensitive information).

<img width="878" height="219" alt="Screenshot 2026-05-11 at 14 51 02" src="https://github.com/user-attachments/assets/b805c0db-dc1b-4193-9233-7472624290db" />


2. Back in the Project's page in Vercel, click on Environment Variables (left menu). 

<img width="878" height="638" alt="Screenshot 2026-05-11 at 14 53 24" src="https://github.com/user-attachments/assets/95a50242-2029-4165-90b8-34a73124f3e3" />

3. Click on Add Environment Variable.

<img width="1223" height="596" alt="Screenshot 2026-05-11 at 14 54 03" src="https://github.com/user-attachments/assets/1a712455-95f9-47d2-bde7-066663733177" />


4. Set the Key and Value according to the information on your `.env` file:

<img width="760" height="617" alt="Screenshot 2026-05-11 at 14 56 17" src="https://github.com/user-attachments/assets/91d546d7-d358-4f6e-9ce7-17c4c11a9a72" />


5. Click Add Another to include more environment variables, in case your app need them.

<img width="760" height="925" alt="Screenshot 2026-05-11 at 14 57 24" src="https://github.com/user-attachments/assets/ee9e1539-d09a-415b-b596-b6d504c31386" />

6. Click on Save.

> NOTE: You can speed up this process by importing the whole `.env` file (option located at the bottom) or pasting key/value lines directly on the `Key` textbox (it automatically detects key and secret value). I recommend to do this only if you are aware of the secrets you are adding. 

7. You are instructed to deploy your application again if you want to use the Environment Variables. Click on `Redeploy`.

<img width="433" height="127" alt="Screenshot 2026-05-11 at 15 00 03" src="https://github.com/user-attachments/assets/02e399e6-96a0-4648-9cb4-97310a8d7cf5" />


8. Confirm the options and click on `Redeploy`.

<img width="614" height="667" alt="Screenshot 2026-05-11 at 15 00 53" src="https://github.com/user-attachments/assets/859e8b25-4162-427d-b6db-d76ee548f2b7" />


9. Once the process finishes, click on `View Deployment`.

<img width="441" height="126" alt="Screenshot 2026-05-11 at 15 01 42" src="https://github.com/user-attachments/assets/ea197128-b981-4f82-8b74-be738deede10" />


10. Click on the Production URL (it has a globe icon). 

<img width="1191" height="461" alt="Screenshot 2026-05-11 at 15 03 37" src="https://github.com/user-attachments/assets/3b7b0ed4-5aa2-482e-bac4-f529f1ad78de" />


11. Test the application. It should work now.

<img width="909" height="1003" alt="Screenshot 2026-05-11 at 15 04 17" src="https://github.com/user-attachments/assets/3bf15af2-321e-4c89-9fd7-8a003ec704de" />

CONGRATULATIONS! Your app has been published and available for the world to see it! (or test it, if it's a backend).

BONUS. If you go to your GitHub repository, you will notice two new things:

- A Production deployment with additional details about the deployment (commit used, deployment URL)
- A URL in the About section that takes you to the published app URL

<img width="1275" height="838" alt="image" src="https://github.com/user-attachments/assets/5d08e50d-7a33-4e50-a7b5-b89439c6b5a1" />


[< Previous Step](step5.md) | Step 6
