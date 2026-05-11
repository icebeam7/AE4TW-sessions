This guide will walk you through how to deploy a Node.js backend using the **Vercel CLI**.

## Step 1. Install Vercel CLI

1. Open a Terminal. Use the following command:

`npm install -g vercel`

<img width="513" height="201" alt="Screenshot 2026-04-23 at 13 19 21" src="https://github.com/user-attachments/assets/0d18eba2-9cfb-4a5e-a6b3-c0fb40c0ae23" />


2. Check if the tool was installed successfully by running `vercel --version`.

<img width="1302" height="166" alt="image" src="https://github.com/user-attachments/assets/0abee6a9-36ee-453a-ae98-4257d8558406" />


Troubleshooting:

If you get `command not found: vercel` when checking the version:

<img width="513" height="83" alt="Screenshot 2026-04-23 at 13 32 22" src="https://github.com/user-attachments/assets/4fa2be84-b490-4cb7-a055-450df1797c95" />


- On MacOS, you might need to execute the following commands in case you get an error message:

```bash
mkdir ~/.npm-global
export NPM_CONFIG_PREFIX=~/.npm-global
export PATH=$PATH:~/.npm-global/bin
echo -e "export NPM_CONFIG_PREFIX=~/.npm-global\nexport PATH=$PATH:~/.npm-global/bin" >> ~/.bashrc
```

<img width="1128" height="146" alt="Screenshot 2026-04-23 at 13 32 34" src="https://github.com/user-attachments/assets/07b1bde0-6234-4ee7-b62b-fbf7d5704f02" />


- The following commands deal with permissions:

```bash
sudo chown -R $(whoami ~/.npm
sudo chown -R $(whoami) /usr/local/lib/node_modules
npm config set prefix ~/.npm
```

<img width="363" height="93" alt="Screenshot 2026-04-23 at 13 40 47" src="https://github.com/user-attachments/assets/3b5454e1-11e6-4eeb-8f94-c6e986fcc24c" />

- Then try to install Vercel CLI again and check the version that was installed on your machine.

<img width="512" height="259" alt="Screenshot 2026-04-23 at 13 37 50" src="https://github.com/user-attachments/assets/100d96f2-045e-44f7-b251-2aa747fcc050" />

Step 1 | [Next Step >](step2.md)
