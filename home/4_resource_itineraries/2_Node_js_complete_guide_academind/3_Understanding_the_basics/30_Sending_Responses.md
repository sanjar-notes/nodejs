# 30. Sending Responses
Created Monday 13 February 2023 at 10:07 pm

- The response (second param) in an `http`'s server callback is not very interesting from a read POV. It's meant to respond (i.e. do an action), so we mostly use functions attached to it to build and send response.
- It's actually a writable stream.
- Some common variables and functions:
	1. **Status**: `res.statusCode` - set this variable to specify the response code. e.g. 200, 404.
	2. **Headers**: `res.setHeader(headerName, headerValue)`. Header names and values follow a specification, i.e. they're not usually\* arbitrary. \*custom ones can be created easily.
	3. **Body**: `res.write(stringOrBuffer)` - used to send data to the client. If data is large, it'll be sent in chunks automatically. <details><summary>TCP abstraction</summary>`write`, I guess, is an abstraction for sending TCP packets. The exact number of TCP packets will depend on the agreed MSS (Maximum Segment Size) of the connection (i.e. multiple `.write` don't mean that many TCP packets - Node.js has a buffer it maintains, where all `.write()` data is kept, a TCP packet is created and sent only when this buffer fills up. However, there is a way to explicitly cause a TCP packet to be created and sent, even if the buffer hasn't filled up - `res.flush()`. Using this without a good reason is discouraged for network efficiency reasons. Since it's a abstraction over TCP, `res.write` and `res.flush` work within the existing HTTP connection without creating a new TCP packet. See [gpt3-res-flush-tcp-node](/assets/gpt3-res-flush-tcp-node.pdf)</details>
	4. **End response**:`res.end([,stringOrBuffer])` - finishes the response, optionally do a write before finishing. Use this at last, as subsequent use of `res` will now in an error.

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
Note: 
- We can use a single `write` to send the whole text. `http` module handles chunking and transmission automatically.
- `res.end()` doesn't end the callback function. Also, `res.end()` it should be the last interaction with `res`. Thus, we may need to `return` from the function, if there's an unguarded interaction with `res`. For example:
```js
(req, res) => {
	if(req.url === '/') {
		res.write("Hello");
		res.end();
		// return; if missing
	}

	res.write("Page not found"); // ...we get an error
	res.end();
}
```
- Headers should be sent first, and completely, before the body is sent. This is not something Node.js or `node:http` specific. It's in the HTTP specification. This means that `res.writeHead` can only be done once, in a request-response lifecycle.
- There's no way to explicitly send headers. They're sent automatically when `res.write()` or `res.end()` is run. Of course, they're only sent once.

## Optional - streaming stuff
It's very easy to "stream" stuff, since the response param is a stream.

Most browsers can directly consume popular MIME types (atleast Chrome).

Common data types:
- Text - need to set headers `Content-Type: text/plain` and `X-Content-Type-Options: nosniff`. [Code](https://github.com/exemplar-codes/nodejs-server-academind/commit/a251ee567861b835c46c9e17c1c8106f4aeb8236)
- HTML - set `Content-Type: text/html`. [Code](https://github.com/exemplar-codes/nodejs-server-academind/commit/665951340266df242d7573aba4a249e122d68ef2)
- Music (mp3) - set `Content-Type: audio/mpeg`. [Code](https://github.com/exemplar-codes/nodejs-server-academind/commit/66d92a21d7efc55e103b3e312b395ac5889a8dcb)
- Images (jpg or jpeg) - set `Content-Type: image/jpeg`. [Code](https://github.com/exemplar-codes/nodejs-server-academind/commit/77081114e9f10e3440873640993cb3a6a1f315bd)

Note: 
- Derived: This isn't actually a new thing, `res.write()` does chunking automatically anyway. It's just that the streaming is more noticeable for large files.
- No client code was needed here. Simply visiting the endpoint worked.
- Of course, this was a very simple scenario. Streaming data is a complex engineering problem that depends on the application, environment, size of the system etc.