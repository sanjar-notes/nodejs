# 3. Chrome's V8 engine
Created Sunday 22 January 2023 at 09:00 pm

## JavaScript engines
JavaScript is a high level lang. A JavaScript engine converts JS code to machine code that can be run directly.

Engines are typically developed by web browser vendors. Some popular ones are:
- V8 - open-source, powers Google Chrome and developed by the same team
- SpiderMonkey - powers Mozilla Firefox
- JavaScriptCore - open-source, powers Safari. Developed by Apple
- Chakra - developed for the original Microsoft Edge (the latest one uses V8)

Our **focus** is on V8, since it's at the core of Node.js.


## V8
Let's see the V8 source code.

- Implements ECMA-262
- Written in C++
- It can run standalone, or can be *embedded* into any C++ application. **This fact helped in the creation of Node.js**.

Since C++ is great for low level operations like file handling, database connections, network operations - and as V8 is a JS <--> C++ bridge, we can now use JavaScript outside the browser.

So, all we need to do is create *a C++ program* that embeds V8.

This *C++ program* with a lot of other functionality is Node.js.


## Summary
- In 2008, Google created a JS engine called V8.
- V8 can be used independently or as a part in C++ programs.
- This means we can write a C++ program that accepts JS and interacts with the computer (outside the browser). This is the core idea behind Node.js.