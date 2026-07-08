---
layout: page
title: Guide to API Requests and Installing Postman
permalink: /tutorials/week1-apirequests-postman
parent: Tutorials
nav_order: 4
---

# Tutorial: Guide to API Requests and Installing Postman

## Contents

- [Introduction to API Requests and Postman](#introduction-to-api-requests-and-postman)
- [Breakdown of an API Request](#breakdown-of-an-api-request)
- [Authentication in APIs](#authentication-in-apis)
- [Testing API Endpoints](#testing-api-endpoints)
- [Steps to Install Postman](#steps-to-install-postman)
- [Using Postman: Basic Steps](#using-postman-basic-steps)
- [Setting Up Authentication in Postman](#setting-up-authentication-in-postman)
- [Setting up environment Variables in Postman](#setting-up-environment-variables-in-postman)
- [Saving API Requests and Using History](#saving-api-requests-and-using-history)
- [Organizing Requests into Collections](#organizing-requests-into-collections)
- [Recommended Tools](#recommended-tools)

## Introduction to API Requests and Postman

**APIs** (Application Programming Interfaces) are essential tools that allow different software applications to communicate with each other. As developers, it's crucial to understand how to interact with APIs, which involves making API requests. API requests are structured interactions where one software sends a request to retrieve or send data to another.

**Postman** is a popular API testing tool that allows developers to build, test, and modify APIs quickly and easily. It provides an interface to interact with APIs and simplifies API development. Postman supports making requests like **GET**, **POST**, **PUT**, **DELETE**, and more.

With this guide, you can:

- **Understand the basics** of making GET and POST requests to an API.
- **Learn how to use Postman** to send requests and test APIs.
- **Test API responses** to ensure that they return the expected results.

### Types of API Requests:

There's a whole [vocabulary of HTTP requests](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods), but GET and POST are the two most important:

- **GET**: Retrieves data from an API. It's commonly used when you want to fetch information without making any changes.
  - _Example_: Use a GET request to retrieve a list of videos related to the one you're currently watching on a streaming platform (e.g., `GET /videos/related`).
- **POST**: Submits new data to an API to create a resource. It's used when you need to send data to the server to create something new.
  - _Example_: Use a POST request to save a newly uploaded video on a platform (e.g., `POST /videos`).

Each of these request types serves a specific purpose in API interactions, and Postman allows you to easily switch between them to test and build your APIs.

## Breakdown of an API Request

Each API request has key components:

### 1. URL

For this URL -> `https://localhost:8000/api/users`

The URL defines the location of the API you're interacting with:

- **Protocol** (`https://`)
- **Domain** (`localhost`)
- **Port** (`8000`)
- **Endpoint** (`/api/users`)

### 2. Method

Defines the action type:

- **GET**: Retrieves data
- **POST**: Submits new data
- **PUT**: Updates data
- **DELETE**: Deletes data

### 3. Parameters (GET) vs. Body (POST)

- **GET** sends data as **query parameters** in the URL:
  https://api.example.com/users?age=25
  In this example, `age=25` is a query parameter used to filter 25 year old users from the list of users.

- **POST** sends data in the **body** (usually JSON). In this example, username and password entered by the user is getting sent to the server for log in.

```json
{
  "username": "user",
  "password": "password"
}
```

### 4. Headers

Headers provide additional information about the request or the client making it. They help the server understand the request. Some common headers include:

- **Content-Type**: Specifies the format of the request body (e.g., `application/json` for JSON data).
- **Authorization**: Contains credentials like [API keys](https://www.ibm.com/think/topics/api-key) or [tokens](https://www.okta.com/identity-101/what-is-token-based-authentication/) required to access certain endpoints.

  - _Example_:
    ```
    Authorization: Bearer <your-api-token>
    ```

- **Accept**: Specifies the format in which the client expects the server to return the response (e.g., `application/json`).
  - _Example_:
    ```
    Accept: application/json
    ```

### 5. Response

After the server processes the request, it sends back a **response**. The response typically includes:

- **Status Code**: A number indicating the result of the request.

  - Common status codes:
    - `200 OK`: The request was successful.
    - `201 Created`: The resource was successfully created (used for POST requests).
    - `400 Bad Request`: There was an error in the request.
    - `404 Not Found`: The resource could not be found.
    - `500 Internal Server Error`: An error occurred on the server.

- **Response Body**: Contains the data returned by the API, usually in JSON format. For example, when creating a new user, the server might return the new user data as response like this:
  ```json
  {
    "id": 1,
    "username": "newuser",
    "email": "newuser@example.com"
  }
  ```

## Authentication in APIs

Common Authentication Methods

1. API Key Authentication

```
Headers:
X-API-Key: your-api-key-here
```

2. Bearer Token (JWT)

```
Headers:
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

3. Basic Authentication

```
Headers:
Authorization: Basic base64(username:password)
```

4. OAuth 2.0
   More complex flow involving authorization servers and access tokens.

### Additional things to note:

- See this [Mozilla documentation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status) for further information on status codes.
- It is good practice to use [environment variables](https://medium.com/chingu/an-introduction-to-environment-variables-and-how-to-use-them-f602f66d15fa) to store sensitive data or data repeatedly used, such as domain names, tokens, or credentials.
- [Request/Response validation](https://medium.com/@theqachronicles/validating-api-responses-8ee9df01ef26) helps ensure every API request and response are following the expected format with expected values.
- See this [Postman documentation](https://blog.postman.com/best-practices-for-api-error-handling/) for implementing comprehensive error handling on server-side.
- You can also use [cURL commands](https://curl.se/docs/tutorial.html) to transfer data with URLs through command line.

## Testing API Endpoints

Testing endpoints allows you to verify that your backend behaves as expected before connecting it to a frontend.

There are multiple ways to test API endpoints.

### Testing GET Requests in the Browser

Web browsers automatically send GET requests, making them useful for quick checks.

Example:
```
http://localhost:8000/api/users
```
If the endpoint works, you should see a JSON response in the browser.

This method is best for:

- Simple GET endpoints
- Quick sanity checks

### Testing GET and POST Requests Using Postman

For more control over requests (especially POST requests), we use Postman.

Postman allows you to:
- Choose the HTTP method
- Set headers
- Send JSON request bodies
- View formatted responses and status codes


## Steps to Install Postman

### Step 1: Download Postman

1. Open your web browser and navigate to the official Postman website: [https://www.postman.com/downloads/](https://www.postman.com/downloads/).
2. Select the latest version that is compatible with your operating system (Windows/macOS) and download. If you're using a Mac or Linux, be sure to download the version that corresponds to your OS: Mac (Intel Chip, Apple Chip) or Linux (x64, arm64).

### Step 2: Install Postman

#### For Windows:

1. Once the download is complete, find the setup file in your downloads folder (typically named `Postman-win64-setup.exe`).
2. Select and run the .exe file to install Postman.

#### For macOS:

1. Open the downloaded `.dmg` file. If your browser downloads the file as a ZIP file, find the file in the Downloads folder, unzip it, and open the Postman file.
2. Drag the Postman app icon into the "Applications" folder.
3. Once copied, go to your Applications folder and double-click the Postman icon to launch the app.
   You can also install Postman using the [Homebrew](https://brew.sh/) package manager:

```
  brew install --cask postman
```

#### Linux:

1. Unpack the downloaded Postman file using the following command:

```
tar zxf linux_64
```

Alternatively, you can install Postman on Linux from the Snap store page or by using the following command:

```
snap install postman
```

### Step 3: Create an Account (Optional but Recommended)

Once Postman is installed:

1. Open the Postman application.
2. You will be prompted to sign in or create a Postman account. You will be led back to the Postman window after signing in.

## Using Postman: Basic Steps

### Step 0: Ensure your backend is running and have a valid API endpoint to test

### Step 1: Launch Postman

After installation, launch Postman. You'll see a workspace where you can start creating requests.

### Step 2: Make Your First API Request

1. Click on the "New" button at the top-left and select **HTTP**.

![Postman1](./assets/week1-apirequests-postman/Postman1.png)

2. In the request window, choose the type of request method (GET, POST, PUT, DELETE) from the dropdown menu (default is GET).
   To send a GET request, enter the URL of the API you want to test in the input field (e.g., `http://localhost:8000/question/getQuestionById/67062b6dd9d59b115c559096?username=user`). Ensure that the params you are passing are correct.

![Postman2](./assets/week1-apirequests-postman/Postman2.png)

To send a POST request you need to enter the URL (e.g., `http://localhost:8000/question/addQuestion`) and include the Body as well.

- Go to the **Body** tab.
- Select **raw**.
- Choose **JSON** as the format.
- Enter the JSON data in this format:

```json
{
  "title": "How do I use Postman?",
  "text": "I am trying to build an API using TypeScript, but I'm unable to test using Postman. How do I do this?",
  "tags": [
    {
      "name": "Postman",
      "description": "API testing tool that allows developers to send HTTP requests."
    }
  ],
  "asked_by": "Pavan Kumar",
  "ask_date_time": "2024-10-08T12:00:00.000Z",
  "answers": [],
  "views": 0,
  "up_votes": [],
  "down_votes": []
}
```

![Postman3](./assets/week1-apirequests-postman/Postman3.png)

3. Click the **Send** button and wait for the response.

### Step 3: View the Response

- After clicking "Send," Postman will display the API response below the request window.
- You will see the **Status Code**, **Response Body**, **Headers**, and **Cookies** (if applicable).

## Setting Up Authentication in Postman

- Go to the Authorization tab in your request
- Select authentication type from dropdown
- Enter credentials
- Postman automatically adds appropriate headers

## Setting up environment Variables in Postman

- Click the gear icon (⚙️) in top right
- Select "Manage Environments"
- Click "Add" to create new environment
- Add variables. For example,

```
Variable: base_url
Initial Value: http://localhost:8000
Current Value: http://localhost:8000

Variable: api_token
Initial Value: your-dev-token
Current Value: your-dev-token
```

Using environment variables:

- In your requests, use double curly braces:

```
URL: {{base_url}}/api/users
Headers: Authorization: Bearer {{api_token}}
```

## Saving API Requests and Using History

One of Postman's key features is the ability to **save API requests** for future use. This can save you time when testing or working on multiple endpoints. Additionally, Postman keeps track of your request history, allowing you to quickly revisit previous requests without re-entering all the details.

To learn more about using Postman's history, visit: [Postman History](https://learning.postman.com/docs/getting-started/basics/navigating-postman/#history).

## Organizing Requests into Collections

Postman also allows you to save and organize requests into **collections**. A collection is essentially a folder where you can store multiple requests, making it easier to manage large projects and share API workflows with your team.

For more information on creating and using collections, refer to the Postman documentation: [Postman Collections](https://learning.postman.com/docs/sending-requests/intro-to-collections/).

These features enhance your ability to efficiently manage, organize, and track your API development process within Postman.

## Recommended Tools

In addition to using the Postman desktop app, you can also integrate Postman with Visual Studio Code through the Postman extension. This extension allows you to send API requests directly from your code editor.

You can find the extension and its documentation here: [Postman VS Code Extension](https://learning.postman.com/docs/getting-started/basics/about-vs-code-extension/).
