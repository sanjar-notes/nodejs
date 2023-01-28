# 26. fs module
Created Sunday 29 January 2023 at 02:59 am

fs is a core module meant for filesystem operations (list, find, create, read, update, delete).

## Importing
- fs needs to be imported.
- It returns an object with various methods.
```js
const fs = require("node:fs");
```


## fs API
- `readFileSync("some_path" [,encoding])` - returns contents of the file as a "buffer" by default. 
	- If "utf-8" (or "UTF-8") encoding is specified, returns the file contents as a `string`. 
	- Executes synchronously (blocking).
- `writeFileSync("some_path", content [, option])` - write given content to the file. 
	- Content can be `string` or buffer. 
	- "option" is an object. Example - `{ flag: 'a' }` is used for writing in append mode.
	- Executes synchronously (blocking).
- `readFile("some_path" [,encoding], callback)` - just like `readFileSync` but executes asynchronously.
	- callback: has two parameters - error and data. Error is null if no error occurs. data is a buffer or a string (if encoding "UTF-8" was specified).
- `writeFile("some_path", content [, option, callback])` - just like `writeFileSync` but executes asynchronously. 
	- callback has one parameter - error. Error is null if no error occurs.

Note:
- All these function accepts both relative and absolute paths.
- In case of writing, Node.js creates a file if it does not exist.
- Async modes follow "error first pattern" for callbacks, i.e. the first param is the error, second is the data (if any).
- "utf-8" and "UTF-8" can be used interchangeably.

[Code example](https://github.com/exemplar-codes/codevolution-nodejs/commit/68910a170d61be572cefe4dd07df832eee279702)


## fs with Promises
- `fs` module with Promises instead of callbacks.
- Async-await can also be used here, since it's just a syntax sugar over Promises.
- This a new thing, and is common in new codebases, especially ones that use ESM.
- Since promises are handled in the micro-task queue, they are given preference of events.

Note - prefer `fs` over `fs/promises` if maximal performance is needed. (FIXME: `fs/promises` has been fixed now, I [guess](https://stackoverflow.com/questions/68883155/node-js-fs-module-callback-api-vs-promises-api-performance-difference/75271525#75271525))

### Import `fs/promises`
Use `fs/promises` instead of `fs` as import name.
```js
const fs = require("node:fs/promises");
```

### `fs/promises` API
- `readFile` - same as callback based `readFile` except that it returns a promise instead of taking a callback. Promise contains file content as a buffer (by default) or string (if "UTF-8" was specified).
- `writeFile` - same as callback based `writeFile` except that it returns a promise instead of taking a callback. Promise will reject with an error value if an error occurs.

[Code example](https://github.com/exemplar-codes/codevolution-nodejs/commit/1e3a6dc9307f5b4c0e3a2aee09beb99bce287a6f)

