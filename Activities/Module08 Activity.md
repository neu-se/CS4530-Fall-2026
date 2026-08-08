---
layout: page
title: Async Activity
nav_exclude: true
---

# Simple Activity using async/await

Learning Objectives for this activity:

- Practice applying asynchronous programming concepts: promises, async/await
- Experiment with applying different ordering constraints in asynchronous code

## Overview

In this activity, you will experiment with asynchronous programming constructs in TypeScript.

### Getting started

As usual, download the [starter code]({{ site.baseurl }}{% link Activities/module08-async-matmult-activity.zip %}) and run `npm install`. 

### Instructions

Matrix multiplication is a common operation in many fields, including computer graphics, physics simulations, and machine learning. In this activity, you will implement matrix multiplication using asynchronous programming techniques in TypeScript.

The conventional way to multiply two matrices is a purely sequential algorithm. However, matrix multiplication can be parallelized because the computation of each element in the resulting matrix is independent of the others. This makes it a good candidate for exploring asynchronous programming.

We start with a version that does all the multiplication locally.  However, for the purposes of this activity, we have created a scenario where each multiplication operation is performed by a simulated remote service, using the `remoteProduct` function. 


You will find two different implementations of matrix multiplication in the starter code:
* `matrixMultiply.ts` - a purely sequential implementation.  This is what you probably learned in your linear algebra class.
* `matrixMultiplyAsync1.ts` - an implementation that calls out to `remoteProduct` for each individual multiplication operation, but awaits each result before proceeding to the next operation.  This is a straightforward asynchronous implementation, but it does not take full advantage of concurrency.

### Your tasks

1. Create a new file `matrixMultiplyAsync2.ts` which calls out to `remoteProduct` for each individual multiplication operation, but allows multiple multiplication operations to be in-flight concurrently.  For each cell in the answer, rather than waiting for each multiplication individually, assemble a list of promises (one for each multiplication that contributes to that cell), and then use `Promise.all` to send them out concurrently. Your program should wait for the results and then take their sum to obtain the value for that cell.  
2. You will also  find a file called `testAll.test.ts` which contains a suite of tests that can be used to verify the correctness of your implementation. You will see that this file contains a function that can run the same set of tests against multiple implementations of matrix multiplication.  Run the tests against your new implementation to verify its correctness.
3. Compare the performance of your three implementations: `matrixMultiply`, `matrixMultiplyAsync1`, and `matrixMultiplyAsync2`.  You can do this by creating a new file called `performanceTest.ts` that generates two medium-sized random matrices (e.g., I found 10x10 to be a good size) and measures the time taken by each implementation to multiply them. There are various ways to measure time in JavaScript/TypeScript; one simple way is to use `console.time` and `console.timeEnd`.  We've also included some of the timing code that we used in the slides. Make sure you are using the provided remoteProduct function when running your performance tests, as using a different implementation will give incorrect results.
4. (Optional) Create a third implementation, `matrixMultiplyAsync3.ts`, that takes concurrency one step further.  `Async2` computes each cell of the result concurrently, but it constructs the matrix sequentially, one row at a time.  In `Async3`, you can compute all the cells of the result concurrently.  This will require a bit more thought about how to organize your code, but it should be doable.  Again, run the tests to verify correctness, and compare performance with the other three implementations.


### Grading Rubric

This assignment is worth 10 points. Submit a zip file containing `matrixMultiplyAsync2.ts`, and a `performanceComparison.txt` summarizing your performance comparison (task 3).   If you did Task 4, include `matrixMultiplyAsync3.ts` as well, and put your performance comparison in `performanceComparison.txt`.

This assignment will be graded on a satisfactory/marginal/unsatisfactory basis, based on the following criteria:

### Satisfactory (10 points)
- `matrixMultiplyAsync2.ts` correctly implements matrix multiplication using asynchronous programming techniques, allowing multiple multiplication operations to be in-flight concurrently.
- All tests in `testAll.test.ts` pass for `matrixMultiplyAsync2.ts`.
- `performanceComparison.txt` provides a clear and accurate comparison of the performance of the three implementations, including actual measured timing values and an explanation of why the timings differ.

### Minimal (5 points)
- `matrixMultiplyAsync2.ts` correctly implements matrix multiplication using asynchronous programming techniques, allowing multiple multiplication operations to be in-flight concurrently.
- All tests in `testAll.test.ts` pass for `matrixMultiplyAsync2.ts`.
- `performanceComparison.txt` is incomplete or lacks clarity.

### Extra Credit (+2 points)
- `matrixMultiplyAsync3.ts` with further optimizations or enhancements.
- - All tests in `testAll.test.ts` pass for `matrixMultiplyAsync3.ts`.
- Include `matrixMultiplyAsync3.ts` in the submission and update `performanceComparison.txt` to compare all four implementations.

### Grading Notes
- The TAs will inspect your code to see if it meets the requirements.  They may or may not run your code, depending on time constraints.