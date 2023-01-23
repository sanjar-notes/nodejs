# 13. Module caching
Created Tuesday 24 January 2023 at 01:37 am

## Situation
Running `require()` multiple times seems to have no effect.
Consider two files, apple.js:
```js
console.log("Running apple.js");
```
and `index.js`:
```js
require('./apple.js'); // prints 'Running apple.js'
require('./apple.js'); // prints nothing
```

In case of exports, e.g. mango.js
```js
const myMango = { country: "India" };
console.log('Running myMango.js')
module.export = myMango;
```
and index.js:
```js
const mango1 = require('./myMango.js'); // console.log happens
mango1.country = "Egypt";

const mango2 = require('./myMango.js'); // console.log DOES NOT occur
console.log(mango2); // prints "Egypt" instead of "India"
```



## Module caching
Default Node.js behavior is that when the file is first imported, Node.js caches (in RAM not disk) anything it exports (which could be nothing). All other imports for the said file are returned from cached value - i.e. `require()` just returns the cached value (without running the file again, of course).

One can use `require` multiple times for a path, that's not a problem - but it'll always return the saved value.

Note: the cached value is not serialized or anything (like deep cloning, removing references etc) - i.e. if multiple files import a variable the same module, they're actually working with the same physical variable.


## Actionable advice (my guess)
So, as to avoid this "module caching" pitfall:
1. Don't "write" to imported variables. Keep them read only, as much as possible.
2. Try to minimize direct closures in exported code.
3. Export classes and functions instead of objects (containing data) directly, as much as possible.

These things don't have to be thought of very much. Practically, following simple programming best-practices covers these things.