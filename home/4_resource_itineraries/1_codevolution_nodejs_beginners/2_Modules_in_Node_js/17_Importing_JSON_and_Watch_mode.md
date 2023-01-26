# 17. Importing JSON and Watch mode
Created Thursday 26 January 2023 at 09:55 pm

## Importing JSON
JSON (JavaScript Object Notation) is a data interchange format commonly used by web servers.

- JSON files can be imported using `require`, no special syntax needed.
- Optionally, `.json` extension can be omitted. However, this is discouraged, since Node.js will look for a file with `.js` before considering `.json` and there could be `.js` file of the same name.
  
"data.json"
```json
{
  "name": "Bruce Wayne",
  "address": { "street": "Wayne Manor", "city": "Gotham" }
}
```
"index.js"
```js
const data = require("./data.json");
console.log(data);      // works
console.log(data.name); // works
```
This is helpful for storing mock data.

## Watch mode
An in-built feature like nodemon or LiveServer (the vscode extension). This was introduced in Node v18.

To use, run `node` with the `--watch` option with a file as argument.
Examples:
```sh
node --watch index.js
node --watch index
node --watch .

node --watch myFile.js
```