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
- `readFileSync("some_path" [,encoding])` - returns all contents of the file as a "buffer" by default. 
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
- `unlink("some_path", callbackCompulsory)` - delete single file.

Note:
- All these function accepts both relative and absolute paths.
- In case of writing, Node.js creates a file if it does not exist.
- Async modes follow "error first pattern" for callbacks, i.e. the first param is the error, second is the data (if any).
- "utf-8" and "UTF-8" can be used interchangeably.
- Deletions (rmdir, unlink etc): https://hackernoon.com/mastering-nodejs-how-to-delete-files-inside-a-nested-folder

[Code example](https://github.com/exemplar-codes/codevolution-nodejs/commit/68910a170d61be572cefe4dd07df832eee279702)