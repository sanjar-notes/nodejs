# 35. HTTP routing
Created Monday 30 January 2023 at 03:43 pm
// rough
[Currently](https://github.com/exemplar-codes/codevolution-nodejs/commit/f024b46b376893c3be766e3a26b4fa0b231b9eb8), we return the same response for all routes (try it). This is of course, not the case in the real world.

The default route is `/`. Note that by route, we mean the URI.

To respond differently based on routes, access the route using `res.url`. Example:
```js
const http = require("node:http");

const server = http.createServer((req, res) => {
  res.writeHead(200, { "Content-Type": "text/plain" });

  res.end(req.url);
});

server.listen(3000, () => {
  console.log("Server started on port 3000");
});
```
[Code](https://github.com/exemplar-codes/codevolution-nodejs/commit/075d783544353d0d276796facc84e3a7d1d0b7aa)

---
Since we know about the route, we can respond differently using conditionals, switch statements or some custom logic.

Let's create a simple server that has 3 pages:
1. "/" - returns home page HTML
2. "/about" - returns about page HTML
3. "/api" - returns some JSON
4. Respond with 404 (not found) HTTP status code for all other routes.
[Code](https://github.com/exemplar-codes/codevolution-nodejs/commit/0c927326e4dac24023ba2f7fa2cb8948be54a5aa)

---
There are many other useful properties in the request param, like:
1. `req.method` - the request's HTTP verb. Example values: "GET", "POST", "PUT", "DELETE".
2. `req.httpVersion` - http version being used. Example values: "1.1", "2.1".

A combination of these properties can be used to handle any kind of request.