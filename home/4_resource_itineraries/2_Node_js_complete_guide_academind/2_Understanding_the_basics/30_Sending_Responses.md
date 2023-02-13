# 30. Sending Responses
Created Monday 13 February 2023 at 10:07 pm

- The response (second param) in an `http`'s server callback is not very interesting from a read POV. It's meant to respond (i.e. do an action), so we mostly use functions attached to it to build and send response.
- It's actually a writable stream.
- Some common variables and functions:
	1. `res.statusCode` - set this variable to specify the response code. e.g. 200, 404.
	2. `res.setHeader(headerName, headerValue)`. Header names and values follow a specification, i.e. they're not arbitrary.
	3. `res.write(stringOrBuffer)` - used to send data to the client. If data is large, it'll be sent in chunks automatically. <details><summary>TCP abstraction</summary>`write`, I guess, is an abstraction for sending TCP packets. The exact number of TCP packets will depend on the agreed MSS (Maximum Segment Size) of the connection. Since it's a abstraction over TCP, `res.write` works within the existing HTTP connection without creating a new one.</details>
	4. `res.end([,stringOrBuffer])` - finishes the response, optionally do a write before finishing. Use this at last, as subsequent use of `res` will now in an error.

Example ([code](https://github.com/exemplar-codes/nodejs-server-academind/commit/93d4ca94b4194bfc3d5d69ea186f03426a9fa7b1)):
```js
const http = require("http");

const server = http.createServer((req, res) => {
	res.setHeader("Content-Type",  "text/html")
	res.write('<html>')
	res.write('<head><title>My first page</title></head>');
	res.write('<body><h1>Hello from my Node.js server</h1></body');
	res.write('</html>');
	res.end()
});

server.listen(3000, () => console.log("Server running on port 3000"));
```
Note: we can use a single `write` to send the whole text. `http` module can handle chunking.