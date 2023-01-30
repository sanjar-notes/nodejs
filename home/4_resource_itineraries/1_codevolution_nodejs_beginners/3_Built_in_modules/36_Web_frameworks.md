# 36. Web frameworks
Created Monday 30 January 2023 at 04:10 pm
// rough
We learnt many things about the http module. We created servers using it that can send back text, HTML, JSON, status code based on routes, methods etc.

This is fine.

But, this is not how one would make a large application. We'd instead use a "framework".

---
A framework simply abstracts the lower level code allowing us to focus on the requirements than the code itself. It does this by providing "code" (functions, classes) and "rules" (opinions on file structuring etc) on top of which we build apps. A library doesn't have the "rules" part.

Note: apart from abstraction and rules. Frameworks also provide "extra" code that is incidentally (generally) needed for the main purpose.  Frameworks that have this are said to be "batteries-included".

Example - Angular, React, Vue are all frameworks/libraries that help you build UIs without having to rely on the lower level DOM API in JavaScript.

Similarly there are "backend" frameworks that can be used to build server apps without having to work with Node's HTTP module. Examples - express, nest, hapi, koa and sails. We'll not learn about a specific framework in this course. This course is about core Node.js
