Chapter 6

Setting Up Your Database

Before you can continue working on your dashboard, you'll need some data. In this chapter, you'll be setting up a PostgreSQL database using @vercel/postgres. If you're already familiar with PostgreSQL and would prefer to use your own provider, you can skip this chapter and set it up on your own. Otherwise, let's continue!

In this chapter...

Here are the topics we’ll cover

Push your project to GitHub.

Set up a Vercel account and link your GitHub repo for instant previews and deployments.

Create and link your project to a Postgres database.

Seed the database with initial data.

Create a GitHub repository
To start, let's push your repository to Github if you haven't done so already. This will make it easier to set up your database and deploy.

Create a Vercel account

Visit vercel.com/signup to create an account. Choose the free "hobby" plan. Select Continue with GitHub to connect your GitHub and Vercel accounts.

Connect and deploy your project


Next, you'll be taken to this screen where you can select and import the GitHub repository you've just created:

Name your project and click Deploy.

Hooray! 🎉 Your project is now deployed.

By connecting your GitHub repository, whenever you push changes to your main branch, Vercel will automatically redeploy your application with no configuration needed. When opening pull requests, you'll also have instant previews which allow you to catch deployment errors early and share a preview of your project with team members for feedback.

Create a Postgres database

Next, to set up a database, click Continue to Dashboard and select the Storage tab from your project dashboard. Select Connect Store → Create New → Postgres → Continue.

Accept the terms, assign a name to your database, and ensure your database region is set to Washington D.C (iad1) - this is also the default region for all new Vercel projects. By placing your database in the same region or close to your application code, you can reduce latency for data requests.

Once connected, navigate to the .env.local tab, click Show secret and Copy Snippet. Make sure you reveal the secrets before copying them.

Navigate to your code editor and rename the .env.example file to .env. Paste in the copied contents from Vercel.

Important: Go to your .gitignore file and make sure .env is in the ignored files to prevent your database secrets from being exposed when you push to GitHub.

Finally, run pnpm i @vercel/postgres in your terminal to install the Vercel Postgres SDK.

            Seed your database


Now that your database has been created, let's seed it with some initial data.

Inside of /app, there's a folder called seed. Uncomment this file. This folder contains a Next.js Route Handler, called route.ts, that will be used to seed your database. This creates a server-side endpoint that you can access in the browser to start populating your database.

Don't worry if you don't understand everything the code is doing, but to give you an overview, the script uses SQL to create the tables, and the data from placeholder-data.ts file to populate them after they've been created.

Ensure your local development server is running with pnpm run dev and navigate to localhost:3000/seed in your browser. When finished, you will see a message "Database seeded successfully" in the browser. Once completed, you can delete this file.

                Exploring your database

Let's see what your database looks like. Go back to Vercel, and click Data on the sidenav.

In this section, you'll find the four new tables: users, customers, invoices, and revenue.


By selecting each table, you can view its records and ensure the entries align with the data from placeholder-data.ts file.

            Executing queries

You can switch to the "query" tab to interact with your database. This section supports standard SQL commands. For instance, inputting DROP TABLE customers will delete "customers" table along with all its data - so be careful!


Let's run your first database query. Paste and run the following SQL code into the Vercel interface:

SELECT invoices.amount, customers.name
FROM invoices
JOIN customers ON invoices.customer_id = customers.id
WHERE invoices.amount = 666;

























