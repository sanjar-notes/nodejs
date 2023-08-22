# 312. Express default error handler middleware
Created Wednesday 23 August 2023

## Situation
Suppose an error occurs in a middleware, or we throw one deliberately. Result: the app crashes, unless the error is handled `try catch` in the same middleware.

This is not elegant, since we'll need to duplicate the try catch in all middlewares.


## Solution
Express.js solves this problem for us.
When an unhandled error occurs, Express stops the usual middleware chain and starts executing some special middlewares at the end of the chain.

Of course, we need to add these middleware(s) ourselves. It could just be one also.

Important - this "error" middleware(s) should have 4 params, at-least. 
Otherwise Express will consider the middleware as a usual "request" middleware. Example:

```js
const app = express();

app.use();
// endpooints
// routers


// "error" middleware (4 params), where control reaches in case of unhandled error
app.use((err, req, res, next) => {
	// err is available
	// send a response, do whatever you want
})
```


---
## How to activate error bubbling
These events cause stoppage (of normal middleware flow) and trigger error bubbling:
1. Occurrence of unhandled error
2. Deliberate `throw` (unhandled)
3. Running `next(errorObjectOrVariable)` from inside a middleware.

Of course, these should happen inside a "normal" middleware.


## Error from async code
If the unhandled error occurs (or `throw` was done) in async code (middleware), it will crash the app. 
The only way to trigger error bubbling from an async middleware is to use `next(errorObject)`.

```js
// below, will trigger Express's error bubbling
// OK
app.use((req, res, next) => { throw new Error('...') });

// below, won't trigger Express's error bubbling
// app will crash
app.use(async (req, res, next) => {
	throw new Error('...');
});

// below: fix
app.use(async (req, res, next) => { 
	next(Error('...'));
});
```

Suggestion - just use `next(err)` inside `catch` (async/await) or `.catch` (if using Promises)


## Error middleware chain behavior
Once bubbling starts, all remaining normal middlewares - will be ignored. The bubbling behavior is simple:
- All normal middlewares are ignored
- Only error type middlewares (i.e. 4 params) one will now be run.
- Interleaving - if normal and error middlewares were interleaved, the normal ones will still be ignored.
- If there was no error bubbling, the error middlewares are ignored.
- If an error middleware calls `next(someValue)`, the next error middleware will be called.
	- Doing `next()` (without params) inside an error middleware stops the chain. The app will hang - no response is sent. *Don't do this*.


note: `(new Error('someMessageee')).message` is possible (in case I need to `.send` the message)

[Code (commit)](https://github.com/exemplar-codes/online-shop-nodejs-branches/commit/77ce492c8c822d692c70fb4b57cfeb040a78cc9e)