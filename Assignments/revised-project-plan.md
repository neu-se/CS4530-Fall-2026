---
layout: page
title: Revised Project Plan
permalink: /assignments/revised-project-plan
parent: Assignments
nav_order: 6
---

# Revised Project Plan **Due Friday Oct 30, 5pm (ET)**{: .label .label-red }
You should use the feedback on your preliminary project plan to revise the scope of your project, and discuss any changes with your assigned TA. The goal of this assignment is to finalize the intended scope of your project based on these discussions and to outline the tasks that you will need to accomplish in order to complete your project.

Your assigned TA mentor will review your project plan and provide you with feedback on the scope and details provided in your preliminary plan.
In this deliverable, you will revise your project plan based on that feedback, and any preliminary research tasks that you have completed.
If there were any deficiencies or concerns noted by your TA mentor on your preliminary plan, you *must* address those concerns in this revised plan.
If you are unsure of how to address any of these concerns or if you have addressed them, please discuss them with your TA mentor before submitting this revised plan.

We list page *maximums* for each section as general guidance of what we are willing to grade. Please do not feel compelled to use all of the pages provided, and remember that a diagram or table can be as expressive (or more) as a comparable amount of text.

## Revised Problem Statement, User Stories and Conditions of Satisfaction (max 6 pages)
Your project plan should begin with a 1-3 paragraph introductory problem statement: what problem in GameNite do your (proposed) features solve? Provide a clear description of the feature(s) you are proposing. Include an analysis of the stakeholders, the values, and any value tensions. 

Given the problem statement, present three user stories to motivate your proposed features(s). User stories are high-level requirements specified in the following format

- _As a < stakeholder's role >,_
- _I want < some capability >,_
- _so that I can < get some benefit >._"

The user stories must be numbered (1,2,3). Every team member should be able to distill every user story into just a few words, and explain how they connect to the overall problem statement of your group.

