# 292. `express-validator` package and two-piece architecture
Created Tuesday 15 August 2023

## About the package
- We are going to use a npm package called "express-validator" for adding validations to our online store app. [npm link](https://www.npmjs.com/package/express-validator). [Docs](https://express-validator.github.io/docs)
- The package provides some basic constructs and in-build validators. We can also add our own custom validators too.
- It **internally** uses "validator" package (aka validator.js). [npm link](https://www.npmjs.com/package/validator)

For in-built validators, we will most be refering to validatorJS package docs, https://www.npmjs.com/package/validator


## Installing
```sh
npm install express-validator
```

That's it.

---

## Two piece behavior of express validator
The package exposes two (kinds) of functions:
1. `check`
2. `validatationResult`

What it wants to us do is simple:
1. Use the `check('')` as a middleware somewhere before final middlewares. 
	- why: `check` generates middlewares which do the validation, and accumulate the error (s), we just need to generate check middlewares and add them correctly (express supports comma separated middlewares, so this is very easy). 
	- Syntax: `check('email').isEmail()` generates a middleware. 
	- void nature - We can think of these generated middlewares as `void` middlewares - they just mutate (accumulate) errors in the `req` object. They don't stop the request handling, just accumulate.
2. Now, in later middlewares, we can call `validatonResult`, this is done in custom middlewares only (since they are concerned with responses). 
	- Syntax: `validatonResult(req)`
	- It returns an object, which has a `.array()` function, with length being equal to number of checks that failed on the way to current middleware. Code: `validationResult(req).array()`
	- Each element of this array has `{param, value, error, message}`.
	- `param` is the key passed in `check`.
	- The package does provide default `messages` for in-built validators.

Note: 
- Look at specific part of request - Just like `check`, the package exposes methods like `body`, `param`, `query`, `cookie`, `header` etc to decrease the check area (make validation precise). Rest is the same - provide a key.
- Validators - I know, the validators  like `isEmail()` are the 3rd of functions here. Btw, some of these do take arguments - usually an argument that configures them, example - `isLength({min:5})`


## Why the two piece approach is good
I like this approach, since:
1. If it was one function, we'd have to move the response code inside the check call somehow - breaking DRY and locality of behavior.
2. Since they are void - they can be ignored for the success case.
3. Since they are 'accumulative', we can get all errors instead of of just the first one - which would make for a less helpful error message.