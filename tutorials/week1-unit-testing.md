---
layout: page
title: Unit Testing with Vitest
permalink: /tutorials/week1-unit-testing
parent: Tutorials
nav_order: 3
---

This tutorial covers the basics on unit testing with Vitest. By the end of this tutorial, you will have an introduction to unit testing with Vitest, best practices, and some handy tricks and tips to use in your tests.

_Note:_ Run `npm i` on the handouts before proceeding to update/run the tests.

Contents:

- [Understanding Unit Testing](#understanding-unit-testing)
- [Testing with Vitest](#testing-with-vitest)
  - [Basics](#basics)
    - [Specs](#specs)
  - [Matchers](#matchers)
    - [.toEqual() vs .toBe() vs .toStrictEqual()](#toequal-vs-tobe-vs-tostrictequal)
  - [AAA](#aaa)
    - [Assemble](#assemble)
    - [Act](#act)
    - [Assert](#assert)
  - [Setup and Teardown](#setup-and-teardown)
  - [Mock Testing](#mock-testing)
    - [Spy](#spy)
    - [Mock](#mock)
    - [Stub](#stub)
  - [Testing Asynchronous Code](#testing-asynchronous-code)
    - [Promise](#promise)
    - [Testing Promise Rejections](#testing-promise-rejections)
    - [Callbacks](#callbacks)
  - [UI Testing](#ui-testing)
- [Setting up testing using Vitest in VSCode](#setting-up-testing-using-vitest-in-vscode)
  - [Features](#features)
  - [Requirements](#requirements)
  - [Installation](#installation)
    - [Direct Installation](#direct-installation)
    - [From Visual Studio Marketplace](#from-visual-studio-marketplace)
  - [Verifying Installation](#verifying-installation)
  - [Project Configuration](#project-configuration)
  - [Using the Extension](#using-the-extension)
  - [Debugging Tests](#debugging-tests)
  - [Extension Settings](#extension-settings)
  - [Troubleshooting](#troubleshooting)
- [General Guidelines For Writing Tests](#general-guidelines-for-writing-tests)


# Understanding Unit Testing
At some point, every programmer has wondered why they should spend time writing test cases instead of focusing on implementing a new feature. The reason for this is that it is important! In this tutorial, we'll go through several aspects of unit testing, with a focus on utilizing Vitest. Before we get into that, let's define unit testing and why it's so important in the real world.

Unit testing is not a new concept; it has been around for a long time. "Unit tests are often automated tests prepared and executed by software engineers to check that a portion of an application (referred to as a "unit") matches its design and behaves as expected," according to Wikipedia. So, to put it another way, it's a technique to undertake rigorous testing of every single function/module in isolation.

Unit testing techniques:
- **Black Box Testing** : It is a process of validating a function's input and output without any knowledge of its internal implementation details.
- **White Box Testing** : Unlike Black Box testing, white box testing focuses on testing the specific internal code flows, uncovering any unidentified error or bug in that component.
- **Gray Box Testing**  : Gray Box testing is a combination of the two above wherein partial knowledge of the internal code is needed. This strategy lowers a tester's reliance on a developer for every minor issue, allowing the tester to detect and resolve it alone.

# Testing with Vitest
## Basics


To understand the basics of unit testing, let us look at the file called 'calculator.ts' present in the directory src/services/math/. This file contains a class called Calculator with a method for add() defined as shown below:

```ts
  // Contents of src/services/math/calculator.ts

  export default class Calculator {
    public add(num1: number, num2: number): number {
      const result: number = num1 + num2;
      console.log("The result is: ", result);
      return result;
    }
  }
  ```

Let us write some tests for this code using Vitest. The test code will go into a file in the same directory titled 'calculator.test.ts'. Create this file now. This pattern of 'file-name.test.ts' is how you should name all of your test files when using Vitest.


All test files start with a suite. A suite is a collection of tests (or a logical grouping of tests). In Vitest, a suite is created by using the function `describe()`. The suite takes 2 arguments: the 1st being the description of the suite and the second being a callback function. Additionally, suites can be nested to form logical groups.
Suites can further be broken down into 3 components that we will explore in detail shortly:

1. Setup
2. Teardown
3. Test

Syntax:

```ts
  describe("Description of suite", () => {
    // The tests go here.
  });
  ```

Suites can be used to make debugging easier when you are using a large number of tests. Here is one recommended suite hierarchy:

- Top level describe should contain the file path after src.
- Second describe should contain the name of the Class/File being tested.
- Subsequent describe blocks should contain the name of the function being tested.

Using this hierarchy, the test file for the above example would look as follows:

```ts
  describe("services > math", () => {
    describe("Calculator", () => {
      describe("add()", () => {
        // Tests for add() go here.
      });
    });
  });
  ```

### Specs

A spec is an actual test that executes some code and asserts some result. A test is created using the keyword `it()` or `test()`. Similar to `describe()`, `it()` takes 2 arguments, the first being the description of the test and the second being a callback. Generally, we want to describe what the code _should_ do in the description of `it()` and assert the described behavior within the test. Each test can be broken down into 3 parts (Assemble, Act, Assert) which makes up the AAA pattern. Optionally, there may be a clean-up/teardown step after the assert.

Syntax:

 ```ts
  it("should check a specific behavior", () => {});
  ```

Let us write a simple test for our add() method to check 1 + 1 = 2.
We start by adding a spec to the suite we created previously.

```ts
  describe("services > math", () => {
    describe("Calculator", () => {
      describe("add()", () => {
        it("should return 2 when inputs are 1 and 1", () => {
          // Assemble
          // Act
          // Assert
        });
      });
    });
  });
  ```



## Matchers
### .toEqual() vs .toBe() vs .toStrictEqual()

All three matchers are used to test equality, though they have slight but important differences. To understand these differences, let us take a look at the example of Store.ts with the below code.

 ```ts
  export default class Store {
    private static _data: any = null;

    public static getData(): any {
      return Store._data;
    }

    public static setData(data: any): void {
      Store._data = data;
    }
  }
  ```

1.  Use .toEqual() to compare recursively all properties of object instances (also known as "deep" equality). It calls Object.is to compare primitive values, which is even better for testing than '===', the strict equality operator.
    This is the most commonly used matcher.

```ts
  import { describe, it, expect, beforeEach } from 'vitest';

  describe("utils > store", () => {
    describe("Store", () => {
      beforeEach(() => {
        Store["_data"] = undefined;
      });

      describe("setData()", () => {
        it("should assign the input data to Store._data", () => {
          const mockData = { key: "value" };

          Store.setData(mockData);

          expect(Store["_data"]).toEqual(mockData);
        });
      });

      describe("getData()", () => {
        it("should return an object equal to Store._data", () => {
          const mockData = { key: "value" };
          Store["_data"] = mockData;

          const returnedValue = Store.getData();

          expect(returnedValue).toEqual(mockData);
        });
      });
    });
  });
  ```

2.  Use .toBe() to compare primitive values or to check referential identity of object instances. It calls Object.is to compare values, which is even better for testing than '===', the strict equality operator.

 ```ts
  describe("getData()", () => {
    it("should return an object with the same reference as Store._data", () => {
      const mockData = { key: "value" };
      Store["_data"] = mockData;

      const returnedValue = Store.getData();

      expect(returnedValue).toEqual(mockData);
      expect(returnedValue).toBe(mockData); // Same reference
      expect(Store["_data"]).toBe(mockData);
    });
  });
  ```

3.  Use .toStrictEqual() to test that objects have the same types as well as structure.
    This checks for undefined in Objects and sparseness in Arrays.
    - { key: undefined } is not strictly equal to { }.
    - [ , 1] is not strictly equal to [undefined, 1].

 ```ts
  it("should return an object strictly equal to object stored in Store._data", () => {
    const mockData = { key: "value" };
    const mockDataWithUndefined = { key: "value", key2: undefined };
    Store["_data"] = mockData;

    const returnedValue = Store.getData();

    expect(returnedValue).toStrictEqual(mockData);
    expect(returnedValue).toEqual(mockDataWithUndefined);
    expect(returnedValue).not.toStrictEqual(mockDataWithUndefined);
  });
  ```
## AAA

The AAA pattern stands for **Assemble-Act-Assert**. You may also see this referred to as **Assemble-Act-Assess** in some materials (including lecture slides), as one typically assesses code behavior using assert statements. Both terms are used interchangeably in practice.

### Assemble

In order to run a test, we need to first assemble it. This may include creating instances of classes/variables, setting up test data for inputs, setting up spies/stubs/mocks (which will be covered in subsequent sections), or setting up the expected output. In simple cases, one may not need to assemble the test. This phase is very similar to the setup phase.

In our example, let us create an instance of the Calculator class as part of assembling the test.

```ts
  import { describe, it, expect } from 'vitest';
  import Calculator from "./calculator";

  describe("services > math", () => {
    describe("Calculator", () => {
      describe("add()", () => {
        it("should return 2 when inputs are 1 and 1", () => {
          const calculator: Calculator = new Calculator();

          // Act

          // Assert
        });
      });
    });
  });
  ```

### Act

In this step, we actually execute the function under test with required inputs and get the returned result (if any).

In our example, we will invoke the add() method with inputs (1, 1) and get the result.

 ```ts
  import { describe, it, expect } from 'vitest';
  import Calculator from "./calculator";

  describe("services > math", () => {
    describe("Calculator", () => {
      describe("add()", () => {
        it("should return 2 when inputs are 1 and 1", () => {
          const calculator: Calculator = new Calculator();

          const result: number = calculator.add(1, 1);

          // Assert
        });
      });
    });
  });
  ```

### Assert

Assertion is a statement that validates the behavior of our code by comparing the actual result against the expected results. There are many assertions provided by Vitest, including some useful assertions we will use throughout our tests. Some of these assertions are listed below:

- `expect(actual).toEqual(expected)` // Expects both entities to have the same value.
- `expect(actual).toBe(expected)` // Expects both entities to be the same.
- `expect(spy/stub/mock).toHaveBeenCalled()` // Expects a function being spied/stubbed/mocked to be invoked.
- `expect(spy/stub/mock).toHaveBeenCalledWith([arguments])` // Expects a function being spied/stubbed/mocked to be invoked with specified arguments.
- `expect(actual).toBeDefined()` // Expects the entity to be defined.
- `expect(actual).not.` // Negates the assertion. Can be chained with any matchers above
- `await expect(error causing code returning a promise).rejects.toThrowError()` // Waits for the error throwing code that returns promise (e.g. an API call) to throw the error and asserts the error was thrown.

A full list of matchers can be found [here](https://vitest.dev/api/expect.html).

In our example, we can use the .toEqual() matcher.

```ts
  import { describe, it, expect } from 'vitest';
  import Calculator from "./calculator";

  describe("services > math", () => {
    describe("Calculator", () => {
      describe("add()", () => {
        it("should return 2 when inputs are 1 and 1", () => {
          const calculator: Calculator = new Calculator();

          const result: number = calculator.add(1, 1);

          expect(result).toEqual(2);
        });
      });
    });
  });
  ```

## Setup and Teardown

Often in tests, we need some things to happen before a test actually runs and some things to happen after it. This may include resetting/initializing values, setting up test data, setting up spies/stubs/mocks, cleaning up variables after a test, or resetting spies/stubs/mocks. Sometimes these steps may need to be repeated for each test. This is where the setup and teardown can be especially useful.

Vitest Provides 2 methods for setup and 2 methods for teardown:

- beforeAll(): Runs one time before all the tests in a suite.
- beforeEach(): Runs before every test in a suite.
- afterEach(): Runs after every test in a suite.
- afterAll(): Runs once after all tests in a suite.

In our example, notice we created an instance of calculator in our Assemble phase. We will probably have multiple tests for the calculator that will require this instance. In order to avoid repeating this in every step, let us move this to the setup phase and add a teardown to clear this after all tests.

_Note:_ Use beforeEach()/afterEach() if the function/class stores state, and we need a clean instance for each test. In our case, calculator does not store any state, and we can share the same instance across tests with out any side effects. Hence, we will use beforeAll()/afterAll().

```ts
  import { describe, it, expect, beforeAll, afterAll } from 'vitest';
  import Calculator from "./calculator";

  describe("services > math", () => {
    describe("Calculator", () => {
      describe("add()", () => {
        let calculator: Calculator;

        beforeAll(() => {
          calculator = new Calculator();
        });

        afterAll(() => {
          (<any>calculator) = undefined;
        });

        it("should return 2 when inputs are 1 and 1", () => {
          const result: number = calculator.add(1, 1);

          expect(result).toEqual(2);
        });
      });
    });
  });
  ```

Let us add another test to cover a different scenario, such as adding negative numbers.

 ```ts
  import { describe, it, expect, beforeAll, afterAll } from 'vitest';
  import Calculator from "./calculator";

  describe("services > math", () => {
    describe("Calculator", () => {
      describe("add()", () => {
        let calculator: Calculator;

        beforeAll(() => {
          calculator = new Calculator();
        });

        afterAll(() => {
          (<any>calculator) = undefined;
        });

        it("should return 2 when inputs are 1 and 1", () => {
          const result: number = calculator.add(1, 1);

          expect(result).toEqual(2);
        });

        it("should return -2 when inputs are -1 and -1", () => {
          const result: number = calculator.add(-1, -1);

          expect(result).toEqual(-2);
        });
      });
    });
  });
  ```

## Mock Testing
As a project grows so do the interdependencies in the project. A function under test can have dependencies from various external entities. This may include other functions, network requests, database connections, or built-in connections. Spies, Stubs, and Mocks are ways of dealing with such external dependencies. You can read more on what you can do with spies/stubs/mocks [here](https://vitest.dev/api/vi.html).

### Spy

A spy is a watcher on a function that tracks various properties of the function being spied on. This can return information such as whether a function was invoked, how many times it was invoked, and what argument it was invoked with. A spy on a function is created using the syntax `const spy = vi.spyOn(object, 'methodName');`

_Note:_ The function being spied on actually executes.

In our example, we have an external dependency on console.log(). Let us add a spy and test for it.

 ```ts
  import { describe, it, expect, beforeAll, afterAll, vi } from 'vitest';
  import Calculator from "./calculator";

  describe("services > math", () => {
    describe("Calculator", () => {
      describe("add()", () => {
        let calculator: Calculator;

        beforeAll(() => {
          calculator = new Calculator();
        });

        afterAll(() => {
          (<any>calculator) = undefined;
        });

        it("should invoke console.log() with the result 2 for inputs 1 and 1", () => {
          const logSpy = vi.spyOn(console, "log");

          const result: number = calculator.add(1, 1);

          expect(logSpy).toHaveBeenCalledWith("The result is: ", result);

          logSpy.mockRestore();
        });
      });
    });
  });
  ```

### Mock

A mock is a function which replaces an existing function. In our example, if we wanted to change the behavior of console.log() for our tests, we can do so using a mock. A mock implementation can be substituted for a spy or a vi.fn(). The syntax is as below:

 ```ts
  spy.mockImplementation(() => {
    // new function body goes here.
  });
  ```

_Note:_ The function being mocked does not execute.
In our example, if we wanted to replace the behavior of console.log(), we can do so as shown:

```ts
  it("should invoke console.log() with the result 2 for inputs 1 and 1", () => {
    const logSpy = vi.spyOn(console, "log");
    logSpy.mockImplementation(() => {
      // This will no longer print to console.
    });

    const result: number = calculator.add(1, 1);

    expect(logSpy).toHaveBeenCalledWith("The result is: ", result);

    logSpy.mockRestore();
  });
  ```

_Warning:_ Watch out for circular dependencies in mock implementations.

### Stub

A stub is a special kind of mock which does not require an alternate implementation but instead returns some value that we specify. When a stub gets invoked, it does not invoke the actual function, but returns the desired value instead. The syntax is as below:

```ts
  spy.mockReturnValue(someValue);
  ```

To return a promise, we can use:

 ```ts
  spy.mockResolvedValue(someValue);
  ```
  This can be especially handy when stubbing Axios requests.

Using a stub in our example simply prevents console.log() from being executed, since it does not return a value anyway.

  ```ts
  it("should invoke console.log() with the result 2 for inputs 1 and 1", () => {
    const logSpy = vi.spyOn(console, "log");
    logSpy.mockReturnValue();

    const result: number = calculator.add(1, 1);

    expect(logSpy).toHaveBeenCalledWith("The result is: ", result);

    logSpy.mockRestore();
  });
  ```

## Testing Asynchronous Code

### Promise

In previous tutorials, we have used Axios to make http requests which return promises. This is how we can write tests for axios requests. Consider the example below:

 ```ts
  import axios from "axios";
  import Store from "../../utils/store/store";

  export default class HttpService {
    public getData(): Promise<any> {
      return axios.get("/myUrl");
    }
  }
  ```

We can test the above code as follows:

 ```ts
  // Assuming we have done the setup as in previous tests
  import { describe, it, expect, vi } from 'vitest';

  describe("getData()", () => {
    it('should invoke axios.get() with "myUrl"', async () => {
      const getStub = vi
        .spyOn(axios, "get")
        .mockResolvedValue({ status: 200, data: {} });

      await httpService.getData();

      expect(getStub).toHaveBeenCalledWith("/myUrl");
    });

    it("should return the status as 200", async () => {
      const getStub = vi
        .spyOn(axios, "get")
        .mockResolvedValue({ status: 200, data: {} });

      const response = await httpService.getData();

      expect(response.status).toEqual(200);

      getStub.mockRestore();
    });
  });
  ```

#### Testing Promise Rejections

When testing async functions that are expected to throw errors or reject promises, you need to use `await expect(...).rejects.toThrowError()`. This is a common source of bugs in tests — if you forget to use the correct pattern, your test may pass even when the code doesn't behave as expected.

Consider a function that validates user authentication:

```ts
  export async function enforceAuth(credentials: { username: string; password: string }): Promise<{ _id: string; username: string }> {
    const user = await validateCredentials(credentials);
    if (!user) {
      throw new Error('Invalid credentials');
    }
    return { _id: user.id, username: credentials.username };
  }
  ```

We can test both successful authentication and failed authentication as follows:

```ts
  import { describe, it, expect } from 'vitest';
  import { enforceAuth } from '../../src/services/auth.service';

  describe('enforceAuth', () => {
    it('should return a user and id on good auth', async () => {
      const user = await enforceAuth({ username: 'user1', password: 'pwd1111' });
      expect(user).toStrictEqual({ _id: expect.any(String), username: 'user1' });
    });

    it('should raise on bad auth', async () => {
      await expect(enforceAuth({ username: 'user1', password: 'no' })).rejects.toThrowError();
    });
  });
  ```

**Important:** Notice the pattern for testing rejections:
- The test function must be `async`
- You must `await` the `expect()` call
- Use `.rejects.toThrowError()` to assert that the promise rejects with an error

A common mistake is writing the test like this (which won't work correctly):

```ts
  // ❌ INCORRECT - This test will pass even if the function doesn't throw!
  it('should raise on bad auth', () => {
    expect(() => enforceAuth({ username: 'user1', password: 'no' })).toThrow();
  });
  ```

The correct pattern ensures the test properly waits for the async rejection:

```ts
  // ✅ CORRECT - Properly tests async rejection
  it('should raise on bad auth', async () => {
    await expect(enforceAuth({ username: 'user1', password: 'no' })).rejects.toThrowError();
  });
  ```

_Note:_ You can return different values for subsequent calls to a stub.

Occasionally, you may run into situations where an http request is made but no promise is returned. This is often found in cases involving "fire and forget" calls or a central store with an Observable pattern implementation (e.g. Redux with react). We cannot await a function that does not return a promise. However, we can use fake timers to simulate passage of time to test such asynchronous behavior. Consider the example below:

```ts
  import axios from "axios";
  import Store from "../../utils/store/store";

  export default class HttpService {
    public getData(): Promise<any> {
      return axios.get("/myUrl");
    }

    public getDataAndSetStore(): void {
      axios.get("/myUrl").then((res) => {
        Store.setData(res.data);
      });
    }
  }
  ```

We can test the above functionality as follows:

 ```ts
  describe("getDataAndSetStore()", () => {
    it('should invoke axios.get() with "myUrl"', async () => {
      const getStub = vi
        .spyOn(axios, "get")
        .mockResolvedValue({ status: 200, data: {} });

      await httpService.getDataAndSetStore();

      expect(getStub).toHaveBeenCalledWith("/myUrl");
    });

    it("should set the data in store", async () => {
      const addDataStub = vi.spyOn(Store, "setData").mockImplementation();
      const getStub = vi
        .spyOn(axios, "get")
        .mockResolvedValue({ status: 200, data: "myData" });
      vi.useFakeTimers();

      httpService.getDataAndSetStore();
      vi.runAllTimers();
      await Promise.resolve();

      expect(addDataStub).toHaveBeenCalledWith("myData");

      addDataStub.mockRestore();
      getStub.mockRestore();
      vi.useRealTimers();
    });
  });
  ```

You can read more about Vitest timers [here](https://vitest.dev/api/vi.html#vi-usefaketimers).

### Callbacks

Callbacks are one of the most commonly used patterns for asynchronous programming in JavaScript/TypeScript. Consider the below callback function use case:

```ts
test('Check if I am a true husky', () => {
  function callback(data) {
    expect(data).toBe('I am from Northeastern!');
  }
  fetchData(callback);
});
```
Here, fetchData() is a function that takes a callback and would call that callback function later in its implementation. Now consider 2 scenarios:

case 1: 
```ts
fetchData(callback) {
  setTimeout(()=>{
    callback('I am from Northeastern!');
  }, 1000);
}
```

case 2: 
```ts
fetchData(callback) {
  setTimeout(()=>{
    callback('I am not from Northeastern!');
  }, 1000);
}
```

The test case would still pass in either of the above scenarios since fetchData() is an async function, which means the program will not wait for the call to complete.

The correct way to test a callback would be using the argument `done` in the test like shown in below example:

```ts
test('Check if I am a true husky', (done) => {
  function callback(data) {
    expect(data).toBe('I am from Northeastern!');
    done();
  }
  fetchData(callback);
});
```

Now, the program would wait for done to be invoked. This implementation would correctly test both the above scenarios.

## UI Testing
Testing UIs can be very tricky, especially when we want to test features involving user interaction (e.g. a user clicking on a button). However, there are some useful tools that can help us. The [React Testing Library](https://testing-library.com/docs/react-testing-library/intro/) provides many helpful features that can help us.
```ts
import {render, screen} from '@testing-library/react'
import Counter from './Counter'
it('renders the Counter component correctly', async () => {
  render(<Counter />);

  // Will throw error if not found
  screen.getByText("Count: 0")
  screen.getByText("Click me!")
})
```
Above is a very simple test to ensure that our Counter component renders as expected without any user input. Suppose now that we wanted to test user interaction with the page:

```ts
import {render, fireEvent, screen} from '@testing-library/react'
import Counter from './Counter'
it('correctly renders the updated count after the user clicks the button', async () => {
  render(<Counter />);
  screen.getByText("Count: 0")
  fireEvent.click(screen.getByRole('button'))
  screen.getByText("Count: 1")
})
```

A full list of testing functions from React Testing Library can be found [here](https://testing-library.com/docs/dom-testing-library/cheatsheet/).
# Setting up testing using Vitest in VSCode

Testing can sometimes get cumbersome as the user is expected to remember all the options provided by Vitest to run a specific set of tests, or otherwise the user will have to run the entire test suite just to verify the result of a single test case. Not anymore!

With the official [Vitest extension](https://marketplace.visualstudio.com/items?itemName=vitest.explorer), you have complete control over the way you want to run tests, with many features that visually inform the users about which specific line is failing with what error.

## Features

- **Run, debug, and watch tests** directly in Visual Studio Code
- **Inline test results** - Show individual pass/fail status next to each test
- **Error highlighting** - Highlights errors next to the `expect` functions
- **Inline console.log display** - Console logs appear inline in the editor next to the code that produced them
- **Coverage support** - Run tests with code coverage (requires VS Code >= 1.88)
- **Continuous run mode** - Watch mode for running tests on file changes
- **Test filtering** - Use `@open` tag to only show tests open in the editor

## Requirements

- Visual Studio Code version >= 1.77.0
- Vitest version >= v1.4.0
- Node.js version >= 18.0.0

## Installation

### Direct Installation

1. Open Visual Studio Code and go to the Extensions tab (`Cmd+Shift+X` on macOS, `Ctrl+Shift+X` on Windows/Linux).
2. Search for "Vitest" (publisher: "Vitest").
3. Click "Install".

### From Visual Studio Marketplace

1. Visit [Vitest - Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=vitest.explorer) and click "Install".
2. Allow the browser to open VSCode.
3. Once VSCode is open, click "Install".

Once installed, the extension should work out of the box without any extra configuration for most projects with Vitest configured.

## Verifying Installation

After installation (VSCode restart may be required):

1. Open the **Testing** view by clicking the flask/beaker icon in the Activity Bar (left sidebar), or open the Command Palette (`Cmd+Shift+P` / `Ctrl+Shift+P`) and run **"Testing: Focus on Test Explorer View"**.
2. You should see your test files and test suites listed in the Test Explorer.
3. Green checkmarks indicate passing tests, red X marks indicate failures.

If tests don't appear, open the Command Palette (`Cmd+Shift+P` / `Ctrl+Shift+P`) and run **"Vitest: Start All Runners"**.

## Project Configuration

For the extension to work, your project needs Vitest configured. Create a `vitest.config.ts` file in your project root:

```ts
import { defineConfig } from 'vitest/config';

export default defineConfig({
  test: {
    globals: true,
    environment: 'node',
    include: ['**/*.{test,spec}.{js,mjs,cjs,ts,mts,cts,jsx,tsx}'],
  }
});
```

Add test scripts in your `package.json`:

```json
{
  "scripts": {
    "test": "vitest",
    "test:watch": "vitest --watch",
    "test:coverage": "vitest --coverage"
  }
}
```

## Using the Extension

### Running Tests from the Testing View

The Testing view in the sidebar provides a tree view of all your tests:

- **Run All Tests**: Click the play button at the top to run all tests
- **Run Single Test/Suite**: Hover over a test or suite and click the play button
- **Run Tests with Coverage**: Click the coverage icon to run tests with code coverage
- **Continuous Run**: Click the "eye" icon to enable watch mode - tests will rerun when files change

### Running Tests from Test Files

When viewing a test file, you'll see icons in the gutter (left margin) next to each test:

- **Click the icon** to run that specific test
- **Right-click the icon** for more options:
  - `Run Test` - Execute the test
  - `Debug Test` - Start a debugging session
  - `Run with Coverage` - Run with code coverage
  - `Reveal in Test Explorer` - Find the test in the Testing view

### Keyboard Shortcuts

VS Code provides testing commands you can access via the Command Palette (`Cmd+Shift+P` / `Ctrl+Shift+P`):

- **Test: Run All Tests** - Run all tests in the workspace
- **Test: Run Test at Cursor** - Run the test at the current cursor position
- **Test: Rerun Last Run** - Re-run the last executed tests
- **Test: Debug Test at Cursor** - Debug the test at the current cursor position

You can also view and customize keyboard shortcuts for these commands by opening the Keyboard Shortcuts editor (`Cmd+K Cmd+S` / `Ctrl+K Ctrl+S`) and searching for "test".

## Debugging Tests

The Vitest extension makes debugging tests straightforward:

1. **Set Breakpoints**: Click in the gutter (left of line numbers) to set breakpoints in your test or source code.

2. **Start Debugging**: 
   - Right-click on the test icon in the gutter and select "Debug Test"
   - Or hover over a test in the Testing view and click the debug icon (bug icon)

3. **Use the Debugger**: When the debugger pauses at a breakpoint:
   - Hover over variables to see their values
   - Use the Debug Console to evaluate expressions
   - Step through code using the debug toolbar (Step Over, Step Into, Step Out)

4. **Debug Configuration**: The extension automatically configures debugging. If you need custom settings, you can modify these in your VS Code settings:
   - `vitest.debuggerPort` - Port for the debugger (default: 9229)
   - `vitest.debugExclude` - Glob patterns to exclude from debugging

## Extension Settings

You can customize the extension behavior in VS Code settings (`Cmd+,` / `Ctrl+,`):

| Setting | Description | Default |
|---------|-------------|---------|
| `vitest.rootConfig` | Path to your Vitest config file | Auto-detected |
| `vitest.nodeExecutable` | Path to Node.js executable | Auto-detected |
| `vitest.showImportsDuration` | Show module import times | `true` |
| `vitest.applyDiagnostic` | Show error squiggly lines | `true` |

### For Monorepo Projects

If you're working with a monorepo, configure a [Vitest workspace](https://vitest.dev/guide/workspace):

1. Create a `vitest.workspace.ts` file at the root:

```ts
import { defineWorkspace } from 'vitest/config';

export default defineWorkspace([
  'packages/*/vitest.config.ts',
]);
```

2. Set the workspace config in VS Code settings:
```json
{
  "vitest.workspaceConfig": "./vitest.workspace.ts"
}
```

## Troubleshooting

**Tests not appearing in Test Explorer:**
- Ensure Vitest is installed (`npm install -D vitest`)
- Check that your config file is named correctly (`vitest.config.ts` or `vite.config.ts`)
- Run "Vitest: Start All Runners" from the Command Palette

**Extension not finding Vitest:**
- Set `vitest.vitestPackagePath` to the path of Vitest's `package.json` in your `node_modules`

**Debugging not working:**
- Ensure source maps are enabled in your config
- Check that the `vitest.debuggerPort` is not in use




# General Guidelines For Writing Tests

> **_Note:_ The following will be used as a reference when grading assignments.**

1. Tests should be hermetic.
   - Reduce flakiness.
   - Flaky tests are those that fail intermittently:
     - Nondeterminism (e.g., hash codes, random numbers);
     - Timing issues (e.g., threads, network).
     - Availability of Resources
2. Tests should be clear.
   - After failure, should be clear what went wrong.
3. Tests should be scoped as small as possible.
   - Faster and more reliable.
4. Tests should make calls against public APIs.
   - Or they become brittle
   - Brittle tests are those that are not self-contained:
     - Ordering of tests (e.g., assume prior state)


> **_Note:_ The following will not be used as a reference when grading assignments. But you should try following these guidelines as much as you can.**

1. Write tests based on the expected behavior, not based on the interpretation/implementation of it.
2. Test assertion (expect) should match the test description.
3. Each spec should test only 1 thing (preferably with 1 assertion per test).
4. Organize tests using suites (i.e. each method has its own suite).
5. Use setup and teardown functions to reduce code duplicity.
6. Code duplicity in tests is preferred over complicated logic to reduce it.
   - If your tests need tests, they have no value.
7. Cover the happy path for your code first.
   - Follow up with edge cases.
   - End with error scenarios.
8. Mock/Stub all external dependencies.
   - Clear the mocks after each test.
9. If large test data is being used, ensure clean-up after tests to prevent memory leaks.
10. Code coverage is a deceptive measure. 100% coverage does not mean 100% tested code.
11. A well designed test suite improves the quality and reliability of code.
