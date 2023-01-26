# 18. Built-in modules
Created Friday 27 January 2023 at 12:06 am

As mentioned before, there are 3 types of modules in Node.js - local, built-in and third party. We studied local modules in the last section. This section is about built-in modules.

- Built-in modules are also known core modules.
- They are available as part of the Node.js installation. They don't need to be installed separately.
- They DO need to be imported before use.

There are a lot of built-in modules, but we'll take a look at 5 most common (and useful) ones:
1. path
2. events
3. fs
4. stream
5. http

path is easy to understand, but the remaining 4 are a little more complex.

The source code for these can be found under the `lib` folder of Node.js's [source code](https://github.com/nodejs/node/tree/main/lib).