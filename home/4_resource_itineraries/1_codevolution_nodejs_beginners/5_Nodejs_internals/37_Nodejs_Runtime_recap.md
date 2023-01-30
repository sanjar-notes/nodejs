# 37. Node.js Runtime recap
Created Monday 30 January 2023 at 08:34 pm
// rough
Recollect what the Node.js runtime is: it is an environment that provides all the necessary components to run JavaScript outside the browser. It's components (bottom to top are):
1. External dependencies - V8, libuv, zlib, crypto and others./
2. C/C++ features like file system access and networking
3. JS library - functions and utilities to interface with the C/C++ features.
---
Recollect what asynchronous JavaScript is: JS, in it's most basic form, is a synchronous (code executes top to down), blocking (code written ahead doesn't execute before code before hasn't finished executing, i.e. due to synchronous nature) and single-threaded (only one operation can take place at any given time) language. 

**But**, this is not how JS (in Node.js atleast) behaves. Operations like `fs.readFile` and `res.end` have asynchronous and non-blocking behavior. 
Also if multiple files are read independently (the overall time is less than total sequential time - i.e. multithreaded. FIXME, check this claim.

All these powers of "actual" JavaScript in Node.js are due to an external dependency called "libuv". Let's learn more about it.