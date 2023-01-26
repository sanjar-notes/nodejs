# 15. `module.exports` vs `exports`
Created Thursday 26 January 2023 at 05:25 pm

Q:We another way to export stuff - using `exports` instead of `module.exports`.
But `module.exports` is the recommended approach. Why?
A: It's actually simple. There are two parts to it:
1. `require()` returns `module.exports`, and not `exports`.
2. `exports` is a reference to `module.exports`
<details><summary>Long explanation in words</summary>At the "top-level" (above the module, i.e. IFFE generator) `module` is an object with an attribute `exports` initialized to an empty object. On the same level as `module`, `exports` is a *variable* that references `module.exports`. **So**, mutations (i.e. adding/removing attributes) on `exports` are propagated/apply to `module.exports`, but reassigning `exports` removes the connection (no change happens `module.exports`).</details>

It's easier to understand via code.
First: `module` and `exports` are initialized before passing to the IFFE, like so (my guess):
```js
const module = {
	exports: {},
	... other_irrevelant_things
};

let exports = module.exports;
```
Now, inside an app file:
```js
// mutating attributes is fine
exports.add = ...; // `module.exports` and `exports` are in sync

// assigment does't work
exports = ...; // default export
exports = {
	add: ...   // named export
}
// reason: `module.exports` and `exports` refer to different objects
```
Here, `exports` does have all there is to export. But it is not what the `require()` returns, `require()` returns `module.exports`. Which, in this case hasn't changed.

## Simple solution
`module.exports` has no such caveats:
```js
module.exports.add = ...;      // works
module.exports = ...;          // works
module.exports = { add: ... }; // works
```


## Conclusion
Avoid `exports` because it requires "thinking".
Use `module.exports` always.