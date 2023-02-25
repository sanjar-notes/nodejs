# 39. Wrap up
Created Sunday 19 February 2023 at 10:41 am

## Stuff learnt
1. Request-Response model of the Web
2. Node.js code runs in a non-blocking way, the event loop, yada yada. Two important things about code execution and event loop:
	1. The event loop comes into play only after all top-level synchronous code has finished execution.
	2. The program stops when the event loop has handled all events.**A Web server program never stops since the _listen_ event never ends**.
4. Request *data* (aka body) is a readable stream through events on it. Response data is a writable stream.
5. Double responses should be avoided, since it leads to an error.

![](../../../../assets/Pasted%20image%2020230216074600.png)


## Conclusion
- This was a lot nitty-gritty information and code. This is not the way (i.e. the right layer of abstraction) web apps (servers) are developed, generally.
- This section was important to understand the basics and how things work under the hood.