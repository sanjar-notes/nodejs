# 16. ES modules
Created Thursday 26 January 2023 at 07:35 pm

## CommonJS
We've learnt about CommonJS module standard, where each file is isolated by default. We share code using `module.exports` and the `require` function.

CommonJS works fine and is easy.


## ESM
"ES modules" is a new (since 2015) module system for JavaScript. 

**Question, why do we need another module system?**
Before 2015, Node.js had defaulted to CommonJS out of need, since JavaScript didn't have any module system at the time.

Note that CommonJS is not an ECMAScript specification.

Since 2015, ECMAScript does have a standardized module system. It is called EcmaScript Modules or ES Modules or ESM. 

It took a long time for Node.js and browser vendors to fully implement ESM.


## ESM details
- File extensions for ES modules is `.mjs` (for both exporter and importer file).
- There are two types of exports:
	1. **Default exports** - name doesn't have to match. Uses the keyword `default` for exporting. Only one entity can be imported.
	2. **Named exports** - name has to match. Uses `const` in place of `default` for exporting. Multiple entities can be imported.
- About the syntax - `ESM` uses a *sugary* syntax for exports and imports, instead of concrete object and function syntax like `module.exports` and `require`.
- Support:
	- Node.js - stable support since Node v14 (since 2020)
	- Browsers - Chrome, Safari, Firefox since 2019 (safe)
- Usage
	- Node.js - CommonJS is still popular for backend dev.
	- Browsers - ESM is popular for frontend codebases.


## Patterns (default exports)
1. Export a single thing
```js
// math-esm.mjs
const add = (a, b) => a + b;

export default add;


// index.js
import add from './math-esm.mjs'; // name doesn't matter
console.log(add(2, 3));
```
2. Export a single thing - alternate pattern
```js
// math-esm.js
export default (a, b) => a + b;
```
3. Export multiple things
```js
// math-esm.mjs
const add = (a, b) => a + b;
const subtract = (a, b) => a - b;

export default { add: add, subtract: subtract };
export default { add, subtract }; // OR, equivalently


// index.js
import math from './math-esm.mjs'; // name doesn't matter
console.log(math.add(2, 3));
console.log(math.subtract(2, 3));
```
4. Export multiple things, de-structure imported entity.
```js
// math-esm.mjs (same as above)

// index.js
import math from './math-esm.mjs'; // name does't matter
const { add, subtract } = math;

console.log(add(2, 3));
console.log(subtract(2, 3));


// this DOES NOT WORK (weird) - "looks like" the above case, right?
import { add, subtract } from './math-esm.mjs';

console.log(add(2, 3));
console.log(subtract(2, 3));
```


## Patterns (named exports)
1. Export a single thing
```js
// math-esm.mjs
export const add = (a, b) => a + b;

// index.js
import { add } from './math-esm.mjs';

console.log(add(2, 3));
```
2. Export multiple things (most popular)
```js
// math-esm.mjs
export const add = (a, b) => a + b;
export const subtract = (a, b) => a - b;

// index.js
import { add, subtract } from './math-esm.mjs';

console.log(add(2, 3));
console.log(subtract(2, 3));
```
3. Export multiple things, import *all*
```js
// math-esm.mjs (same as above)
export const add = (a, b) => a + b;
export const subtract = (a, b) => a - b;

// index.js
import * as math from './math-esm.mjs';

console.log(math.add(2, 3));
console.log(math.subtract(2, 3));
```
4. Export multiple things, de-structure the *all* entity.
```js
// math-esm.mjs (same as above)
export const add = (a, b) => a + b;
export const subtract = (a, b) => a - b;

// index.js
import * as math from './math-esm.mjs';
const { add, subtract } = math;

console.log(add(2, 3));
console.log(subtract(2, 3));
```
There may be other patterns, like aliases etc. I'll not waste time enumerating all.

We'll be using CommonJS for the remainder of the course, since it's the popular format for Node.js.