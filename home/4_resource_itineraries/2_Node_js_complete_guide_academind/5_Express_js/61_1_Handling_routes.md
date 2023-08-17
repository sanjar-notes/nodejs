# 61. Handling routes
Created Tuesday 21 February 2023 at 09:48 am

## Situation
The simplest and naive way to do routing is based on `req.url` and running `next()` (with `return`) conditionally to ignore the current middleware.

Express.js has an easy way to get around this.


## How
The `app.use()` function already provides an easy way to do this. The function actually has 5 forms. It accepts a path (string) as first argument that decides if the middleware will be run or ignored (think auto `next()`).

```js
const express = require('express');

const app = express();

app.use('/shop', (req, res, next) => {});
app.use('/user', (req, res, next) => {});

app.listen(3000, () => console.log('Server running on port 3000'));
```

The **match criteria** for the path is "starts with", and not an exact match. This means:
1. `/` will match all routes. `/` is actually the default value for the path param in `.use()`.
2. Order of middlewares is important for correct routing.
```js
const express = require('express');

const app = express();

// correct order, if one wants to respond directly if '/user'
app.use('/user', (req, res, next) => {});
app.use('/', (req, res, next) => {});

// wrong order, for the goal stated above
app.use('/', (req, res, next) => {}); // will be run
app.use('/user', (req, res, next) => {}); // will be run if `/` has next()


app.listen(3000, () => console.log('Server running on port 3000'));
```

Note: 
- Other than auto-next(), the usual rules apply.
- Path (i.e. first argument for middleware register) [can](https://expressjs.com/en/api.html#path-examples) be an `Array` of `string`s too, instead of just a single `string`, match criteria remains the same. e.g `app.use(['/order', '/api/order'], () => {})` is fine.