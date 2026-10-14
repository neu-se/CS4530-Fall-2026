---
layout: page
title: Continuous Deployment Pipeline for GameNite
permalink: /activities/continuous-deployment
nav_exclude: true
---

# Continuous Deployment Pipeline for GameNite

In this activity, you will set up a continuous deployment pipeline using MongoDB Atlas and Render.com. The application will be deployed through Render.com, while the MongoDB database will be hosted in the cloud using MongoDB Atlas.

Only one member of each team needs to complete these steps, as the resulting deployment will be shared with the entire team. However, if preferred, the team can work together to deploy the application.

{: .note }
In this activity, we will focus on building a continuous deployment pipeline, but what about continuous integration? There are many ways to use continuous integration in your projects. For example, you can use GitHub Actions to automatically run tests after pushing a commit. GameNite has a continuous integration setup for running tests, and you can find the workflow in `.github/workflows/main.yml`.

## Changelog

2026-06-02: If your GitHub Actions checks hang during `Install Playwright Dependencies`, update Playwright from `1.58.1` to `1.60.0` in `client/package.json` and rerun the workflow.

## Pre-Requisites

There are three pre-requisites for this activity.

### GitHub Repository

Your team's deployment must take place within a private GitHub repository in our GitHub Classroom. To create your repository, each member of your team should follow these instructions (please review the instructions carefully first):

