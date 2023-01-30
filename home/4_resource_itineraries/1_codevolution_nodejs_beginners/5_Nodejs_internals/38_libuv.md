# 38. libuv
Created Monday 30 January 2023 at 08:48 pm
// rough
## What
libuv is a cross platform open source library written in the C language


## Why
It handles the asynchronous and non-blocking operations in Node.js (FIXME: multi-threading abstraction is provided by libuv or not?). It abstracts away the complexities of dealing with the OS (FIXME: you mean multi-threading, process management, scheduling right? Because not all OS utilities are hard to use).


## How
How does libuv help with asynchronous and non-blocking nature? It does so with the help of two constructs:
1. Thread pool
2. Event loop

Of course, these are a small part of libuv. These constructs are enough for us to understand how Node.js handles these 3 problems (of synchronous, blocking and single-threaded execution).