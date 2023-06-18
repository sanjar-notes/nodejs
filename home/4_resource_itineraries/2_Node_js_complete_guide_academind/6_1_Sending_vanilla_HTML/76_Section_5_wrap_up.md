# 76. Section 5 wrap up
Created Saturday 4 March 2023 at 07:23 pm

Learnt 4 things:
1. Express - a convenient way to write server side code. Built on top of the `node:http` module, and inherits almost all fields (if it may be needed). It's minimalist, but still very useful.
2. Middlewares - the primary construct in Express to run code. Middlewares execute (or skipped) linearly and in order. Special types of middlewares are available for handling requests based on method, route. **Also**, many built-in and 3rd party plugins are available for express.
3. Routers/routing - split code for a route in a separate file. Is the de-facto construct for multi-file express code. Route filter can be turned off (by not specifying it).
4. Serving files statically - the `express.static()` middleware can be used to create a static server in one-line.