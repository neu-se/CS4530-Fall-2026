---
layout: page
title: Preliminary Project Plan
permalink: /assignments/project-plan
parent: Assignments
nav_order: 5
---

# Project Plan **Due Friday Oct 16 (5pm) ET**{: .label .label-red }

All projects will involve frontend and backend development of new features for our GameNite project.
Once teams have been formed, you and your team will decide what kind of new features you would like to build.
Your features should be something that can be implemented within the timeframe allotted (5 weeks, plus 2 week of planning), and will be implemented in a fork of the main codebase.
In the coming weeks, we will provide tutorials and instructions for you to run the entire application in a local development environment, and also to deploy it to the cloud.
Given that you will be up-to-speed on the GameNite codebase (and have been introduced to TypeScript, React, NodeJS, and testing frameworks like Vitest and Playwright),
and that you will have a team of four, we expect that the features that you propose will be more complex than the features implemented in the individual assignments.

A typical project may be larger than 3x of the combined size of all the individual projects (IP1+IP2+IP3) and may take anywhere from 150-250 hours (5 weeks, 3 or 4 members).

Sites that have functionality in common with GameNite include [Twitch](https://www.twitch.tv/), [Lichess](https://lichess.org/), the [Wavelength](https://www.wavelength.zone/) app, and even [Reddit](https://www.reddit.com/r/hexaword/), which has social games as well as a forum with comments.

Examples of features that students have proposed include:

- Introduce Markdown or images into forum threads
- Introduce more social features, such as friend requests and private direct messaging
- Provide users with more personalization features, including customizable profiles or user icons
- Create hidden or invite-only games
- Introduce leaderboards for site-wide activity or for game-specific participation
- Augment or replace the forum and threads with user-moderated communities that users can join
- Improve the accessibility of the UI for some class of user (e.g.: screen-reader user, low-vision user, user with color-blindness, or users only accessing the site through a mobile phone)
- Introduce time-based games like, such as [skribbl](https://skribbl.io/)-like pictionary games
- Add additional games (chess, checkers, go...)
- Allow games to be played against an algorithmic opponent
- Propose some other cool extension or modification to the website using the infrastructure in the starter code (REST, WebSockets, persistent database). Use your imagination!

All of these examples are user-centric features. Groups often want to explore a particular technology or technical change to the codebase; we strongly encourage this to be done with a particular user-focused goal in mind:

- If you want to modify code so that it is easy to switch to other persistence options (e.g. Firebase, Supabase, Postgres + GraphQL), this should be motivated by some user-centric goal or goals, like supporting text search over game chat or forum entries
- If you want to retarget the client to use the Chakra UI library, this should be motivated by some user-centric goal or goals, like improving accessibility

When considering your project, please keep in mind that you will be allowed to publicly post your project online after the end of semester: while your immediate audience for the project is the course staff, if you are ultimately looking for software engineering jobs or co-ops, this project can be a useful piece of your portfolio.

The project plan will include:

- Introductory problem statement
- User stories and acceptance criteria: high level description of how users will interact with your new feature.
- Work breakdown: Define engineering tasks that will be necessary to implement your new feature. Map each task to a sprint.

You should plan on spending the next two weeks (until the deadline of this assignment) in a "Sprint -1" in which you will undertake organizational and research tasks to help you decide on a project and formulate your plan.

You should be in contact with your assigned TA mentor before you submit the project plan, so they can answer questions and make sure you are on the right track. You may wish to share a draft of your plan with them _before_ the deadline to get early feedback.

Your team will self-organize, as agile teams should, and will enhance and adapt its plan during the project lifecycle.
As such, the primary goal of this document is to _begin_ the planning process, and _not_ to produce a detailed plan that must be followed precisely.
The course staff will provide regular feedback on your project to help ensure that the scope of your project is appropriate.

We list page _maximums_ for each section as general guidance of what we are willing to grade. Please do not feel compelled to use all of the pages provided, and remember that a diagram or table can be as expressive (or more) as a comparable amount of text.

## Problem Statement (max 1 page)

Your project plan should begin with a 1-3 paragraph introductory problem statement: what problem in GameNite do your (proposed) features solve? Provide a clear description of the feature(s) you are proposing.

When you review your project plan with course staff, you will be expected to have an even shorter "elevator pitch" version of this problem statement: if you had 30 seconds on an elevator with the CEO of GameNite, or with a potential investor, how would describe your overall plan as one clear theme? Catchy slogans (like GameNite's pitch of being "twitch for correspondence chess") aren't necessary, but can be a useful tool.

## User Stories and Conditions of Satisfaction (max 5 pages)

Given the problem statement, develop 4 or 5 user stories to describe your proposed features(s). User stories are high-level requirements specified in the following format

- _As a < stakeholder's role >,_
- _I want < some capability >,_
- _so that I can < get some benefit >._"

The user stories must be numbered (1,2,3,4...). Every team member should be able to distill every user story into just a few words, and explain how they connect to the overall problem statement of your group.

Each user story should include numbered conditions of satisfaction. (The conditions of satisfaction for user story #1 should be numbered 1.1, 1.2, 1.3, etc.) Please make sure that your conditions of satisfaction cover all the common cases, describe any unusual special cases, and can be turned into testable behaviors. Each condition of satisfaction must have a priority (**E**ssential, **D**esirable, or e**X**tension). The set of Essential items constitutes the “Minimum Viable Product” for your user story.

With feedback from course staff, you will revise your user stories and pick exactly three user stories that will form the core of your project. Half of the credit for implementing your project comes from delivering the minimum viable product for these three user stories.

We suggest that you should have no less than 10-12 conditions of satisfaction (per user story), and your essential COS be twice the number of desirable COS. You should also include a few extension COS in case you need to negotiate a replacement feature or if you can complete extra work. Your problem statement and description of user stories and conditions of satisfaction should be between 4-6 pages.

Your user stories and conditions of satisfaction should be laid out in a **table** for easy reference. 

Use the INVEST+E criteria to evaluate your user stories.

### Roles

For the purpose of this project, a role specifies a set of connected needs and desires inhabited by people who are not directly involved in the project’s implementation. People can inhabit a role from time to time (“card game enthusiast,” “forum moderator,” “site administrator,” “advertiser,” “subway commuter,” “parent of a college student”) or more permanently (“mobility impaired person,” “colorblind person”).

### Capabilities, Benefits, and Features

Remember that features are not capabilities or benefits, and that working with user stories should prompt you to revisit the features you plan to implement. Your problem statement may (and probably should) discuss features that you want to implement, and your conditions of satisfaction will definitely need to discuss some specifics of features.

## Work Breakdown (max 10 pages)

Given the project concept that you have chosen and the functionality that you expect to implement to satisfy your user stories, define a breakdown of the work that will be necessary to complete the project. The revised project plan will likely contain a significantly revised work breakdown. For the preliminary project plan, your work breakdown needs to clearly answer the following questions:

- How will your make sure your group is doing software engineering in a collaborative way?
- How will you schedule tasks in such a way that you don't get surprised by unexpectedly difficult tasks at the last minute?
- How will you deliver incremental value so that you're able to demo essential aspects of all your user stories by the end of Sprint 3?

Your work breakdown does not need to cover all your user stories, but should fully cover at least the three you think you are most likely to select.

The work breakdown includes all of the tasks necessary to accomplish the project, and will be an artifact that we will refer back to throughout the project to evaluate whether you are making satisfactory progress.
Consider all of the kinds of tasks that your team will need to perform, including knowledge acquisition, design, implementation, testing and documentation tasks.
It is hard to say (generically) how many work items are necessary.

Each task on the work breakdown should be assigned — on a preliminary basis! — to exactly one team member as the primary responsible party. This team member should provide a "T-Shirt" estimate for how long it will take (along with a justification for that estimate).
Consider the dependencies between tasks: perhaps an API needs to be designed and specified before implementation can begin; perhaps your development environment needs to be configured before anything else can proceed.

Assign tasks to sprints considering these dependencies. Given the preliminary nature of your plan, we do not expect that you will know all of the details about precisely how to implement your feature such that you could break it down into tasks that you feel could be implemented in a day or two. Large tasks (those which you can not provide a responsible estimate for) must be accompanied by smaller “research” tasks that can be performed early on in the project. You may wish to provide deadlines by which the task must either be refined into smaller tasks (based on new knowledge gathered), or reworked/abandoned.

It will be helpful for all concerned if your Project Plan lists the major unknowns or things that you expect to need help with, because this will help the TA provide more useful feedback for you. If you are uncertain that some tasks will be feasible, then be sure to include evaluation tasks earlier-on in the project that will allow for "go/no-go" decisions to move forward on a task or drop it.

For example: Consider if you were proposing the "job advertisement" feature, without the experience of having completed it. It might be difficult to consider how to break down a task like "Implement the frontend components for ad video playback" into something that you could commit to doing within a day or two. Given that this is a task that can be delayed until the end of the project (no other tasks depend on it), it would be wise to consider having some tasks early on in the project, such as: "Find react components that embed video ads," and "Implement simple video player that does not synchronize playback." Completing these smaller tasks early would let you both demonstrate that some forward progress is being made, and also allow you to create a much more responsible estimate for how that last, otherwise insurmountably large task would take.

Be realistic, and leave time for contingencies (including spring break and the time around the midterm exam in week 9).
Remember that you will need to have a demo prepared of your feature by project deadline - less than one month from the due date of this assignment.

We understand that it is quite difficult to estimate the technical complexity of a new project (as you are doing in the case of this course).
We will provide you with feedback on this preliminary project plan, which you will use to produce a revised project plan (due 2 weeks later).
Throughout the project period, teams will meet regularly with their dedicated TA Mentor, who will help track progress on a week-to-week basis and help to determine when adjustments to the project scope are needed.

Each work item should contain the following information:

- Task to be performed
- User story (or stories) that this task relates to
- Team member {primarily} responsible for completing the task
- T-shirt size estimate of how long will be needed to complete the task, using the following buckets:
  - Small: Can likely be completed by one team member in one sitting of less than 3-4 hours
  - Medium: Likely to require involvement of multiple team members, over the course of 1-2 days
  - Large: Currently unable to provide a responsible estimate.
- A brief (1-2 sentence max) justification of how you reached the size estimate of the task
- Milestone for delivering the task, chosen from one of the following:
  - Sprint 0: Oct 16-Oct 30
  - Sprint 1: Oct 31-Nov 6 (Sprint 1 is just a single week)
  - Sprint 2: Nov 7-Nov 20
  - Sprint 3: Nov 21-Dec 04

Your work breakdown may take the format of a simple textual list or a table. Pay attention to dependencies between different tasks and schedule them accordingly.

**Do not wait for your TA feedback to begin work.** You probably know more about the details of your project then they do.

**We strongly encourage you to schedule all development tasks during Sprints 1-3**.

## Submission

Your project plan should be submitted as a single PDF in Canvas to the assignment "Preliminary Project Plan."
Each team submits a single document to Canvas. Be sure to include your group number in your project plan.

## Grading

The project plan will account for 10% of your project grade, and will be graded out of 100 points. The grading of the project plan is further broken down as follows:

### Introductory problem statement (15 points):

- Receive full marks if
  - there is a narrative consisting of 1-3 paragraphs that describes the specific problems that your project aims to solve, and provides a clear description of the feature or features you are proposing.
- Receive partial credit if the narrative is present, but does not describe the problems that the project aims to solve, or does not give a clear description of the feature or features you are proposing.

### User Stories and Conditions of Satisfaction (45 points):

- Receive full marks if:
  - Each user story fits the problem statement.
  - Each user story has the appropriate structure.
  - Each user story includes conditions of satisfaction that cover the "normal" expected behavior of the feature, and any important error cases.
  - Each condition of satisfaction can be turned into one or more testable behaviors. (You don't have to enumerate testable behaviors.)
  - Each condition of satisfaction is marked with a priority (essential, desirable, extension).
  - Each user story must include one or more conditions of satisfaction marked as essential, desirable, and extension.
  - User stories and conditions of satisfaction satisfy the INVEST+E criteria for good user stories (construed quite broadly).

The user stories must be numbered (1,2,3) and each the conditions of satisfaction must likewise be numbered (1.1, 1.2, 1.3) and laid out in a table for easy reference.

Remember that you will get credit for delivering a minimum viable product (MVP) only if you deliver working implementations of all of your essential user stories and conditions of satisfaction. To receive full credit in the project, you must implement essential AND all desirable conditions of satisfaction. Essential and desirable features are worth 8% and 4% of the overall course grade respectively.

### Work breakdown (40 points):

Your work breakdown will be evaluated holistically on the following rubric:

#### Coverage of tasks needed (20 points):

Receive full marks if the work breakdown includes all (reasonably expected) tasks to implement your feature, considering these kinds of tasks:

- Background research
- Design of interfaces and data types
- Deployment of third-party services
- Implementation
- Testing
- Documentation

It is not possible to state generically for all projects whether _all_ of the above types of tasks are necessary.
However, we believe that this list is exhaustive (we do not expect other kinds of tasks).

#### Assignment of tasks (5 points):

Receive full marks if:

- Each element on the work breakdown is assigned to one team member (with primary responsibility).
- Each team member is assigned work that includes development / coding, even if working with pair programming.
- Each user story has tasks associated assigned to at least two group members.
- The distribution of tasks of each size are roughly similar between the whole team (no single person is assigned significantly more or fewer tasks of one size).

#### Sizing of tasks (10 points):

Receive full marks if each element on the work breakdown:

- Has a size estimate (small, medium, or large) that is provided by the team member assigned the task.
- Has a responsible justification for that estimation.
- Every "large" task:
  - Is accompanied by a reasonable explanation of why the team is unable to provide a responsible estimate
  - Is accompanied by at least one small or medium task, scheduled well-before the "large" task is due to be completed. We would expect that most of these research tasks are scheduled to sprint 0 or sprint 1.

#### Scheduling of tasks (10 points):

Receive full marks if:

- Each element on the work breakdown is assigned to a sprint.
- There are no obvious constraint violations (tasks that logically must happen before others should be scheduled before them).
- There are no "Large" tasks scheduled in sprint 0.
- Progress on every user story is planned in every main sprint (sprint 1, sprint 2, and sprint 3).
- The minimum viable product is scheduled to be completed before Sprint 3, or there is an explanation given for why this is not feasible in a specific instance.