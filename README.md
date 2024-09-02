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