1. Sign in to GitHub.com, and then use [our invitation](https://classroom.github.com/a/vWAG9U_Y) to create a repository with the GameNite codebase. Check to see if one of your groupmates has already created a group - if so, select it to join it. Otherwise, create a repo using the format `su26-group-xyy` where X is your section number and YY is your group number. Be sure that your group number has the correct format (e.g., su25-group-101)

2. Check your email for the invitation to join the repo. After that, refresh the page, and it will show a link to your new repository, for example: https://github.com/neu-cs4530/summer26-project-group-xyy. Click the link to navigate to your new repository. This is the repository you will use for the project. Be sure that your repo name uses the format mentioned above and doesn't include duplicate words.

This repository will be private, and visible only to your team and the course staff. After the semester ends, you will be welcome to make it public - you will have complete administrative control of the repository.

### MongoDB Account

MongoDB Atlas is a cloud-based service that provides fully managed MongoDB databases. It allows you to easily deploy, manage, and scale MongoDB clusters without needing to handle server infrastructure, security, backups, or updates, making database management simpler and more efficient.

To use MongoDB Atlas, create a MongoDB account [here](https://account.mongodb.com/account/register).

After you register you will be asked to verify your email. The steps on how to create a MongoDB database and configure are provided below.

### Render.com Account

Render.com is a cloud platform that simplifies deploying and hosting web applications, APIs, and databases. It automatically manages servers, scaling, and security, allowing developers to easily build, deploy, and run applications without worrying about infrastructure management.

You can create a Render.com account [here](https://dashboard.render.com/register). Clicking on the "GitHub" button and sign up using the **same GitHub account** as the one used to create the GitHub project repository.

After you register you will be asked to verify your email. You might be asked to authorize the Render app for the "neu-cs4530" organization - choose your repository using the "Only select repositories" option, DO NOT choose "All repositories".

## Steps

You will first create the MongoDB database, and then setup the continuous deployment pipeline for the server and the client.

### Setup your MongoDB Database

1. Navigate to your [MongoDB Cloud Overview](https://cloud.mongodb.com).
2. Click on the "Project Overview" button.
3. Click on the "Create" button on the center of the screen. (If you don't see a "Create" button, make sure you are in the "Project Overview" section on the left navigation)
4. In the configuration options:
   1. Choose the "Free" tier.
   2. For the Name, provide a name such as "db-cs4530-summer26-XYY" (where XYY is your group number).
   3. Keep the Provider and Region the default values.
5. Click on "Create Deployment".
6. You will be prompted about connecting to your database.
   1. **Copy and save the username and password that is automatically generated, as it is shown only once and cannot be retrieved later.** You'll use this username and password in a later step. (If necessary, you can create new users users after the database has been created.)
   2. Click on "Create Database User".
   3. Click the "Close" button.
7. Wait for your database cluster to complete creation. Once complete, click on the "Database & Network Access" option in the left navigation (you may have to expand the "Security" section to see this), and then click on "IP Access List" under "Network Access"
8. Your current public IP address will be automatically present. Click the "EDIT" button, and then click "ALLOW ACCESS FROM ANYWHERE". (If you don't see this button, you can paste `0.0.0.0/0` as a new Access List Entry.) Click the "Confirm" button.
9. Click on the "Clusters" option in the left navigation. Then, click on the "Connect" button.
   1. Click on "Compass".
   2. Note the "connection string" — you will need to use your connection string in a later step. Make sure to replace `<db_password>` with the actual database password from step 6.

{: .note }
For simplicity, and since you're not handling sensitive data, the Network Access is set to allow connections from anywhere. However, for projects involving sensitive data, you should restrict access to only the necessary range of IP addresses.

You can optionally connect your locally deployed server to the cloud-hosted MongoDB database, which can be useful when developing a feature and testing it before deployment. To do this, update the `.env` created as [part of the IP2 setup](https://neu-se.github.io/CS4530-Fall-2026/assignments/ip2#12-setting-up-the-server-to-use-mongodb).

```
MONGO_STR=<add your connection string here>
MONGO_DB_NAME=GameNiteDev
```

If you get an error about an "unsettled top-level await", it means the connection string is not working. Make sure you've included your actual database password.

Starting the server will populate the database; at this point you should be able to "Browse Collections" on the MongoDB website, visit the GameNiteDev database, and see the collections `auth`, `chat`, `game`, etc.

Note: The .env file is not required for the Render.com setup. The above instructions are only if you want to connect the cloud MongoDB to your local (laptop) server.

### Setup your Server

1. Open the [Render Dashboard](https://dashboard.render.com/).
2. Click on "Create new project", and create a new project with a name such as "cs4530-s26-XYY" (where XYY is your group number).
3. From the top menu, click on the "+ New" button and click on "Web Service".
   1. For the Source Code, choose your project repository. In case you do not see your project repository, go to your GitHub account and authorize access to your project repository.
   2. For the Name, you can EITHER choose an unique name OR use the default.
   3. For the Project, select the project created earlier. For the environment, select Production or any default value.
   4. For Language, select "Node".
   5. For Branch, select "main".
   6. For Region, keep the default value.
   7. For Root Directory, leave it empty.
   8. For Build Command, type in `npm install; npm run build`.
   9. For Start Command, type in `npm start`.
   10. For Instance Type, choose the "Free" option.
   11. In the Environment Variables section, add three variables:
      - `NODE_VERSION` should be `24.13.1`
      - `MONGO_STR` should be the connection string from the previous step
      - `MONGO_DB_NAME` should be `GameNiteProd`.
   12. If you need to change any of these, you can do so from the tab called "Settings" (or "Environment")
4. Click "Deploy Web Service".
5. The URL of the your site will be displayed in purple just below near the top of the window in the "Logs" section.
6. When the logs indicate a successful deployment, you can visit the link to see your deployed site.
7. You can check the server's logs by going to the "Logs" section: the logs are the place to check if your server is not responsive.

{: .note }
Any servers running with the same `MONGO_STR` and `MONGO_DB_NAME` will share the same database. If you have multiple group members working on a similar feature, you may want to use the same database, or even the production database `GameNiteProd`. You can also pick a new `MONGO_DB_NAME` if you want to easily reset your application to the initial setup.

## Grading

Once your app is deployed, please show your deployment to your Mentor TA during your next meeting: you should show making a change through the deployed web interface, like updating a display name, and then show how that change has been recorded in the MongoDB database.