# 301. Santitization
Created Tuesday 22 August 2023

## Two kinds of sanitizations
This is simply the process of trimming the data to match it to our backend/system requirements. There are two aspects here:
1. Security sanitization - this refers to escaping of user given text, like SQL or HTML, which could open our app to vulnerabilities like SQLi/XSS.
2. Normal santization - stuff like normalizing emails, trimming spaces at the ends, etc.


## How `express-validators` helps
The library, in addition to validation constructs, also provided sanitization functions.

- Operation - Doing *will* mutate the req object parts (of course, only the ones that are specified). Again, there will be information loss, since "express-validator" directly mutates the `req` (of Express).
	- This means custom middlewares ahead (written by us), will also get sanitized values.
- Usage - to use, just chain it to the `check` (or other accumulator), like validators are chained.
	- There's no need to use `validationResult` (collector), to get the sanitized value, since the Express `req` was mutated directly.

Example:
```js
  check("adhocEmail")
    .isEmail()
    .normalizeEmail(),

(req, res, next) => { req.body.x }; // will be sanitized.
```

## Some sanitizers
- `.trim()`
- `.normalizeEmail()`
- `escape()` - replaces symbols in HTML (like `<`, `>`) with their HTML entity codes
- ``


## More
The library has security based sanitizers too, check the [docs](https://express-validator.github.io/docs/guides/validation-chain/#standard-validatorssanitizers). 
This article is also very good - [Flavio Copes - Sanitizing input in Express using express-validator
](https://flaviocopes.com/express-sanitize-input/)