# 62. Responses
Created Thursday 23 February 2023 at 12:27 am

# Situation
obvs


## Syntax
```js
const express = require("express");

const app = express();

app.use((req, res) => {
  res.send("Hello, world"); // sent as "text/plain"
});

app.listen(3000, () => console.log("Server running on port 3000"));
```

### 1. Status
 - `res.status(200)`
 - `res.sendStatus(200)` sends the status code with the corresponding status message as text, it also ends the response.

### 2. Headers
`res.set`

There are two forms:
	1. One header - two args. `res.set(HEADER_KEY, HEADER_VALUE)`. Example: `res.set('Content-Type', 'text/plain')`
	2. Multiple headers - one object as argument. `res.set({key1: value1, key2: value2})`. Example:
```js
res.set({
  'Content-Type': 'text/plain',
  'Content-Length': '123',
  ETag: '12345' // no hypen, so string notation not needed
})
```

### 3. Body
1. S*end* variables - `res.send()`. This is supposes to be the "convenient" default over `http.req.end` (which is still available if needed). It behaves in the usual way, i.e. ends the response. It accepts all *JSONable* data types `String`, `Boolean`, `Array`, `Object`. Accepts `Buffer` too.
2. Send JSON - `res.json()`. Prefer this over `res.send` for JSON responses.
3. S*end* a file (not download) - `sendFiles("absolute_file_path")` or alternatively `sendFiles("relative_path", {root: ""})`. Zip files will be automatically be downloaded in the browser, as they're not consumable directly. **Intended for small files only, since it doesn't use chunking**.
4. Send a file (for download) - `res.download(...)`. Same as `res.sendFiles`, except sends proper headers and causes download on the browser.
5. Send file efficiently - create a read stream, pipe it through to `res`, just like with vanilla `http` module.

Note: 
- There's auto content-type inference, for variables and files both. It's binary level for files (so wrong extension is also handled properly). [Code](https://github.com/exemplar-codes/express-app-academind/commit/60e88a6d4bf1524c789749811c72076b0fae48da)
- `res.write()` (inherited from `node:http`) is still available, for sending data without ending the connection. Just [remember](https://stackoverflow.com/a/34187352/11392807) the `"no-sniff"` header value.
- If using `res.write()`, don't use `res.send()` or `res.json()` etc. Either send body using `node:http` methods or Express methods, otherwise it leads to errors. FIXME: why does this happen?

### 4. Convenience functions
1. Redirect - `res.redirect([statusCode=302], "my_absolute_or_relative_location")`.
2. Set the content-type header - `res.type("content_type_value")`. Partial arguments are fine - i.e. if "/" is absent in the argument, for example "html", it'll set the type correctly (i.e. "text/html"), else will set it to same as passed argument.


## Examples and nuances
1. Types of responses (content types):
	1. [Text](https://github.com/exemplar-codes/express-app-academind/commit/384f76a1ee9c2aac45cee6a35d27732f2e7ed477) - `res.send("my_string_here")`. Sent as `"Content-Type: text/plain"`.
	2. [JSON](https://github.com/exemplar-codes/express-app-academind/commit/62d86f57f68134d39b1883bbf0e6fe7b3b9f2c26) - `res.send(myJSONObject)`. Sent as `"Content-Type: application/json"`. Object should be JSON serializable.
	3. [HTML](https://github.com/exemplar-codes/express-app-academind/commit/63559a1ddc7f97c224512df5e57342d73f145fda) - `res.send("my_HTML_here")`. Sent as `"Content-Type: text/html"`.
	4. Image, audio - `res.sendFile("./path_to_file", { root: __dirname})`. Will be sent as proper `"Content-Type"`. [Code example](https://github.com/exemplar-codes/express-app-academind/commit/9c2c6b1279b031b2af273491258e5532ab8c6f09)
	5. [ZIP file](https://github.com/exemplar-codes/express-app-academind/commit/17cc84628b179cc68d3f40adbb85ef0d39ec0577) - `res.sendFile("./path_to_file", { root: __dirname})`
2. Middlewares can be run (i.e. `next()` works) even after ending the response. Don't if this is a bad practice or a deliberate thing for stateful servers. FIXME.
3. Avoid double response ends.
4. Express only `res` functions are chainable. This chaining doesn't work with `http.res.` functions, use individual statements with them.


## Doubts
1. Sending some data with redirect - not possible/encouraged since redirect is a complete action itself, it cannot be paired with a data response. Technically, redirect does send an automatic response - the HTML of the new location. If I still want to send some data, I can add a temporary query string in the redirect location. See [StackOverflow](https://stackoverflow.com/a/62297733/11392807).