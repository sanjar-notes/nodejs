## 316. Unhandled async errors (missing await)
Created Monday 28 August 2023

[dev.to article](https://dev.to/sanjarcode/catch-async-middleware-errors-in-express-v4-53f7)
## Context
I am working on a plain JS Express.js app. It has middlewares, a few routers.

&nbsp;

## Situation - strange error
I was getting an error from Mongoose package. The error would crash the app, in spite of having an error sink - which would never get triggered (unexpected).

I am trying to use the `.save()` mongoose function, an async function, without `await`. But there's a reason I do this - I wish to send the response before the call succeeds.

Exact problem (comparison):
```js
// error
app.get('/xyz', async (req, res, next) => {

  try {
	// some code here
	product.save(); // this _will_ throw an error (expected, ok)
  } 
  catch (e) {
	next(e);
  }

  console.log('Everything is fine.'); // runs (unexpected)
  
});

app.use((err, req, res, next) => {})

// error middleware doesn't run (app crashes)
```

```js
app.get('/xyz', async (req, res, next) => {

  try {
	// some code here
	await product.save(); // this _will_ throw an error (expected, ok)
  } 
  catch (e) {
	next(e);
  }

  console.log('Everything is fine.'); // doesn't run now, as expected
  
});

app.use((err, req, res, next) => {})

// error middleware runs (app doesn't crash)
```

&nbsp;

## Fix (here)
I needed to add `await`.

&nbsp;
## Explanation
Since I did not wait for `product.save()` (which is async - so error is thrown after some time), to express, the error never occurred.

So, it never ran the code inside `catch`. 

And therefore, the error middleware never ran.

But the `product.save()` does throw an error, and it does bubble up at the runtime level (Node.js process instead of within Express), crashing the app.

&nbsp;

## Hack - catch error at a lower level (runtime instead of Express)
The following is a native way to catch errors. Add the following as the first middleware:
```js
app.use((req, res, next) => {
  process.on("unhandledRejection", function (reason, p) {
    console.log("hack, Unhandled Rejection at: Promise ", p, " reason: ", reason);
    // application specific logging, throwing an error, or other logic here
  });
})
```
Source: https://stackoverflow.com/a/30650609/11392807

Here:
- Crash is prevented - since this will catch the unhandled error, prevent bubbling to the runtime level, so the crash will be prevented.
- The error middleware is still not called.
- Unfortunately, you can't respond (`res.send`/`res.json`/`res.render`, since this execution is happening outside the middleware chain: we don't have access to `res`.

Why would you I use this? If the app is old, there may be a lot of such "non-awaited" middlewares.

&nbsp;

## Actual fixes
1. Use `await`.
2. For non awaited parts, use `.then` and call `next(e)` from `.catch`. Example: If the user doesn't care about the result immediately.

&nbsp;

## Conclusion
If async middlewares (Express.js) contain code that doesn't use await. 
Then execution of such code starts happening outside the middleware chain.
This leads to problems like failed triggering of error middlewares, app crashes, and inability to send a response.