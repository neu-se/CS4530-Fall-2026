---
layout: page
title: Messing With APIs
nav_exclude: true
---

## Activity 3.1: Messing with APIs

When you navigate to [this URL](https://name-seeing-server.onrender.com/) your browser makes an HTTP GET request that will get a JSON response.

That URL also accepts HTTP POST requests containing JSON data. The server at that URL also doesn’t correctly validate its input. Because you can [see the source code for this server](https://github.com/neu-se/name-seeing-server/blob/main/server.ts), the app is very easy to "attack."

In this activity, you will understanding the server by reading the woefully uncommented code and interacting with it with HTTP requests. One way to do this is with [Postman]({{site.baseurl}}{% link tutorials/week1-api-requests-postman.md %}), but you can also just write cURL commands if you want. You’ll also try your hand at using [Zod](https://zod.dev/api?id=objects) to describe the desired shape of input. Unlike TypeScript types, Zod validators can actually check whether inputs have the right shape.

You’ll hand in your assignment as a single TypeScript file `handin.ts` as required by your instructor. The template is [here](https://github.com/neu-se/name-seeing-server/blob/main/handin.ts). If you go to <https://github.com/neu-se/name-seeing-server>, find the green "Use this template" button, and select "Open in a codespace," you can edit the `handin.ts` in your browser.

### Grading Criteria: 10pts

- Task 1 cURL commands (5 points)
- Task 2, 2 points
- Tasks 3, 4, and 5: 1 point each.
