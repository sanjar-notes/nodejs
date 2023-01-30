# 32. JSON response
Created Monday 30 January 2023 at 12:07 pm

In the previous video, we responded with plain text by using `res.end` and set "Content-Type" header to "text/plain" using `res.writeHead`.

Similarly, we can send JSON (as the response body) by populating the response body (using `res.end()`). Important checks when sending JSON data:
1. Set "Content-Type" to "application/json" so the client can interpret it properly.
2. "Stringifying" the JSON - since `res.end()`(or `res.write()`) only take a string or buffer as argument, we'll have to "stringify" the object we wish to send as JSON, using `JSON.stringify(myObject)`. 

[Code](https://github.com/exemplar-codes/codevolution-nodejs/commit/bfa636d8f3bf1257b2e2e5504085402068a23645)
```js
const http = require("node:http");

const server = http.createServer((req, res) => {
  res.writeHead(200, { "Content-Type": "application/json" });
  const superHero = {
    firstName: "Bruce",
    lastName: "Wayne",
  };
  res.end(JSON.stringify(superHero));
});

server.listen(3000, () => {
  console.log("Server started on port 3000");
});
```

Note: `JSON` is available globally without import. It's implemented inside the JS engine (V8 in case of Node.js, Chrome) itself. To convert a JSON string to an object, the `JSON.parse(json_string)` function is available.