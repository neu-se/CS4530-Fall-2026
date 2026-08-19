---
layout: page
title: Mutation Testing with Stryker
nav_exclude: true
---

## Activity 3.2: Mutation Testing with Stryker

This activity is intended to supplement the CS4530 lecture on mutation testing development. You will need to have already completed the development environment setup for the class.

### Steps

1.  Get the starter code by cloning the [`transcript-service-m03` repository from GitHub](https://github.com/neu-se/transcript-service-m03)
2.  Run `npm install` inside the directory that is created when you unzip the download.
3.  Check that every member of the group can run

    ```
    npm run test
    ```

    and see that the tests pass and give full branch and line coverage.

4.  Check that every member of the group can run

    ```
    npm run stryker
    ```

    and see that 7 variants survive, associated with lines 40, 43, 53, 54, 70, 121, and 125.

    Classify the surviving mutants into innocuous (didn’t introduce a bug) and non-innocuous (did introduce a bug).
    Note: Student IDs should be positive.

5.  In a new file `src/additional.spec.ts`, write tests that will kill each non-innocuous mutant. For each mutant that you classified as innocuous, write a comment explaining why you think it is innocuous (no test needed for innocuous mutants). You can rerun `npm run test` to make sure your tests still pass, and rerun `npm run stryker` to see if your tests kill identify the bad mutants.

6. When you are done, submit `src/additional.spec.ts` as required by your instructor.

### Grading Criteria: 10pts

10 points total. -2 points for each mutant incorrectly classified or improperly handled (not killed if non-innocuous, or not explained if innocuous).