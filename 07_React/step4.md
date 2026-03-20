## Step 4: Set Up the Project

1. Launch a new Terminal (Command Prompt), and set the current directory to the project directory you will use, for example, `AE4TW` folder:

<img width="1320" height="360" alt="image" src="https://github.com/user-attachments/assets/0e4fe9d0-e8fb-439e-a8bc-a9c79627f719" />

2. Run the following command to create a new React app using the `create-react-app` template:

```bash
npx create-react-app posts-app
```

<img width="1422" height="334" alt="image" src="https://github.com/user-attachments/assets/857715a6-a36a-4985-bf8a-677773284e1a" />


3. If you are asked to install the `create-react-app` package, type `y` to proceed.

<img width="848" height="142" alt="image" src="https://github.com/user-attachments/assets/d03838bc-d1ce-48e4-ad74-4f020c303690" />


4. In VS Code, open the `posts-app` folder.

<img width="1160" height="745" alt="Screenshot 2026-03-20 at 12 08 38" src="https://github.com/user-attachments/assets/77dc46f4-5b38-4f44-93e5-9f209e8c0461" />


5. Review the project structure.

<img width="718" height="1290" alt="image" src="https://github.com/user-attachments/assets/a44e7a38-df7d-4770-84fb-aef6020ce138" />


6. Delete the following files located in the `src` folder (they will not be used):
- `App.test.js`
- `reportWebVitals.js`
- `setupTests.js`

<img width="718" height="330" alt="image" src="https://github.com/user-attachments/assets/f2b78f3f-7e84-48e3-85c6-66ec04ed8c9a" />


7. Open `index.js` in the `src` folder 

8. Remove (or comment out) the following elements:

- The unused import that references the deleted `reportWebVitals` file (line 5).
- Line 17 as well, which calls that function.

<img width="765" height="487" alt="Screenshot 2026-03-20 at 12 13 47" src="https://github.com/user-attachments/assets/3d6477be-db94-4b29-8063-446f5b4d0998" />


9. Save the file.

[< Previous Step](step3.md) | Step 4 | [Next Step >](step5.md)
