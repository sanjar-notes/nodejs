# 69. Creating HTML pages
Created Tuesday 28 February 2023 at 11:02 am

Until now's we've been sending HTML as a string. That's not at all scalable. In this section, we'll send client side HTML, CSS and JS.

---
It is common for apps to have a fixed number of page skeletons. These are called "views" and stored in a folder named so. A view can either be completely static or contain some parts that may be replaced by relevant data (i.e. server side rendering).

---
[Code - basic routes, HTML files](https://github.com/exemplar-codes/traditional-web-app-express/commit/832b70455ac0e57e18c38f0a32dd69d04a6f1df3)

## Sending HTML files
`res.sendFile()`, enough.

## Specifying file path
`sendFile`, by default takes a single argument - absolute path of file. Doing this however is not realistic, using relative paths is easier.

`sendFile` also accepts a relative path, but the prefix (i.e. `.` or `..`) *needs* to be specified too. Here's the syntax:
```js
sendFile("/home/sanjar/Desktop/shop.html"); // OK, since absolute path

sendFile("./shop.html"); // error!

sendFile("./shop.html", { root: "/home/sanjar/Desktop" }); // OK. Practical to use.
```

### Practically specifying file paths (simple but wordy, saved for posterity)
#### Problem
- The simplest (and best) to specify paths is to start from the project's root, since all files are available from it, and people know where files lie w.r.t it.
- `__dirname` is a reliable way to know absolute paths.
- Problem with `__dirname` is that it refers to the file being executed, and not where it was run from. This is good because we can run our app from anywhere in the system (don't have to navigate to the directory and run), but it's also a little problematic since it's value is different for each file.


#### Solution approach
- A simple way to solve all these issues is to store value of `__dirname` of a top-level file JavaScript file, somewhere somehow.
- Use core module function `node:path.join()` to construct the absolute path of a file before passing it to `sendFile()`.
```js
const myEasyRootPath = ;// stored path

const path = require("node:path");
sendFile(path.join(myEasyRootPath, "views", "shop.html"));
```
Note: Note: it's not neccessary to use top-level, any level from where it's easy (based on knowledge of the codebase) to construct paths to files.


### Solution (any Node project)
```js
// my-project/utils/path.js
const path = require("node:path");
module.exports = path.join(__dirname, "..");
```

```js
// my-project/../../..../some-app-file.js
const rootPath = require("../../util/path.js");
```
Note: 
- Not very helpful since we are having to write a path to get the rootPath. But works reliably. FIXME.
- FIXME: For serving static files directly, i.e. URL ending with raw file, use [`express.static('absolue_path_to_folder')`](https://expressjs.com/en/starter/static-files.html)
- FIXME: add root path to the globally available `process` variable. Experiment later.


#### Solution in Express
- Express projects usually have a top-level file where the server first runs. This top server file is usually at the root itself, or atleast at a place higher than all sendable files. Simply store the `__dirname` in the "app settings", using `app.set('easy-root-path', __dirname)`.
- Where to store root path - in top-level app's 'settings'. And since the root "app" is available  to every middleware, including routers (nested or not), we can read the value:
	- At the top-file itself - `app.get('easy-root-path')`
	- At a place below top-file - `req.app.get('easy-root-path')`. This is because `req.app` (or `res.app`) available in all middlewares and point to the root Express "app".

```js
// top level file, index.js, app.js OR src/app.js
const express = require("express");
const app = express();

const shopRouter = require("some-path-to-shop-router");
app.set('my-easy-root-path', __dirname); // key name important

app.use("some-shop-uri-here", shopRouter);

...more code here
```

```js
// nested router, middleware etc - shop.js
const express = require("express");
const router = express.Router();

const path = require("node:path");

router.get("my-uri", (req, res, next) => {
	const fileToSendPath = path.join(req.app.get('my-easy-root-path'), "views", "shop.html");

	res.sendFile(fileToSendPath);

	// or equivalently, a little verbose though
	res.sendFile(path.join("views", "shop.html"), { root: req.app.get('my-easy-root-path') });
});

... more code here
```
Note: don't export root path from a server file, or any file containing app code since it can result in circular-dependency errors. Exporting root path from a utility file is fine, though.

[Code - file paths in Express app](https://github.com/exemplar-codes/traditional-web-app-express/commit/a448f3db4fe924b61ad5b4f1db03ff60442d9c90)