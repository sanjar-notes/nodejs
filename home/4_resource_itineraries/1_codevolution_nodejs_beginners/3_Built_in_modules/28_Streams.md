# 28. Streams
Created Sunday 29 January 2023 at 06:42 pm

## Thinking out loud
// FIXME: rough - done. Not immediately important. Just for fundamentals
// will probably help in completion - https://medium.freecodecamp.org/node-js-streams-everything-you-need-to-know-c9141306be93

Let's learn about streams using the fs module.

A stream is a sequence of data that is being moved from one point to another over time.
Example - moving a large file within a computer

The idea is to work with data in chunks instead of loading(in RAM)/downloading/uploading entire data at once.

This "chunking" prevents unnecessary memory usage. Secondary advantages are low internet bills.


Stream is in fact a built-in node module that inherits from the event emitter class.

We rarely work with streams directly.

Other modules internally use streams for their functioning.

Let's explore how the `fs` module uses streams to read and write data.

To read data, we use "readable stream" available via `fs.createReadStream("my_path", options)`, example of "options" - `{encoding: "utf-8"}`. Using this we can create a stream that reads data from `file1.txt`.

Similarly create a writable stream using `fs.createWriteStream("my_path" [, options])`. Example options -  `{flags: 'a'}` for append mode.

Now, "Streams" inherit from the EventEmitter class. Streams emit an event whenever they update. We can  add listeners...

Readable stream has a "data" event that we can add a listener for. This listener receives a chunk of the data from the stream. We can write to the writable stream via `.write` from inside this listener.

`myReadableStream.on("data", (chunk) => {})"`

[Code example](https://github.com/exemplar-codes/codevolution-nodejs/commit/d6bb66feef879d5e35f718d3984ef065be0b5c9e)
```js
const fs = require("node:fs");

const readableStream = fs.createReadStream("./file.txt", { encoding: "utf-8" });

const writeableStream = fs.createWriteStream("./file2.txt");

readableStream.on("data", (chunk) => {
  writeableStream.write(chunk);
});
```

[Code example for append write](https://github.com/exemplar-codes/codevolution-nodejs/commit/5d4efacf6849affdbf20a5f4aeb0c0be4d6fcdf8)

Question: how big is the chunk?
Answer: the default "read" buffer is 64 KB. So, if the file is less than this size, the "chunk" contains the whole file contents. Yet, to simulate a large file, we can change the buffer size. `highWaterMark` in bytes. [Code](https://github.com/exemplar-codes/codevolution-nodejs/commit/b7bed560a8a27b38e95d9c9d30be5bd363e925e3).

Question2: Isn't write an async operation too, shouldn't we use events for that as well. Or can we just batch writes?
Answer: IDk


HTTP module also uses streams. the "HTTP request" is a readable stream, and "HTTP response" is a writeable  stream.

## Types of Streams
1. Readable streams - from which data can be read.
2. Writable streams - to which we can write data.
3. Duplex streams - are both readable and writable
4. Transform streams - that can modify or transform the data as it is written and read

Examples:
- Reading, writing from a file are readable, writable streams respectively 
- Sockets is a duplex stream
- File compression where we can write compressed data and read de-compressed data to and from a file as a transform stream.

## Streams concepts undiscussed (FIXME)
source: [chatgpt](https://chat.openai.com/c/4346dd1f-eb30-44d0-a8fb-863472d483f5)
> Streams are a powerful and efficient mechanism in Node.js for handling data, especially when dealing with large datasets or real-time processing. They provide a way to read or write data in chunks, making it memory-efficient and allowing for asynchronous processing.

Here are some key concepts and features related to Node.js streams that you might find interesting:

1. **Readable Streams:**
   - Represent a source of data that you can read from.

2. **Writable Streams:**
   - Represent a destination for data that you can write to.

3. **Transform Streams:**
   - Act as both readable and writable streams, allowing for data transformation during the process.

4. **Piping:**
   - The `pipe` method allows you to easily connect readable and writable streams, creating a seamless data flow.

5. **Events:**
   - Streams emit events like 'data', 'end', and 'error', allowing you to respond to different phases of the streaming process.

6. **Object Mode:**
   - Streams can operate in object mode, where each chunk is treated as a discrete object, rather than a chunk of binary or string data.

7. **Backpressure:**
   - Streams handle backpressure automatically, ensuring that the producer doesn't overwhelm the consumer with data.

8. **Custom Streams:**
   - You can create custom streams by extending the `Transform`, `Writable`, or `Readable` classes, tailoring them to your specific needs.

Node.js streams are an essential part of building scalable and performant applications, especially when dealing with I/O operations, network communication, or data processing. Feel free to ask any specific questions or explore more aspects of Node.js streams as you dive into learning and experimentation!