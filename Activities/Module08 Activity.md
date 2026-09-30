---
layout: page
title: Bank Activity
nav_exclude: true
---

# Simple Activity using async/await

Learning Objectives for this activity:

- Observe how async and await do not always succeed in avoiding data races
- Fix the simple banking example to eliminate the data race

## Overview

In this activity, you will remove a data race from a simple banking application

## Getting started

As usual, download the [starter code](https://github.com/neu-se/M08-Bank-Activity.git) and run `npm install`. 

## Scenario

`src\AccountService.ts` implements the following operations: 
- `depositFunds(accountId:string, amount:number):Promise<void>` (If the account does not exist in the repository, it creates a new one)
- `withdrawFunds(accoundID:string, amount:number):Promise<WithdrawalReult>` 
- `getBalance(accountID:string):Promise<number>`.
The withdrawal result contains a `succeeded` field which is false if there are nsufficient funds to make the withdrawal.

`scenario.ts` executes the following sequence of activities using the service:

1. Creates a fresh account with a zero balance
2. Deposits $100 and cnfirm the balance
3. Fires two concurrent $75 withdrawals via Promise.all
4. Reports the final balance and whether it matches a correct system

## Your tasks

1. Run the test in `test/race.test.ts` using `npm run test` and observe the data race that causes the account to become overdrawn.
2. `src/simpleLock.ts` contains the code for a simple lock.  Modify `src/AccountService.ts` to use this lock so that `test/race.test.ts` does not ever result in an overdrawn account.
3. Turn in just your modified `src/AccountService.ts`

### Grading Rubric

This assignment will be graded on a satisfactory/marginal/unsatisfactory basis, based on the following criteria:

### Satisfactory (10 points)

When we run `test/race.test.ts` against your modified `src/AccountService.ts` if is always the case that only one of the two parallel withdawals succeeds.

### Minimal (5 points)

When we run `test/race.test.ts` against your modified `src/AccountService.ts` sometimes the duplicate withdrawal is rejected, but sometimes both withdrawal succeed, resulting in an overdrawn account.

### Grading Notes
- The TAs will run `test/race.test.ts` with your modified `src/AccountService.ts`.  They may nor may not inspect your code, and they may or may not ask you oral questions to see if you understand the code that you have turned in.  (You may treat the code in  `src/simpleLock.ts` as a black box.)
