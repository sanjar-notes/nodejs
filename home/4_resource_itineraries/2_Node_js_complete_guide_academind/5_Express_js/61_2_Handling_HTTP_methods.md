# 65. HTTP methods
Created Wednesday 22 February 2023 at 11:28 pm

## Situation
Filtering w.r.t HTTP method is a common thing done using an `if` on `req.method`.

## What is app.METHOD
It's conceptually a filter on top of `app.use()`, based on the HTTP method of the request. There are many (as many as HTTP methods). Common ones:
1. `app.get("")`
2. `app.post("")`
3. `app.put("")`
4. `app.delete("")`
5. `app.all("")` - handles all HTTP methods. Generally used for multi-file middleware organization, **but** prefix won't be trimmed off.

Syntax - `app.get`, `app.delete`, `app.post`, `app.all` etc, instead of `app.use`.

- Unlike `app.use()`, passing a path to app.METHOD is necessary (even if it's just `"/"` ). It'll be silently ignored otherwise.
- The match criteria for path specified in app.METHOD is an **exact match**. Of course, a trailing "/" if any is ignored and handled properly.
- Multi-file middleware organization is possible with all these, but prefix will be not be trimmed (it'll be passed to the child *as is*). [Code example](https://github.com/exemplar-codes/express-app-academind/commit/19e738f6969544e358d074d0b56f297b78f993fc)

[Code example](https://github.com/exemplar-codes/express-app-academind/commit/01c10d54a073f86069088751b922d5e8fcc38308)

### Doubts (mental edge cases)
- In case a child middleware file's register (in the parent) was an app.METHOD, the child file's non-method middlewares will still run, since there's no concept of nesting in Express - it's all linear.
- Multiple `app.METHOD` if applicable, will all execute (i.e. there's no auto response/stoppage after executing of any of them). Example - If a `app.get` and an `app.all`, both, are present, and a `GET` request comes up, both will run (assuming there's no response from anyone between them, including the previous one among them). [Code example](https://github.com/exemplar-codes/express-app-academind/commit/bb97487b43fc6b260e72c303c3a0b967a6d10ff3)