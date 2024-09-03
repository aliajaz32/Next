Chapter 6 :- Set up database

                To Deploy

1. Create a gihub repo and vercel account 

2. deploy project.

3.Next, you'll be taken to this screen where you can select and import the GitHub repository you've just created:

4. Name your project and click Deploy.

5. Hooray! 🎉 Your project is now deployed.

6. By connecting your GitHub repository, whenever you push changes to your main branch, Vercel will automatically redeploy your application with no configuration needed. When opening pull requests, you'll also have instant previews which allow you to catch deployment errors early and share a preview of your project with team members for feedback.

        Create a Postgres database

1. Next, to set up a database, click Continue to Dashboard and select the Storage tab from your project dashboard. Select Connect Store → Create New → Postgres → Continue.


2. and ensure your database region is set to Washington D.C (iad1)

3.Once connected, navigate to the .env.local tab, click Show secret and Copy Snippet. Make sure you reveal the secrets before copying them.

4. Navigate to your code editor and create file .env. Paste in the copied contents from Vercel.

5.  Go to your .gitignore file and make sure .env is in the ignored files to prevent your database secrets from being exposed when you push to GitHub.

6. Finally, run pnpm i @vercel/postgres in your terminal to install the Vercel Postgres SDK.

                        Seed your database

1. Inside of /app, there's a folder called seed. Uncomment this file. This folder contains a Next.js Route Handler, called route.ts, that will be used to seed your database.

2.  Ensure your local development server is running with pnpm run dev and navigate to localhost:3000/seed in your browser. When finished, you will see a message "Database seeded successfully" in the browser. Once completed, you can delete this file.






