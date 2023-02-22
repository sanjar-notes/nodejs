# 60. Adding Middlewares
Created Tuesday 21 February 2023 at 09:15 am

/storymode

## What is a middleware
- The most important (and used) construct in Express.js is middleware. A middleware is just a function.
- Almost everything is a middleware (i.e. some specific implementation of the middleware) in Express.
- A middleware has access to request, respond params. Additionally, it has a "next" param that's used to transfer control to the next middleware.


## Where do middlewares fit-in in Express
![](../../../../assets/Pasted%20image%2020230221091754.png)
- Middlewares are an array of functions that run (linearly, and in top-down file order) between the phase of request and response.
- There's actually no "response" function in Express. Some middleware ends the request-response cycle by responding. 
- If no middleware responds, the connection will not end (most likely time-out). This practically never happens, since an "all accepting" 404 middleware is always present at the end.

## Anatomy of a middleware
1. A middleware has access to request, respond params, in addition to a "next" param that's used to transfer control to the next middleware.
2. If "next" is not called in a middleware, it should either respond or else the connection will be stalled (never finish).
3. Since middlewares are just functions, a lot of useful 3rd party middlewares are available.


## Syntax
1. A middleware is added to the app using `app.use()`. That's it.
```js
const express = require('express');

const app = express();

app.use((req, res, next) => {});
app.use((req, res, next) => {});

app.listen(3000, () => console.log('Server running on port 3000'));
```