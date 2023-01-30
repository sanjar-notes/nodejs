# 25. Asynchronous JavaScript
Created Sunday 29 January 2023 at 02:27 am

## JS - most basic form
JS, in it's most basic form is synchronous, blocking and single-threaded.
1. Synchronous - by default.
2. Blocking - due to synchronous nature.
3. Single threaded - default by choice.


## JS - problems with most basic form
JS in this form is not helpful. Let's think:
- Browsers will freeze until there's a network response.
- If JS is made asynchronous (and thus non-blocking), then making HTTP requests is possible, since "work" is done by external devices (internet) - browsers won't freeze.
- Writing server-side however, is almost impossible. At most, the server will be able to handle 1 request at a time. This is different from "HTTP requests" since "HTTP responses" need work to be done by the server.
- Server-side - even if JS is made asynchronous, single-threaded nature will allow only 1 request to be handled at a time (since database, file system reads need be done, and there's only 1 thread)

In other words, this form of JS is not beneficial for writing apps - client-side as well as 


## Making JS asynchronous, non-blocking and \*single-threaded
1. Synchronous - JS is made asynchronous by having an event-loop and task-queues.
2. Non-blocking - JS is automatically made non-blocking when asynchronous operations are possible.
3. Single threaded - To solve this problem, we need to create an abstraction of "single-threadedness" by having runtime components (on the server-side) that either are multi-threaded completely or can atleast get work done in a multi-threaded way using OS level utilities. FIXME: I guess this is what Node.js and the browser (think "service workers") runtimes do. **So, JS becomes \*single-threaded, in the sense that all JavaScript code is single-threaded but it is allowed to use data processed by other threads**. FIXME: \#3 is an educated guess, just verify it once.


## Asynchronous JS programming constructs
I already know these.
1. Events
2. Callbacks, promises, async-await

Note: all these "improvements" constructs - event-loop, task-queues, "single-threaded" wrappers are parts of the runtime, not the JS engine.

[Polling vs Interrupts - document](../../../../assets/ChatGPT-interrupts-vs-polling.pdf)