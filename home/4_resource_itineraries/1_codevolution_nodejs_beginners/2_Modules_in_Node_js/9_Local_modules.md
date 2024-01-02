# 9. Local modules
Created Monday 23 January 2023 at 11:18 pm

- Local modules are modules we create. 
- Each JavaScript file is a module.

## Breaking a file into modules
Suppose all our code is written into a single file `app.js`.
```js
// file 1 - util code
const add = (a, b) => a + b;

// file 2 - app code
const sum = add(1, 2) 
console.log(sum); 
```
Now, we wish to split the code into two files (for better organization).

Assume we do this segregation. But how do we tell Node to run both files in proper order and make the `add` function available to the second file.

This is where CommonJS comes in. JavaScript, for a long time, didn't have a module system. It was only later that a module system was standardized. "CommonJS" was the first standard (that's still supported by all systems). It uses a function and object approach to export and import code between modules.


## How to import/export
1. To import  - use the `require` function which takes the path of the module(file) as argument. `require` is available inside every file.
`myMain.js`
```js
const addFunction = require('./add.js');

console.log(addFunction(1, 2));
```
2. To export something (variable or object or class) - use the `module` object, specifically the `module.exports` attribute. `module` object is available inside every file.
`add.js`
```js
const add = (a, b) => a + b;

module.exports = add;
```
To run the app, just run `myMain.js`.

Note:
1. **Names don't matter** - There's no need to use the same name for importing and exporting stuff. CommonJS uses a function (`require`) and an object `module` for import/export - so names don't matter.
2. **Importing a module executes it** - A file will execute completely, if it exports something. i.e. you can't import stuff from a file without causing a full execution of that file.
3. **Omit `.js` extension** - we can omit the `.js` extension in `require`. This is optional.
4. **"Loading" a file** - `require`ing a module that exports nothing will just run the file. There will be no errors. This is also called "loading" a file, which is sometimes needed, e.g. we wish to do (void function) things in order but they are unrelated, so "exporting" doesn't make sense. Also, loading them from a single file is definitely better than providing multiple arguments to `node` in the correct order.
5. **"Named" and "default" exports** - `module.exports` is the single source of exports from a file. So, if we need to export only one thing (a "default" export), one can directly write to it. But for exporting multiple things, we just export an object or an array containing the things we wish to export. Imports work like usual, i.e. we destructure or use dot notation to access exported things.
	```js
	// mathFuncs.js
	const add = (a, b) => a + b;
	
	module.exports = {
		add,
		subtract: (a, b) => a - b
	}
	
	// or equivalently
	module.exports.add = add;
	module.exports.subtract = (a, b) => a - b };
	```


## Local modules execution flow
Let's add some print statements to observe the execution flow.
`myMain.js`
```js
console.log("myMain.js started execution"); // 1 (start)

const addFunction = require('./add.js'); // 2

console.log("back in myMain.js"); // 8

console.log(addFunction(1, 2)); // 9

console.log("myMain.js finished execution"); // 10 (end)
```
`add.js`
```js
console.log("Inside add.js"); // 3
const add = (a, b) => a + b;  // 4

console.log("Still executing add.js"); // 5

module.exports = add; //6 // file execution does not stop here

console.log("Completing add.js execution"); // 7 // this DOES execute
```
This is the flow.
Note: "exporting" does not end execution of a file, i.e. it's not like a `return` inside function.


## More about local modules
- Each module is isolated from all others, by default. 
- **In other words**, Node.js does not 'watch'/'consider' all files in the projects before running something. The scenario where multiple files are run is If a file (say `app.js`) imports another one (`sound.js`),  and is run, the other file (`sound.js`) will be run, but only because it was imported.
- It's best to have a single top-level file (module) which imports some modules (which import some other module ...). This makes it easier to run the app, since only a single argument needed to be passed.

This is sufficient to work on any Node.js project, but we'll dive a little deeper and see how modules work.