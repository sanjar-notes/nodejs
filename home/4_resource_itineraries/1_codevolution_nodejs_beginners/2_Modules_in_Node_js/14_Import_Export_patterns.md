# 14. Import/Export patterns
Created Tuesday 24 January 2023 at 02:05 am

*Everything except the last point here is already known/obvious to me*.

These are some common patterns that are used in projects.
1. Exporting a single thing (already using)
```js
// add.js
const add = (a, b) => a + b;
module.exports = add;

// index.js
const add = require('./add'); // imported code name can be anything
```
2. Direct export of single thing. Makes sense - CommonJS is only concerns with objects (`module.exports`) and functions (`require`)
```js
// add.js
// const add = (a, b) => a + b;
module.exports = (a, b) => a + b; // export directly


// index.js
const add = require('./add'); // no change in import
```
3. Export multiple things - assign an object containing stuff to `module.exports`. Or point to an array (not preferred but works).
```js
// math.js
const add = (a, b) => a + b;
const subtract = (a, b) => a - b;

module.exports = {
  add: add,
  subtract: subtract
}

// OR equivalently. Since identifier and key name is the same
module.exports = { add, subtract };


// index.js
const math = require('./math');

const add = math.add;
const subtract = math.subtract;

// OR, use destructuring
const { add, math } = require('./math');
```
4. Directly attach stuff to be exported to the `module.exports` via a key.
```js
// math.js
const add = (a, b) => a + b;
const subtract = (a, b) => a - b;

module.exports.add = add;
module.exports.subtract = subtract;


// index.js - no change in import
```
5. Use `exports` instead of `module` (`.exports`) to export stuff. This is *discouraged*, let's see why in the next video. It's better to use `module.exports`.
```js
// add.js
const add = (a, b) => a + b;
exports = add;

// index.js - no change here
const add = require('./add');
```