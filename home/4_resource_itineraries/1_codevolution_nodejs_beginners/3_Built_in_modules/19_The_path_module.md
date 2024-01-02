# 19. The path module
Created Friday 27 January 2023 at 12:16 am

## path module
Meant for manipulating paths (filesystem locations).
I doesn't *do* anything - for that you'll need the "fs" module.

## Two path related convenience variables
Node.js provides two convenience variables that are available by default (no import needed). They are:
1. `__dirname` - absolute path current directory .
2. `__filename` - absolute path of current module (file).

In short, if you just need these, there's no need to use the `path` module.


## Path API
Path module has 14 properties and methods. We'll look at the 7 most used ones.
- `path.basename("my_path_here")` - last portion of a given path
- `path.extname("my_path_here")` - extension of the file at path. Returns empty string otherwise - for a directory or invalid path.
- `path.parse("my_path_here")` - an object containing useful information about the path.
- `path.format(pathObject)` - returns an absolute path string for given "path" like object.
- `path.isAbsolute("my_path_here")` - boolean
- `path.join()` - returns an absolute path by joining path segments. Additionally, it takes care of platform specific delimiters and does normalizing (ignoring, adding delimiters and process nesting delimiters if any). Delimiters - `/`, `\`, `.`, `..`
- `path.resolve()` - behaves like `join()`, except it is processed right to left. Also the latest (right most argument) becomes the root if it has a `/`. If no argument has a `/`, the actual system root path becomes the root. Returns an absolute path in all cases.

Example:
```js
const path = require("node:path");

const currentDirectoryConvenienceVariable = __dirname;
console.log(currentDirectoryConvenienceVariable);
const currentModuleConvenienceVariable = __filename;
console.log(currentModuleConvenienceVariable);


console.log("\n# basename");
console.log(path.basename(__dirname));


console.log("\n# extname");
console.log(path.extname(__filename));


console.log("\n# parse");
console.log(path.parse(__filename));
console.log(path.parse(__dirname));


console.log("\n# format");
const obj1 = path.parse(__filename);
const obj2 = path.parse(__dirname);
console.log(path.format(obj1));
console.log(path.format(obj2));


console.log("\n# path.join");
console.log(path.join("folder1", "folder2", "index.html")); // simple join
console.log(path.join("/folder1", "folder2", "index.html")); // simple join
console.log(path.join("/folder1", "//folder2", "index.html")); // smartly ignores redundant
console.log(path.join("/folder1", "//folder2", "../index.html")); // smartly ignores redundant, processes nesting
console.log(path.join(__dirname, "data.json"));


console.log("\n# path.resolve");
console.log(path.resolve("folder1", "folder2", "index.html")); // no root like argument, so actual root becomes root
console.log(path.resolve("/folder1", "folder2", "index.html")); // has a root like argument, so it becomes root

console.log(path.resolve("/folder1", "//folder2", "index.html"));
// has multiple root like arguments, the latest one becomes root, smartly ignores redundant delimiter

console.log(path.resolve("/folder1", "//folder2", "../index.html"));
// has multiple root like arguments, the latest one becomes root, smartly ignores redundant delimiter, processes nesting

console.log(path.resolve(__dirname, "data.json"));
```