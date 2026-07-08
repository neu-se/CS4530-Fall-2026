---
layout: page
title: Simple Storage with Keyv
permalink: /tutorials/week2-keyv
parent: Tutorials
nav_order: 8
---

# Incredibly Simple Storage with Keyv

Most web applications need some kind of database to serve as a repository of user data: examples include game state, forum messages, user profile information.

In very simple web applications, much or all of the user data can be represented as _key-value maps_, which support a couple of operations:

- associating new values with keys
- updating the value associated with a key
- retrieving the value associated with a key

For example, an application might give each user a username, and always have a key-value mapping from a key — the username — to a value — a record storing relevant information about that user.

```ts
interface UserRecord {
  displayName: string;
  profile: string | null;
}
```

In JavaScript, the simplest way to store a key-value map is with a JavaScript object.

```ts
type UserHashtable = { [key: string]: UserRecord };

const users: UserHashtable = {};
console.log(users["alice"]); // undefined
users["alice"] = { displayName: "Alice the Okay", profile: "New here" };
users["bob"] = { displayName: "Bobbo", profile: null };

users["alice"] = { ...users["alice"], displayName: "Alice the Great" };
users["bob"] = { ...users["bob"], profile: "Not here to make friends"};

console.log(users["alice"].displayName); // 'Alice the Great'
console.log(users["bob"].displayName); // 'Bobbo'
```

In the mid-2010s, JavaScript introduced a Map type which provided a slightly different way to do the same thing. (MDN talks about the difference between Object and Map [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map#objects_vs._maps), but notes that both work as key-value maps.)

```ts
const users = new Map<string, UserRecord>();
console.log(users.get("alice")); // undefined
users.set("alice", { displayName: "Alice the Okay", profile: "New here" });
users.set("bob", { displayName: "Bobbo", profile: null });

users.set("alice", { ...users.get("alice")!, displayName: "Alice the Great" });
users.set("bob", { ...users.get("bob")!, profile: "Not here to make friends" });

console.log(users.get("alice")!.displayName); // 'Alice the Great'
console.log(users.get("bob")!.displayName); // 'Bobbo'
```

What JavaScript Objects and Maps do not do is make sure that key-value data is stored in the hard drive, rather than memory. If all you need your database to do is store key-value mappings, but you might want your data to survive when your computer reboots, the [Keyv](https://keyv.org/docs/) library can be a terrific option.

## Keyv basics

Keyv, when used in its most basic form, works exactly like a built-in JavaScript `Map` except that all its methods are `async`.

```ts
import { Keyv } from "keyv";

const users = new Keyv<UserRecord>();
console.log(await users.get("alice")); // undefined
await users.set("alice", { displayName: "Alice the Okay", profile: "New here" });
await users.set("bob", { displayName: "Bobbo", profile: null });

await users.set("alice", {
  ...(await users.get("alice"))!,
  displayName: "Alice the Great",
});
await users.set("bob", {
  ...(await users.get("bob"))!,
  profile: "Not here to make friends",
});

console.log((await users.get("alice"))!.displayName); // 'Alice the Great'
console.log((await users.get("bob"))!.displayName); // 'Bobbo'
```

On its own, this is just a more-inconvenient version of JavaScript `Maps`. Where `Keyv` is more useful is when a storage adapter is used.

## Keyv Storage Adapters

If you have almost any kind of database, then there's a way to use Keyv on top of that database with a storage adapter. A local MongoDB database can be used with the `@keyv/mongo` adapter.

```ts
import { Keyv } from "keyv";
import { KeyvMongo } from "@keyv/mongo";

const users = new Keyv<UserRecord>(new KeyvMongo("mongodb://localhost:27017"));
console.log(await users.get("alice")); // undefined OR { displayName: 'Alice the Great', profile: "New here" }
await users.set("alice", { displayName: "Alice the Okay", profile: "New here" });
await users.set("bob", { displayName: "Bobbo", profile: null });

await users.set("alice", {
  ...(await users.get("alice"))!,
  displayName: "Alice the Great",
});
await users.set("bob", {
  ...(await users.get("bob"))!,
  profile: "Not here to make friends",
});

console.log((await users.get("alice"))!.displayName); // 'Alice the Great'
console.log((await users.get("bob"))!.displayName); // 'Bobbo'
```

This example looks almost the same aside from the adapter, but it behaves differently in an important way: key-value mappings aren't cleared when the program restarts. After the first time this code is run, subsequent runs of the program will show the last stored record for Alice when `users.get('alice')` is called.

## When Keyv is not enough

Keyv is small: it only helps you build key-value stores.
There are a bunch of reasons why key-value stores aren't the only tool people use for building real websites.

Using Keyv as the only repository of your information means you can't easily get access to any of the following:

- Text search, which would let you look up all the times "Nim" was mentioned in the forum
- Efficient retrieval of your ten most recently created users, games, or forum posts
- Atomic database transactions, which could avoid race conditions where two users try to send a chat message simultaneously, but only one gets stored in the permanent log

Almost any "real" database system (MongoDB, PostgreSQL, MySQL, SQLite) will make it straightforward to support these kinds of actions, and you may want to switch to a more complicated repository layer depending on your course project goals.
