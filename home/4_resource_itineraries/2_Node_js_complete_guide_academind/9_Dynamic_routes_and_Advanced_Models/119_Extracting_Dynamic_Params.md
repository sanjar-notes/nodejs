# 119. Extracting Dynamic Params
Created Sunday 19 March 2023 at 09:49 pm

## Route params
- **Capturing** (from the URL) - Express uses colon notation to specify path params. Example:
	```js
	router.get('/product:myProductId', ...)
	```
- **Accessing** (in code) - `req.params` is an object with route params. Key names are the same as those used for capturing.

All params are `String`. **This is important, especially for the bug where === used in code**. Either parse the value properly or use `==` (non-strict equality).


## Query params
- **Capturing** - done by default.
- **Accessing** - `req.query` is an object with query params. Complex queries are properly handled - arrays, objects are created.

I already covered this in [67. Requests - Path](../5_Express_js/67_Requests#2.%20Path)

[Code](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/6a868c7e584162d911a0a6e97a6736bb16ec4915)