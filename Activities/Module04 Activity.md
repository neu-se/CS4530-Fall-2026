---
layout: page
title: Persistent Transcript Server
nav_exclude: true
---

## Activity 4: Persistence Transcript Server

This activity is intended to supplement the CS4530 lecture on Web Application Architecture. You will need to have already completed the development environment setup for the class.

### Steps

Get the starter code by cloning the [`transcript-service-m03` repository from GitHub](https://github.com/neu-se/transcript-service-m03)

Modify the persistent Transcript server so that

1. Every grade carries with it a date, which is a Semester (which must be one of Fall, Spring, or Summer), and a year (which must be a 4 digit number greater than or equal to 2026).
2. A student may take a course multiple times.
3. Add a new route /api/getGPA which returns the GPA for a given ID. The GPA should wait each course equally, but if a student takes a course more than once, only the highest grade should count. As part of your code, include a comment explaining why you put the code for this feature where you did.
4. Add suitable tests to persistentService.spec.ts to test your solution to part (3)
5. When you are done, submit `persistentService.spec.ts` as required by your instructor.

### Grading Criteria: 10pts

10 points total. To be acded