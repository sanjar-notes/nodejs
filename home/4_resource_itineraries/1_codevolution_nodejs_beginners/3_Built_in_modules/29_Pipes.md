# 29. Pipes
Created Sunday 29 January 2023 at 07:36 pm

// FIXME: rough done. Not immediately important. Just for fundamentals
In the previous lesson, we learnt about streams to read and write files.
This seems to be a common pattern in server programming and systems programming.
Node.js has a simpler and better pattern that does the same - called piping.

In non-technical terms, we understand what a pipe is. A pipe transports matter from one device to another, over some period of time.

Similarly, in Node.js, the "pipe" method connects the readable stream to a writable stream.
![](../../../../assets/Pasted%20image%2020230129194113.png)

[Code](https://github.com/exemplar-codes/codevolution-nodejs/commit/85f89e279119f9096eddea4882f445644a58aed5)

Pipes, by their very nature are chain-able. However, only a non-writable stream can be changed. This is because all parts of a chain should update one by one, and not abruptly (i.e. its like mutating an array while traversing it, not a good idea). Here we are using writableStream, so we cannot pipe further.

To demonstrate piping, let's create a compressed file containing some text. [Code](https://github.com/exemplar-codes/codevolution-nodejs/commit/ef9cb9b25dc2ae09e63aedcad4ecbc4afa97fc42)