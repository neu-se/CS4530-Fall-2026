---
layout: page
title: Socket.IO Tutorial
permalink: /tutorials/week2-socketio-basics
parent: Tutorials
nav_order: 5
---

This tutorial covers the basic concepts of Socket.IO. By the end, you'll understand when sockets are useful, and how to emit and listen for events for real‑time updates.

## Contents
- [What is Socket.IO](#what-is-socketio)
  - [What problem does Socket.IO solve?](#what-problem-does-socketio-solve)
  - [How Does It Work?](#how-does-it-work)
  - [Socket.IO vs. REST APIs](#socketio-vs-rest-apis)
  - [Example Uses](#example-uses)
- [Using Socket.IO](#using-socketio)
  - [Starter Files (Express 5 + TS ESM)](#starter-files-express-5--ts-esm)
  - [Setting Up a New Project](#setting-up-a-new-project)
  - [Emitting & Receiving Socket Events](#emitting-and-receiving-socket-events)
  - [Putting It All Together](#putting-it-all-together)
  - [Troubleshooting](#troubleshooting)
- [Useful Resources](#useful-resources)

# What is Socket.IO?
Socket.IO is a library that enables real‑time, bidirectional, persistent communication between client(s) and server(s). **Bidirectional** means both the client and server can send messages at any time. These features make Socket.IO ideal for live dashboards, chats, multiplayer games, and collaborative tools.

## What problem does Socket.IO solve?

With normal HTTP, communication is request–response. The client asks the server for data, the server responds, and the connection closes. If something changes on the server, the client won’t know unless it asks again.
Socket.IO keeps a persistent connection open between the client and the server. This lets the server push updates to the client the moment something changes, without waiting for a new request.
This is what makes real-time features possible, like live chat messages, shared cursors in a collaborative editor, multiplayer game updates, or dashboards that update instantly when new data arrives.

## How Does It Work?
Socket.IO uses a listener-based event model.

When you call `.on(...)`, you are **registering a listener** for a specific event. That listener will run every time the event occurs.

When you call `.emit(...)`, you are **sending an event** with some data. Any listeners registered for that event will be notified and receive the data.

In practice, this means:
- `.on(event, handler)` sets up code that waits for something to happen
- `.emit(event, data)` triggers that event and passes data to all listeners

Under the hood, Socket.IO uses [WebSockets](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API) (with fallbacks) to maintain a persistent connection.
If this feels familiar, it’s because Socket.IO follows the same idea as the observer/listener pattern, which we’ll revisit later in the course.

## Socket.IO vs. REST APIs

| Feature            | Socket.IO                               | REST API                              |
| ------------------ | --------------------------------------- | ------------------------------------- |
| **Design Pattern** | Bidirectional, Publisher–Subscriber     | Request–Response, client‑initiated    |
| **Connection**     | Persistent (WebSocket or fallback)      | Per‑request (HTTP)                    |
| **Use Cases**      | Real‑time, low‑latency updates          | CRUD, on‑demand data fetch            |
| **Data Flow**      | Either side can send anytime            | Client pulls; server responds         |
| **Statefulness**   | Often stateful                          | Stateless                             |

## Example Uses:

Socket.IO is great for any use case where real-time updates are essential, or when the client and server need continuous communication. A few examples are:

1. **Chat Room** – This is a simple use case outlined in the documentation (linked [below](#useful-resources)). Users need to send and receive messages in real time, instantly. With Socket.IO, the user can emit a message to the server, which then broadcasts it to the other connected users. If you were to use a REST API here, there would be a lot of overhead and latency in sending/receiving messages due to the need for constant requests to the API.

2. **Multiplayer Games** – Real-time game state sharing with low latency is essential for smooth multiplayer gameplay. By emitting socket events with the updated game state, you can ensure that all connected player clients have the same synchronized copy of the game state to display.

3. **Collaborative Tools** – For applications like collaborative text editors or whiteboards, sockets can help keep the state synchronized across clients. When a user makes a change, the change will be emitted to the server, which may internally update the "source of truth" (i.e. the most reliable, accurate, and centralized location for critical data) for the application. Then, the updated state would be emitted to all other connected clients, so that everyone sees the edits in real time.

### Client vs Server: who does what?

In a Socket.IO application, the client and server have different responsibilities.

- The **client** emits events when a user does something, such as clicking a button, submitting a form, or typing a message.
- The **server** listens for those events, decides what should happen next, and chooses what information to send back and to which clients.

For example, in a chat app:
- The client emits a `chat message` event when a user sends a message
- The server receives it and broadcasts the message to other connected clients

Keeping this separation clear will matter more as we introduce rooms, namespaces, and multiple connected users.

# Using Socket.IO

## Starter Files (Express 5 + TS ESM)
> **Why this section?** The previous tutorial let learners install packages ad‑hoc, which pulled the latest Express (v5) but showed code written for older setups. To avoid version mismatches, start from the following files and then run `npm install`.

Create the four files below in your project root:

### `index.html`
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Socket.IO Tutorial</title>
    <script src="/socket.io/socket.io.js"></script>
  </head>
  <body>
    <h1>Hello Socket.IO!</h1>
    <script>
      const socket = io();
      socket.on("connect", () => console.log("Connected to the server"));
      socket.on("disconnect", () => console.log("Disconnected from the server"));
    </script>
  </body>
</html>
```

### `package.json`
```json
{
  "name": "socketio-tutorial",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "type": "module",
  "scripts": {
    "dev": "ts-node --esm server.ts"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "express": "^5.1.0",
    "socket.io": "^4.8.1"
  },
  "devDependencies": {
    "@types/express": "^5.0.3",
    "@types/node": "^22.5.0",
    "@types/socket.io": "^3.0.1",
    "ts-node": "^10.9.2",
    "typescript": "^5.9.2"
  }
}
```

> Notes:
> - We keep **Express 5** and **Socket.IO 4** pinned here.
> - We run in **ESM** mode and use `ts-node --esm` for development.

### `tsconfig.json`
```json
{
  "compilerOptions": {
    "target": "es2022",
    "module": "nodenext",
    "moduleResolution": "nodenext",
    "lib": ["es2022"],
    "types": ["node"],

    "strict": true,
    "skipLibCheck": true,
    "esModuleInterop": true,
    "forceConsistentCasingInFileNames": true
  },
  "include": ["./**/*.ts"],
  "exclude": ["node_modules"]
}
```

### `server.ts`
> **Important:** In ESM, `__dirname` is not defined. Use `import.meta.url` to derive it.

```ts
import express from "express";
import type { Request, Response } from "express";
import http from "http";
import { Server } from "socket.io";
import type { Socket } from "socket.io";
import { fileURLToPath } from "url";
import { dirname, join } from "path";

const __filename = fileURLToPath(import.meta.url);
const __dirname = dirname(__filename);

const app = express();
const server = http.createServer(app);
const io = new Server(server);

app.get("/", (req: Request, res: Response) => {
  res.sendFile(join(__dirname, "index.html"));
});

io.on("connection", (socket: Socket) => {
  console.log("A user connected");
  socket.on("disconnect", () => {
    console.log("A user disconnected");
  });
});

const PORT = 3000;
server.listen(PORT, () => {
  console.log(`Server is running on http://localhost:${PORT}`);
});
```

## Setting Up a New Project
1. **Create a project and add the files**
   ```bash
   mkdir socketio-tutorial && cd socketio-tutorial
   # Create index.html, package.json, tsconfig.json, server.ts exactly as above
   ```
2. **Install packages**
   ```bash
   npm install
   ```
3. **Run the dev server**
   ```bash
   npm run dev
   ```
4. Open `http://localhost:3000` to see a page with a 'Hello Socket.IO!' message. You can check your terminal for the connection logs. Opening and closing the tab/browser will show connection and disconnection logs respectively.

## Emitting and Receiving Socket Events

### 1) Creating sockets on client and server
**Client (in `index.html`):**
```html
<script>
  const socket = io();
  socket.on("connect", () => console.log("Connected"));
</script>
```
**Server (in `server.ts`):**
```ts
io.on("connection", (socket) => {
  console.log("A user connected");
});
```

### 2) Emitting a custom event
**Client → Server:**
```html
<script>
  // Send a chat message
  socket.emit("chat message", { user: "John", message: "Hello, World!" });
</script>
```
**Server listens:**
```ts
io.on("connection", (socket) => {
  socket.on("chat message", (data: { user: string; message: string }) => {
    console.log(`${data.user}: ${data.message}`);
  });
});
```

### 3) Broadcasting to all clients
**Server → All clients:**
```ts
io.emit("chat message", { user: "Server", message: "Welcome to the chat!" });
```
**Client listens:**
```html
<script>
  socket.on("chat message", (data) => {
    console.log(`${data.user}: ${data.message}`);
  });
</script>
```

## Putting It All Together
**Server (`server.ts`):**
```ts
io.on("connection", (socket) => {
  console.log("A user connected");

  socket.on("chat message", (data: { user: string; message: string }) => {
    // Re-broadcast to everyone
    io.emit("chat message", data);
  });

  socket.on("disconnect", () => {
    console.log("A user disconnected");
  });
});
```

**Client (`index.html`):**
```html
<script>
  const socket = io();

  socket.on("chat message", (data) => {
    console.log(`${data.user}: ${data.message}`);
  });

  // Example: immediately emit something
  socket.emit("chat message", { user: "John", message: "Hello, World!" });
</script>
```
## Common Mistakes

- **Static files not being served**  
  Make sure your Express server is serving `index.html`. If the browser loads but the socket never connects, this is often the issue.

- **Mismatched Socket.IO versions**  
  The Socket.IO client and server must use compatible versions. Always install dependencies using the provided `package.json`.

- **Using `io.emit` vs `socket.emit` incorrectly**  
  - `socket.emit(...)` sends a message to a single connected client  
  - `io.emit(...)` broadcasts a message to all connected clients

## Troubleshooting
- **`ReferenceError: __dirname is not defined`** — You’re in ESM. Use the `fileURLToPath(import.meta.url)` pattern shown above.
- **Type errors for Node globals** — Install `@types/node` (already listed) and ensure `"types": ["node"]` is set in `tsconfig.json`.
- **Wrong Express/Socket.IO versions** — Don’t install ad‑hoc. Use the provided `package.json` and run `npm install` so versions match this tutorial.

# Useful Resources
- [Socket.IO Introduction (Documentation)](https://socket.io/docs/)
- [Socket.IO Chat App Tutorial (Documentation)](https://socket.io/docs/v4/tutorial/introduction)
- [Learn Socket.io In 30 Minutes – Web Dev Simplified](https://www.youtube.com/watch?v=ZKEqqIO7n-k)
- [How to test Socket.io](https://socket.io/docs/v3/testing/)