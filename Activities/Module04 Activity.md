---
layout: page
title: Modifying the C-S-R Server
nav_exclude: true
---

## Activity 4: Modifying the Persistent Server

This activity is intended to supplement the CS4530 lecture on Web Application Architecture. You will need to have already completed the development environment setup for the class.

### Steps

Get the starter code by cloning the [Module 04 repository from GitHub](https://github.com/mwand/m04-csr-examples-fall-2026.git)

Modify the persistent transcript server at `src/withPersistence` so that

1. Every grade carries with it a date, which is a Semester (which must be one of Fall, Spring, or Summer), and a year (which must be a 4 digit number greater than or equal to 2026).[1 pt]
2. A student may take a course multiple times. [2 pts]
3. Add a new route /api/getGPA which returns the GPA for a given ID. The GPA should weight each course equally, but if a student takes a course more than once, only the highest grade should count. If the student has no grades, getGPA returns 0. As part of your code, include a comment explaining why you put the code for this feature where you did. [2 pts]
4. Add suitable tests to persistentService.spec.ts to test your solution to part (3) [5 pts]
5. When you are done, submit a zip file containing the whole `src/withPersistence` folder (including `persistentService.spec.ts`) and your `src/types.ts` file, as required by your instructor.

### Grading Criteria: 10pts

10 points total, as indicated above.
