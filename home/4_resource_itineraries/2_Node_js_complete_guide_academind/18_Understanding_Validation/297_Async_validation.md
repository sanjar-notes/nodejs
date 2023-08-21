# 297. Async validation
Created Tuesday 22 August 2023


## Situation
Suppose a sign up request comes up, and it has 'username' and other things. We wish to check if the `username` is taken (already exists in our database) or not.

This validation isn't synchronous code - since DB calls are async.

How can we do this kind of validation using `express-validator`?


## Solution
Just create a custom validator, but the callback will be an `async` function.
This is supported by `express-validator` by default. Code:
```js
check('username')
.custom(async (value, { req }) => {
	const doesUserNameExists = await someDbCall(value);

	if(doesUserNameExists) throw new Error('username already exists');

	// else (do nothing)
})
```
There's a catch here, unlike the synchronous (where we must return `true` to signal validation is OK) - here we don't need to return anything. Throw an error if validaton is not OK, otherwise do nothing.

Note:
- If `async/await` syntax is not used, just return the promise. Signals are the same:
	- If OK - do nothing
	- If not OK - throw an error, or return `Promise.reject('error message')` from the last call.