# 5. Node.js overview
Created Monday 23 January 2023 at 01:20 am


## What is Node.js? (revisit)
Let's go back to the definition. Node.js is open-source, cross-platform JavaScript runtime environment. We understood all parts.


## What can one build with Node.js
Since Node.js can run outside the browser, it opens a new world of possibilities. Some examples:
1. Traditional websites <details><summary>(but Node.js runs only outside the browser, right?)</summary>Yes. But we can have frontend libraries/frameworks that spit out HTML, CSS, JS in an automated way. We can do this with any language, but it's easier to have a system in the same language (isn't that the primary reason why we made Node.js, 😅😂)</details>
2. Backend services like APIs
3. Real-time application
4. Streaming services
5. CLI tools
6. Multiplayer games
7. Anything that any other general purpose programming language can do.

The crux is that Node.js allows us to build complex and powerful applications.


## Components of Node.js (exploring the source code)
- **deps** (dependencies - external code Node uses). Some are:
	- V8 - JS engine
	- libuv - provides Node.js access to OS features like filesystem, networking
	- crypto - cryptography tool library.

![](/assets/5_Nodejs_overview-image-1.png)
- **src** (source) folder - contains the C++ code of Node.js. Since JavaScript was not designed to run outside the browser (but C++ was) the code here implements the features of Node.js like filesystem, networking.

![](/assets/5_Nodejs_overview-image-2.png)
- **lib** - contains JS code (functions, classes) that apps will use.
	- OS level functions - `fs`, `http`
	- utility functions
	- This is the final component that faces the application code.

![](/assets/5_Nodejs_overview-image-3.png)

Note:
- Unlike the browser runtime, the Node.js does not implement `window`, `document` or other "browser APIs", since it's does no tasks of that need these.


## Summary
- Node.js is _plug_definition_here_
- It's a runtime - not a language, library or framework.
- It can execute JavaScript outside the browser.
- It can execute not only standard ECMAScript but also new syntax and features that are made available through C++ bindings using the V8 engine.
- Node.js consists of C++ files which form it's core features and it exposes them through JavaScript files, to make system programming accessible via JavaScript.