Each user story should include numbered conditions of satisfaction. (The conditions of satisfaction for user story #1 should be numbered 1.1, 1.2, 1.3, etc.) Please make sure that your conditions of satisfaction cover all the common cases, describe any unusual special cases, and can be turned into testable behaviors. Each condition of satisfaction must have a priority (**E**ssential, **D**esirable, or e**X**tension). The set of Essential items constitutes the “Minimum Viable Product” for your user story.

We suggest that you should have no less than 10-12 conditions of satisfaction (per user story), and your essential COS be twice the number of desirable COS. You should also include a few extension COS in case you need to negotiate a replacement feature or if you can complete extra work. Your problem statement and description of user stories and conditions of satisfaction should be between 4-6 pages.

Your user stories and conditions of satisfaction should be laid out in a **table** for easy reference. 

Use the INVEST+E criteria to evaluate your user stories.

This revised project plan should be a standalone document (it is OK to copy/paste from the preliminary plan in this case).

### Roles

For the purpose of this project, a role specifies a set of connected needs and desires inhabited by people who are not directly involved in the project’s implementation. People can inhabit a role from time to time (“card game enthusiast,” “forum moderator,” “site administrator,” “advertiser,” “subway commuter,” “parent of a college student”) or more permanently (“mobility impaired person,” “colorblind person”).

### Capabilities, Benefits, and Features

Remember that features are not capabilities or benefits, and that working with user stories should prompt you to revisit the features you plan to implement. Your problem statement may (and probably should) discuss features that you want to implement, and your conditions of satisfaction will definitely need to discuss some specifics of features.


## Revised Work Breakdown (max 10 pages)
Given the project concept that you have chosen and the functionality that you expect to implement to satisfy your user stories, define a breakdown of the work that will be necessary to complete the project. This breakdown is required for all essential, desirable and extension tasks for 3 user stories that were chosen. For the revised project plan, your work breakdown needs to clearly answer the following questions:

- How will you make sure your group is doing software engineering in a collaborative way?
- How will you schedule tasks in such a way that you don't get surprised by unexpectedly difficult tasks at the last minute?
- How will you deliver incremental value so that you're able to demo essential aspects of all your user stories by the end of Sprint 2?
 
The work breakdown includes all of the tasks necessary to accomplish the project, and will be an artifact that we will refer back to throughout the project to evaluate whether you are making satisfactory progress.
Consider all of the kinds of tasks that your team will need to perform, including knowledge acquisition, design, implementation, testing and documentation tasks.
It is hard to say (generically) how many work items are necessary.

Each task on the work breakdown should be assigned to exactly one team member as the primary responsible party, and should come with "T-Shirt" estimate for how long it will take, along with a justification for that estimate. Consider the dependencies between tasks: perhaps an API needs to be designed and specified before implementation can begin; perhaps your development environment needs to be configured before anything else can proceed. 

Assign tasks to sprints considering these dependencies. Even at this stage, we do not expect that you will know all of the details about precisely how to implement your feature such that you could break it down into tasks that you feel could be implemented in a day or two, though it should be clearer now than it was for the preliminary project plan. Large tasks (those which you can not provide a responsible estimate for) must be accompanied by smaller “research” tasks that can be performed early on in the project. You may wish to provide deadlines by which the task must either be refined into smaller tasks (based on new knowledge gathered), or reworked/abandoned. Teams should try to keep the number of large tasks to minimum (if not zero).

It will be helpful for all concerned if your Project Plan lists the major unknowns or things that you expect to need help with, because this will help the TA provide more useful feedback for you. If you are uncertain that some tasks will be feasible, then be sure to include evaluation tasks earlier-on in the project that will allow for "go/no-go" decisions to move forward on a task or drop it.

For example: Consider if you were proposing the "job advertisement" feature, without the experience of having completed it. It might be difficult to consider how to break down a task like "Implement the frontend components for ad video playback" into something that you could commit to doing within a day or two. Given that this is a task that can be delayed until the end of the project (no other tasks depend on it), it would be wise to consider having some tasks early on in the project, such as: "Find react components that embed video ads," and "Implement simple video player that does not synchronize playback." Completing these smaller tasks early would let you both demonstrate that some forward progress is being made, and also allow you to create a much more responsible estimate for how that last, otherwise insurmountably large task would take.

Be realistic, and leave time for contingencies (including spring break and the time around the midterm exam in week 9).
Remember that you will need to have a demo prepared of your feature by project deadline - less than two months from the due date of this assignment.

Throughout the project period, teams will meet regularly with their dedicated TA Mentor, who will help track progress on a week-to-week basis and help to determine when adjustments to the project plan are needed.

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
  - Sprint 0: Oct 16-Oct 30 — This is now in the past, and your revised plan should reflect this. (See below.)
  - Sprint 1: Oct 31-Nov 6 (Sprint 1 is just a single week)
  - Sprint 2: Nov 7-Nov 20
  - Sprint 3: Nov 21-Dec 04

Your work breakdown may take the format of a simple textual list or a table. Pay attention to dependencies between different tasks and schedule them accordingly.

**Do not wait for your TA feedback to begin work.** You probably know more about the details of your project then they do.

**We strongly encourage you to schedule all development tasks during Sprints 1-3**.

All teams will be required to use project tracking software to track their progress. We will provides further instructions later.

**Mandatory update for all teams:** Be sure to include tasks related to UI Design. Even if you are not planning to revamp the entire UI for project, you should still add some tasks to improve the UI, as needed.

**Mandatory update for all teams:** Even if your work breakdown is entirely unchanged compared to the preliminary plan, please be certain to include updates on all "sprint 0" tasks (those which were scheduled to be completed before the due date of this revised plan). Many teams included research/learning tasks in the first week to help inform the rest of the work breakdown: you should be certain to revise your work breakdown based on what you have learned so far.

**Please note that in order to receive full credit for the final delivered product, each team is expected to deliver Minimum Viable Product (marked as essential) as well as additional feature(s) proposed in the project plan (marked as desirables). Please plan your work accordingly.**

## Submission 

Your revised project plan should be submitted as a single PDF on Canvas under the assignment "Revised Project Plan." (with team number in file name, e.g., Revised project plan - Team 101). Each team submits a single document. Make sure that your team number is listed at the beginning/title of the document and also added to filename (of the document).

## Grading
The revised project plan will account for 10% of your project grade, and will be graded out of 100 points. The grading of the revised project plan is further broken down as follows:

### Introductory problem statement (5 points): 
* Receive full marks if 
  * there is a narrative consisting of 1-3 paragraphs that describes the specific problems that your project aims to solve, and provides a clear description of the feature or features you are proposing.
* Receive partial credit if the narrative is present, but does not describe the problems that the project aims to solve, or does not give a clear description of the feature or features you are proposing.

### User stories (45 points):
* Receive full marks if:
  * Each user story fits the problem statement
  * Each user story has the appropriate structure.
  * Each user story satisfies the INVEST+E criteria for good user stories (construed quite broadly)
  * Each user story includes conditions of satisfaction that cover the "normal" expected behavior of the feature, and any important error cases
  * Each condition of satisfaction can be turned into one or more testable behaviors. (You don't have to enumerate testable behaviors.)
  * Each condition of satisfaction is marked with a priority (essential, desirable, extension)
  * Each user story includes one or more conditions of satisfaction marked as essential, desirable, and extension. 
  * Any deficiencies or concerns noted by your TA mentor on your preliminary plan are addressed

The user stories must be numbered (1,2,3) and each the conditions of satisfaction must likewise be numbered (1.1, 1.2, 1.3) and laid out in a table for easy reference.

Remember that you will get credit for delivering a minimum viable product (MVP) only if you deliver working implementations of all of your essential user stories and conditions of satisfaction. To receive full credit in the project, you must implement essential AND all desirable conditions of satisfaction. Essential and desirable features are worth 8% and 4% of the overall course grade respectively.


### Work breakdown (50 points):
Your work breakdown will be evaluated holistically on the following rubric:

#### Coverage of tasks needed (20 points):
Receive full marks if the work breakdown includes all (reasonably expected) tasks to implement your feature(s), considering these kinds of tasks: 
  * Background research 
  * Design of interfaces and data types
  * Deployment of third-party services
  * Implementation
  * Testing
  * Documentation

It is not possible to state generically for all projects whether *all* of the above types of tasks are necessary.
However, we believe that this list is exhaustive (we do not expect other kinds of tasks).

#### Assignment of tasks (10 points):
Receive full marks if:
* Each element on the work breakdown is assigned to one team member (as primary responsible party)
* Each team member is assigned work that includes development / coding, even if working with pair programming 
* Each user story has tasks assigned to at least two group members
* Each group member has tasks associated with at least two user stories (this requirement can be waived at a TA's discretion if discussed in advance).
* The distribution of tasks of each size are roughly similar between the whole team (no single person is assigned significantly more or fewer tasks of one size)
* Any deficiencies or concerns noted by your TA mentor on your preliminary plan are addressed

#### Sizing of tasks (10 points):
Receive full marks if each element on the work breakdown:
* Has a size estimate (small, medium, or large) that is provided by the team member assigned the task.
* Has a responsible justification for that estimation
* Every "large" task:
  - Is accompanied by a reasonable explanation of why the team is unable to provide a responsible estimate
  - Is accompanied by at least one small or medium task, scheduled well-before the "large" task is due to be completed. We would expect that most of these research tasks are scheduled to sprint 0 or sprint 1.
* Any deficiencies or concerns noted by your TA mentor on your preliminary plan are addressed

#### Scheduling of tasks (10 points):

Receive full marks if:

* Each element on the work breakdown is assigned to a sprint
* There are no obvious constraint violations (tasks that logically must happen before others should be scheduled before them)
* There are no "Large" tasks scheduled in sprint 1.
* Tasks scheduled to be completed before the deadline of this assignment have an update as to their status, and the work breakdown is updated to reflect the result of these tasks.
* Progress on every user story is planned in every sprint (sprint 1, sprint 2, and sprint 3).
* The minimum viable product is scheduled to be completed before Sprint 3, or there is an explanation given for why this is not feasible in a specific instance.
* Any deficiencies or concerns noted by your TA mentor on your preliminary plan are addressed