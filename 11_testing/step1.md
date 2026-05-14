## Testing a Node.JS application

In this tutorial, you will test a backend application using **Jest** and **Supertest**.

1. Extract the provided backend application to a folder and open it using Visual Studio Code.

2. Install the project dependencies using `npm install`

3. Run the application using `npm run start`

<img width="909" height="724" alt="Screenshot 2026-05-14 at 5 37 29" src="https://github.com/user-attachments/assets/81f1b5ce-9434-49fb-b00f-5ad7f6d8001b" />

4. The application runs on port `3000`. Evaluate the following APIs (you can use any app/extension such as **Postman** or **curl**. Here I am using **ThunderClient** extension):

- Create a user with `POST` over `auth/signup` endpoint. You need to provide user information in the `Body` as part of the request. Send the request:

<img width="882" height="457" alt="Screenshot 2026-05-14 at 5 40 44" src="https://github.com/user-attachments/assets/cd9956cb-3b12-4d83-a3a1-a3c6ef3ab3a9" />

- Get a `JWT token` by signing in with a `POST` request over `auth/login` endpoint and by providing the new user's credentials in the `body`. Send the request:

<img width="568" height="375" alt="Screenshot 2026-05-14 at 5 43 03" src="https://github.com/user-attachments/assets/fa355e2c-e5c0-43b0-8a43-0f15c2d7646f" />

- Copy the generated token from the previous response and set it in the `Bearer authentication` scheme of a new `POST` request over `items` endpoint. Do not send the request yet. 
  
<img width="600" height="276" alt="Screenshot 2026-05-14 at 5 45 14" src="https://github.com/user-attachments/assets/e6e053c8-dbef-4298-b430-8522217b4f29" />

- Complete the request by setting the new product information in the `body` section. Send the request:

<img width="600" height="462" alt="Screenshot 2026-05-14 at 5 45 38" src="https://github.com/user-attachments/assets/74bd47d9-7f1e-4abf-beef-ededc2586221" />

- Finally, check if the item was really inserted by sending a `GET` request to the `items` endpoint:

<img width="600" height="518" alt="Screenshot 2026-05-14 at 5 46 28" src="https://github.com/user-attachments/assets/e655b8ea-46d2-4d02-b2fe-99f9f9d98dc2" />

Step 1 | [Next Step >](step2.md)
