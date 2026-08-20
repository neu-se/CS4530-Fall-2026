---
layout: page
title: Guide to API Requests
permalink: /tutorials/week1-apirequests
parent: Tutorials
nav_order: 4
---

# Tutorial: Guide to API Requests

## Contents

- [Introduction to API Requests](#introduction-to-api-requests)
- [Breakdown of an API Request](#breakdown-of-an-api-request)
- [Authentication in APIs](#authentication-in-apis)
- [Testing API Endpoints](#testing-api-endpoints)
- [Recommended Tools](#recommended-tools)

## Introduction to API Requests

**APIs** (Application Programming Interfaces) are essential tools that allow different software applications to communicate with each other. As developers, it's crucial to understand how to interact with APIs, which involves making API requests. API requests are structured interactions where one software sends a request to retrieve or send data to another.

With this guide, you can:

- **Understand the basics** of making GET and POST requests to an API.
- **Test API responses** to ensure that they return the expected results.

### Types of API Requests:

There's a whole [vocabulary of HTTP requests](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods), but GET and POST are the two most important:

- **GET**: Retrieves data from an API. It's commonly used when you want to fetch information without making any changes.
  - _Example_: Use a GET request to retrieve a list of videos related to the one you're currently watching on a streaming platform (e.g., `GET /videos/related`).
- **POST**: Submits new data to an API to create a resource. It's used when you need to send data to the server to create something new.
  - _Example_: Use a POST request to save a newly uploaded video on a platform (e.g., `POST /videos`).

Each of these request types serves a specific purpose in API interactions, and a tools like Postman allows you to easily switch between them to test and build your APIs.

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

## Recommended Tools

**Postman** is a popular API testing tool that allows developers to build, test, and modify APIs quickly and easily. It provides an interface to interact with APIs and simplifies API development. Postman supports making requests like **GET**, **POST**, **PUT**, **DELETE**, and more.

It also allows you to:
- Choose the HTTP method
- Set headers
- Send JSON request bodies
- View formatted responses and status codes

Here is a brief [tutorial on postman](https://neu-se.github.io/CS4530-Spring-2026/tutorials/week1-apirequests-postman) 