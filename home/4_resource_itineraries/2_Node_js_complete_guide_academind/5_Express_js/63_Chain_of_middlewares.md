# 63. Chain of middlewares
Created Friday 18 August 2023

## Situation
Suppose I need to run multiple middlewares for the exact same method, route, router or maybe with `.use()` itself.

Let's try with the `.use()` one, should be simple, I just write them one below the other. 

But what if the number of middlewares are not known, or I'm lazy. Can I use a for loop?
No. Since all `.use(callback)` are callbacks, we never run them until we get a request - so it's *not possible* with a for loop.


## Solution - how
Since looping is not possible.
Express supports comma separated syntax or an array of middlewares passed to `.use` (and other functions).
The syntax is very flexible - everything is linearized.


## Solution - syntax
Here's the syntax:
```js
app.use(myMiddleware); // already familiar


// 1. Comma-separated works fine too (all will be run in order)
app.use(myMiddleware1, myMiddleware2, myMiddleware3);

// 2. Array also works 
app.use([myMiddleware1, myMiddleware2, myMiddleware3]);

// 3. can use both - it still works
app.use(myMiddleware1, [myMiddleware2, myMiddleware3], myMiddleware4);

// 4. btw, nested arrays work too, Express just flattens them
app.use(myMiddleware1, [myMiddleware2, [myMiddleware3]], myMiddleware4);
```

Works with `.router()`, `method('', )` too.


## Doubt (ignorable)
Q: It could work with this notation of comma, or array if we can write a wrapper with a loop?
A: It would work, but not properly or for call cases:
1. For middleware that don't respond. 
	1. It would *seem* to work. Since each middleware in the loop would call `next()`, but the first iteration would end the wrapper (which is a middleware itself). So the others in the loop would run (but not in the queue - they will run independently). **Doesn't work**
2. If they respond - won't work. 
	- If the first one is a non-responding middleware, point 1 happens (out of order exec) - not acceptable.
	- If we ignore out of order/independent execution. Let's see what happens, the responding middleware runs... fine, no. When the next middleware (be it responding or non-responding), we would get headers set error - since it would reach the 404.

I know, we can update `res.locals` and catch that in 404, but the out of exec order is till not solved.

Conclusion: Construct of arrays/comma separated middleware is a REQUIRED feature.