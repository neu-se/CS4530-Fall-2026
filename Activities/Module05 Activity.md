---
layout: page
title: React
nav_exclude: true
---

## React Activity - Todo Tracker

This activity is designed to give you practice with React.  You will enhance the ToDo app that was discussed in lecture. 

### Steps

To get started, download the [starter Code]({{ site.baseurl }}{% link Activities/module-05-react-activity.zip %}). Run the command `npm install`, and then `npm run dev`. The development server should start, and If you open your browser to `localhost:3000`,it will start running the app in `src/App.tsx`. 

In the ToDoApp, make the following three enhancements:

1. Currently the "priority" field will accept any value. Modify it so that the priority must be a number. (Hint: `NumberInput` is your friend)
2. Add a button that will sort the todo items by priority, lowest number first
3. Add an entry field that will take a number and delete all the todo items with priorities **greater** than that number. (We are assuming that priority 1 means the thing that has to be done first.)

When you are done, copy the files from `Apps/ToDoApp` into a fresh folder, and submit a zip file with those files only. The assignment has been configured to accept zip files only. Do NOT do  `npm run zip` and submit that.  If you do, you will get 0 points.

### Grading Rubric:
This assignment is worth 10 points.  

If you do any *two* of the 3 enhancements listed in the assignment, you get 5 points

If you do all 3 of the enhancements, you get 10 points.