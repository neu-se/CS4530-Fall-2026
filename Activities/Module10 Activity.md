---
layout: page
title: Mocks and Dependency Injection Activity
nav_exclude: true
---

# Testing Activity
This is an optional activity. You are encouraged to work on it for your learning but no submission is required. **There is no grade assigned to this activity.**

## Using mocks and spies to test GameNite
The overall code coverage for GameNite has always been kind of garbage; there's essentially no coverage of code used by websockets. The controller functions that interact with the socket.io library use dependency injection: the user-specific socket connection and server-wide socket server object are passed as arguments to the socket functions. We only needed a suitable mock `GameSocket` and `GameSocketServer` in order to test our functions. 

Place the [test file `chat.controller.spec.ts`]({{ site.baseurl }}{% link Activities/chat.controller.spec.ts %}) in the `server/tests` directory your IP2 codebase, and it will use the mock socket connection and socket server to test the `socketJoin` controller.

Your first task is to understand the tests for `socketJoin`. Can you think of how a suitable incorrect mutant implementation might pass these tests?

Your main task then is to write similar tests for `socketLeave`. If you're a little ambitious, you can also try writing some tests for `socketSendMessage`.

Submit your modified `chat.controller.spec.ts` file as directed by your instructor.

### Grading Rubric:
Any suitable attempt at testing the `socketLeave` controller will get partial credit, and any test that passes on our implementation and assesses the behavior of `socketLeave` suitably will get full credit.