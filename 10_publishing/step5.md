## Step5. Deploy your app

First, we are going to try deploying our application first using the CLI. It will fail. This is intended, so you can see where to track the error, fix it, and then trigger an automated deployment.

### Task A. Manual deployment

1. Come back to VS Code and launch a Terminal. Run the command `vercel deploy --prod` to deploy your application to Vercel.

<img width="918" height="122" alt="Screenshot 2026-05-11 at 14 35 08" src="https://github.com/user-attachments/assets/c1205b1d-28f2-49b1-98df-cf46cb240a0b" />


The command returns an error message and also two URLs:

- Inspect URL: Use this URL to see the logs and track the errors. 
- Production URL: The URL where you can see your app if deployment was successful.

### Task B. Fix the errror

1. Copy the Inspect URL and paste it in a new tab in your browser.

<img width="1323" height="733" alt="Screenshot 2026-05-11 at 14 37 47" src="https://github.com/user-attachments/assets/433901ba-c8ec-4f8e-bedb-e31dd420e425" />

2. Scroll down in the Build Logs section and you will see the specific error. In this case: 

```
[eslint] 
src/App.js
  Line 1:8:  'logo' is defined but never used  no-unused-vars
```

This sounds like a warning message (the app works, as demonstrated before), but for a production deployment we need to get rid of it.

3. Come back to VS Code and fix the error. In this case, I have commented line 1 on `App.js`, as mentioned by the error message.

<img width="669" height="352" alt="Screenshot 2026-05-11 at 14 40 06" src="https://github.com/user-attachments/assets/c6d3496c-1275-49e4-8cda-8fa26a839294" />

4. Another recommended set of actions:
   
  4.1 Use `node -v` to check which Node.js version your are using.

  <img width="562" height="129" alt="Screenshot 2026-05-11 at 14 45 11" src="https://github.com/user-attachments/assets/58d311fa-d588-4328-8578-3319106ddc39" />
  
  4.2 Then, click on your Vercel project

<img width="1326" height="461" alt="Screenshot 2026-05-11 at 14 45 48" src="https://github.com/user-attachments/assets/5eb87c3e-49b9-4c96-9818-1432dc7e13ea" />

  
  4.3 On the left menu, scroll down and click on Settings

<img width="729" height="874" alt="Screenshot 2026-05-11 at 14 46 39" src="https://github.com/user-attachments/assets/3963173c-8cee-4e92-94c3-b187536cc539" />

  
  4.4 Click on Build and Deployment and set the Node.js version to the same local version you are using. Click on Save.

<img width="1150" height="958" alt="Screenshot 2026-05-11 at 14 47 57" src="https://github.com/user-attachments/assets/0877dce2-76bb-4d37-9bec-d088a235a047" />


### Task C. Automatic deployment

1. Commit and push your changes to GitHub. This triggers an automated Vercel workflow that takes your code and publishes to an endpoint.

<img width="411" height="181" alt="Screenshot 2026-05-11 at 14 41 17" src="https://github.com/user-attachments/assets/bef52531-c1a3-4280-8278-84e0d9e3bd18" />

2. Go to Vercel, access your project. This time, you can see a `Ready` status, which means the deployment was successful.

<img width="1119" height="474" alt="Screenshot 2026-05-11 at 14 49 34" src="https://github.com/user-attachments/assets/65084526-4741-48ff-b5d6-0a953959bfb7" />


3. Click on the Domains URL to access your application.

<img width="878" height="219" alt="Screenshot 2026-05-11 at 14 50 53" src="https://github.com/user-attachments/assets/721b1f34-1c29-4a19-8364-93224e8c1585" />


[< Previous Step](step4.md) | Step 5 | [Next Step >](step6.md)
