# 64. Conditional middlewares
Created Friday 18 August 2023

## Situation
There is a backend app with many middlewares, including two named X and Y. The requirement is that only X runs or Y runs based on a condition.
&nbsp;

## Solution
How do we handle this?
There are a few cases here, with minor variations.
1. Keep it linear - we add the middlewares one after the other. In the body of these middlewares we `return` early if the condition is not matching.
	- If both are custom middlewares
	```js
	function mwX(req, res, next) {
		if(condition)
			return next();
		// do X mw logic
	}
	
	function mwY(req, res, next) {
		if(condition)
			return next();
		// do Y mw logic
	}

	app.use([mwX, myY]);
	```
	- If any of them is library generated. Or if you don't want to litter conditional code into middlewares.
    ```js
	// of course, this can be done using array too
	function xConditional(req, res, next) {
		if(condition)
			return X;
		return ((req, res, next) => { return next(); });
	}

	function yConditional(req, res, next) {
		if(condition)
			return Y;
		return ((req, res, next) => { return next(); });
	}

	
	app.use([xConditional, yConditional])
	```
2. Ternary - works only if the condition is static (i.e. not dependent on `req` or `res`), we can use the ternary operator. `app.use(condition ? X : Y);`. X and Y could be custom or library generated doesn't matter. Code:
	```js
	app.use(staticCondition ? X : Y);
	```


Note: 
- Prefer differentiation based on route, method and router before doing this. They are in-built control mechanisms which are intuitive and easy to use.
- Can be generalized to more than 2 middlewares too.
- Direct wrapper  (special case) - if the middlewares are exclusively conditional. Code:
	```js
	function wrapperMiddleware() {
	  if(condition) // based on req or res logic or otherwise
	    return X;
	  else
	    return Y;
	}

	app.use(wrapperMiddleware());
	```