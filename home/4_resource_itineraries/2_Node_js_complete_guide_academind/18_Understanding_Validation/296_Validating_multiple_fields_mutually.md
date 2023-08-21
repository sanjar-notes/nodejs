# 296.  Validating multiple fields mutually
Created Tuesday 22 August 2023

## Situation
Suppose the body has `email`, `password`, and `confirmPassword`. And we wish to check if `password` and `confirmPassword` are equal or not.

There's no other way - we have to use a `custom` validator.

Generally, passwords have a general validation too (length, strength etc). Since we're checking for equality, using the validator on any of `password` or `confirmPassword` will work. Code:
```js
check('password')
.custom((value, { req }) => {
	if(value === req.body.confirmPassword) return true;

	throw new Error("passowrds don't match");
})
.someOtherValidator();
```

Note: even if both validators fail, `express-validator` will accumulate the error successfully, instead of crashing the app.