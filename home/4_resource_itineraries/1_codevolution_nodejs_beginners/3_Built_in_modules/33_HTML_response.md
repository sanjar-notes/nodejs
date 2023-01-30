## 33. HTML response
Created Monday 30 January 2023 at 12:33 pm

Just like with text and JSON response, set the correct "Content-Type" ("text/html") and send the HTML as a string using `res.end()` (optionally with`res.write()`).

[Code](https://github.com/exemplar-codes/codevolution-nodejs/commit/00715f610d73485a1e210d22c407f7551e9012ce
)
```js
const http = require("node:http");

const server = http.createServer((req, res) => {
  res.writeHead(200, { "Content-Type": "text/html" });
  res.end("<html><head><title>Test</title></head><body><h1>Hello, world</h1><body>");
});

server.listen(3000, () => {
  console.log("Server started on port 3000");
});
```

---
This code above is fine for a demo. But a server sends HTML *files* and not strings, at the very least.
To send an HTML file, use the `fs` module to read the file. [Code](https://github.com/exemplar-codes/codevolution-nodejs/commit/7705af4df307a9cc8467c4c203898abd62293ba4
)
```js
(req, res) => {
  res.writeHead(200, { "Content-Type": "text/html" });

  const htmlFileContents = fs.readFileSync("./index.html", "utf-8");
  res.end(htmlFileContents);
}
```

---
Some optimizations. 

We could make the process asynchronous by using callback or promises.
[Code - callback](https://github.com/exemplar-codes/codevolution-nodejs/commit/aa3b6efc0d77d1911c5b0852d8bc35ae410dad46)
[Code - Promise](https://github.com/exemplar-codes/codevolution-nodejs/commit/3e3e44efa424b07cd035d1de013459af73b37b7c)

Still, we are reading the whole file (i.e. keeping it in RAM) at once.
To avoid this, we can use streams. Note that doing this result in a *slower* response. 
[Code - streams](https://github.com/exemplar-codes/codevolution-nodejs/commit/49e542aa5f3b7aa41b79db9d9759f6c809b036ea) or even simply [Code - streams with pipe](https://github.com/exemplar-codes/codevolution-nodejs/commit/13278a26abdbbc48caf54598a1945352ff47f66e) (also, realize that `res` param is actually a stream).

Here, the response a continuous stream that takes a long time. i.e. the client will receive data in chunks.
(FIXME: how is this continuous, I mean yes, multiple TCP transfers make sense, but aren't we calling `.end` once. Maybe there's something going on with "keep-alive).