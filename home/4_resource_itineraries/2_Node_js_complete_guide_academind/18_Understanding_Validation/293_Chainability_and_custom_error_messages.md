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