# 27. fs with Promises
Created Sunday 29 January 2023 at 03:47 am

## fs with Promises
- `fs` module with Promises instead of callbacks.
- Async-await can also be used here, since it's just a syntax sugar over Promises.
- This a new thing, and is common in new codebases, especially ones that use ESM.
- Since promises are handled in the micro-task queue, they are given preference of events.

Note - prefer `fs` over `fs/promises` if maximal performance is needed. (FIXME: `fs/promises` has been fixed now, I [guess](https://stackoverflow.com/questions/68883155/node-js-fs-module-callback-api-vs-promises-api-performance-difference/75271525#75271525))


### Import `fs/promises`
Use `fs/promises` instead of `fs` as import name.
```js
const fs = require("node:fs/promises");
```


### `fs/promises` API
- `readFile` - same as callback based `readFile` except that it returns a promise instead of taking a callback. Promise contains file content as a buffer (by default) or string (if "UTF-8" was specified).
- `writeFile` - same as callback based `writeFile` except that it returns a promise instead of taking a callback. Promise will reject with an error value if an error occurs.

[Code example](https://github.com/exemplar-codes/codevolution-nodejs/commit/1e3a6dc9307f5b4c0e3a2aee09beb99bce287a6f)

