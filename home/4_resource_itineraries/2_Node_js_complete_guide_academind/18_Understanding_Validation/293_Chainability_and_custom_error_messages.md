# 293. Chainability and custom error messages
Created Sunday 20 August 2023

## Multiple validators (chaining)
The `check` (accumulator) can accept more than one validatior at a time, via chaining.
```js
check("adhocEmail").isEmail().isLength({ min: 5 })
```

```js
// usage example
router.post("/edit-product/some-path",
			
  check("adhocEmail")
    .isEmail()
    .isLength({ min: 5 }),

  adminController.postEditProduct
);
```
Example - `.isEmail()` or something built in again.


## Custom error messages
The custom error message is bland - 'Invalid value'. For passing custom error messages, use the `withMessage()` function chained to a validator, like so:
```js
check("adhocEmail").isEmail().withMessage("this ain't an email...")
```

```js
// usage example
router.post("/edit-product/some-path",
			
  check("adhocEmail")
    .isEmail()
    .withMessage("this ain't an email..."),

  adminController.postEditProduct
);
```


## Note
- A chain of validators (chained to `check`) will still generate a single middleware.
- Multiple chained validators could have a single `withMessage`. Example:
	```js
	// usage example
	router.post("/edit-product/some-path",
				
	  check("adhocEmail")
	    .isEmail()
	    .isLength({ min: 5 }),
	    .withMessage("invalid email or too short"),
	
	  adminController.postEditProduct
	);
	```
- If multiple chained validator fail (i.e. value is invalid), `express-validator` will still successfully accumulate the errors and let the remaining middlewares run. It does not crash the app.
- Of course `check().check()` *doesn't make sense*, and won't work since `check` just plucks a path and accumulates errors if any.
- If both `throw` (or return falsy) and `withMessage` are used, `withMessage`'s message will override the throw Error's message.