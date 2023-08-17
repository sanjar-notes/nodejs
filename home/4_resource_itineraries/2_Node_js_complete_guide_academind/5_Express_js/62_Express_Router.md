# 66-68. Express Router
Created Wednesday 22 February 2023 at 08:36 am

## Situation
Multi-file organization + (optional) router prefix trimmed.


## How (to use)
```js
// main.js file
const express = require("express");

const app = express();

const shopRouter = require("./routes/shop"); // file path doesn't matter

// shopRouter is a valid middleware
app.use("/shop", shopRouter); // router route specified here, in parent file

app.use("/", (req, res, next) => {
  console.log("Main middleware ran");
});

app.listen(3000, () => console.log("Server running at port 3000"));
```

```js
// routes/shop.js file
const express = require("express");

const router = express.Router(); // just like an app

router.use((req, res, next) => {
  console.log("Shop middleware ran");
});

// actual request URL is "/shop", but this will match, since prefix is trimmed
router.get("/", (req, res, next) => {
  console.log("Shop GET ran");
});

module.exports = router;
```

[Code example](https://github.com/exemplar-codes/express-app-academind/commit/0b38a374f223ef3c50e44deeee8b008639aa751a)

## Syntax
1. A router is created using `express.Router()` instead of `express()`.
2. The router can register middlewares onto it just like an app.
3. The router is a valid middleware, so it can be exported to and registered normally by the parent.
4. The router path is specified in the parent. This part (prefix) is trimmed, i.e. not accessible to the router. Technically, it is accessible, but the intent is to hide/not-use it.
5. The router should be registered in the parent, preferably using `use('path_here', myRouter)`
   
## Doubts (everything works as expected)
1. Simplest - No path for router specified (i.e. using full path in router too). **Expected**, **OK**
2. Default spec - Router path '/' (i.e. using full path in router too). **Expected**, **OK**
3. Path in parent, no path in router. **OK**. **Prefer** `.use('', myRouter)` only for registering router, since:
	1. Path normalized forwarding is not done if `get`.
	2. `app.route('').use(myRouter)` is just too caveat-ed. Caveats - `app.route()` can only chain an app.METHOD, and since app.METHOD does not trim the route for the router, there's no use of `app.route` for a router (i.e. or in general for any useful multi-file scenario).
4. Path in parent, "/" or some larger path in router. **Expected**. **OK**.

Note:
- Things learnt - app.METHOD always needs the path param, even if it is `'/'`.
- Standard rules apply, unless specified otherwise.
- The router path trimming feature assumes all paths in the router have a common prefix.
- The router can be used without the path trimming feature also (i.e. don't specify a path while registering). This is actually the better way to do multi-file middleware/route organization (instead of using `express()` to make the child - see [code](https://github.com/exemplar-codes/express-app-academind/commit/2be76a9c2fb4c542967cd94e568f40367f17e2d8)).
- Don't *call* the imported router when registering. A middleware is specified using a callback (since `express() or express.Router()` return a callback functions with attached attributes). 
	- This is a common mistake since plugable middlewares *seem to be called* - `app.use(express.json())` or `app.use(express.static())`. These entities need to be called since they're not actually a middleware (callback), but a function that returns a configured middleware (callback), based on the arguments are passed.
	- [Code](https://github.com/unclassified-repos/academind-nodejs-assignment-2/commit/b0cd454943d3681bc5a642778c6109782e6b7877)
	- The error message from Express.js is quite useless, BTW. FIXME: discuss about better error message for this case, on the Express.js project site.