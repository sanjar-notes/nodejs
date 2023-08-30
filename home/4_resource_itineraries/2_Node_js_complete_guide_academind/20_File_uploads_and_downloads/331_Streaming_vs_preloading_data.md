## 331. Streaming vs pre-loading data
Created Thursday 31 August 2023

Basically this means if we're using a buffer or not. Already discussed this in "66 responses".

Again, Express does _not_ provide a direct streaming construct, except that `res` is a writable stream, and therefore piping is supported.

```js
res.sendFile('path-here');

// vs

const fileStream = fs.createReadStream(path.join('/path-of-file'));res.statusCode = 200;
fileStream.pipe(res);
```

Note: join the global path (that we're storing a util here) with the remaining path, to avoid, path issues

Code (commit) - https://github.com/exemplar-codes/online-shop-nodejs-branches/commit/e195d00a700be0aad58c0136b5e0dc8670907dd3