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

app.use((req, res, next) => {
    console.log("1 ran");
    next();
  });

app.use((req, res, next) => {
	console.log("2 ran");
});

app.use((req, res, next) => {
	console.log("3 did not run");
});

app.listen(3000, () => console.log('Server running on port 3000'));
```


## My understanding of middleware (not in course)
### Mechanics of middlewares
1. All top-level express code are middlewares.
2. Middlewares don't have nesting. Router may look like nesting, but they're actually a syntactic sugar for linearity. There's no possibility of branching.
3. Middle-wares are evaluated top-down.
4. A middleware runs only if it's the first one in the app or if the one before it executed `next()`.
5. Middlewares can consume other middlewares to give a new middleware. This can be used for non-route organization into files.
6. If a middleware does not call `next`, it has to send a response

### Types of constructs in Express
Structuring/organizing/classification of middlewares:
1. Simplest - seen above
2. Multi-file
3. Route based
4. HTTP verb based
5. Router
![](../../../../assets/express-middlewares.drawio.svg)