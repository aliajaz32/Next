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

            Chapter 7

                    Fetching Data

Now that you've created and seeded your database, let's discuss the different ways you can fetch data for your application, and build out your dashboard overview page.

In this chapter...

Here are the topics we’ll cover

Learn about some approaches to fetching data: APIs, ORMs, SQL, etc.

How Server Components can help you access back-end resources more securely.

What network waterfalls are.

How to implement parallel data fetching using a JavaScript Pattern.

                Choosing how to fetch data 

                API layer

APIs are an intermediary layer between your application code and database. There are a few cases where you might use an API:

If you're using 3rd party services that provide an API.

If you're fetching data from the client, you want to have an API layer that runs on the server to avoid exposing your database secrets to the client.

In Next.js, you can create API endpoints using Route Handlers.

            Database queries

When you're creating a full-stack application, you'll also need to write logic to interact with your database. For relational databases like Postgres, you can do this with SQL or with an ORM.

There are a few cases where you have to write database queries:

When creating your API endpoints, you need to write logic to interact with your database.
If you are using React Server Components (fetching data on the server), you can skip the API layer, and query your database directly without risking exposing your database secrets to the client.

                Using Server Components to fetch data

By default, Next.js applications use React Server Components. Fetching data with Server Components is a relatively new approach and there are a few benefits of using them:

Server Components support promises, providing a simpler solution for asynchronous tasks like data fetching. You can use async/await syntax without reaching out for useEffect, useState or data fetching libraries.
Server Components execute on the server, so you can keep expensive data fetches and logic on the server and only send the result to the client.
As mentioned before, since Server Components execute on the server, you can query the database directly without an additional API layer.

            Using SQL

For your dashboard project, you'll write database queries using the Vercel Postgres SDK and SQL. There are a few reasons why we'll be using SQL:

SQL is the industry standard for querying relational databases (e.g. ORMs generate SQL under the hood).
Having a basic understanding of SQL can help you understand the fundamentals of relational databases, allowing you to apply your knowledge to other tools.
SQL is versatile, allowing you to fetch and manipulate specific data.
The Vercel Postgres SDK provides protection against SQL injections.
Don't worry if you haven't used SQL before - we have provided the queries for you.

Go to /app/lib/data.ts, here you'll see that we're importing the sql function from @vercel/postgres. This function allows you to query your database:

You can call sql inside any Server Component. But to allow you to navigate the components more easily, we've kept all the data queries in the data.ts file, and you can import them into the components.

Fetching data for the dashboard overview page

Now that you understand different ways of fetching data, let's fetch data for the dashboard overview page. Navigate to /app/dashboard/page.tsx, paste the following code, and spend some time exploring it:

In the code above:

Page is an async component. This allows you to use await to fetch data.
There are also 3 components which receive data: <Card>, <RevenueChart>, and <LatestInvoices>. They are currently commented out to prevent the application from erroring.

            Fetching data for <RevenueChart/>

To fetch data for the <RevenueChart/> component, import the fetchRevenue function from data.ts and call it inside your component:

Let's continue importing some more data queries!

            Fetching data for <LatestInvoices/>



























































































