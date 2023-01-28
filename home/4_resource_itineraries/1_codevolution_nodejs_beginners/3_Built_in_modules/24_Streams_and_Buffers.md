# 24. Streams and Buffers
Created Saturday 28 January 2023 at 04:00 pm

## Stream
A piece of data that is being moved from one point to another over time.
Examples:
1. File being transferred from one computer to another over the internet
2. Data being transferred from one file to another within the same computer

The goal is to process streams of data in chunks as soon as they arrive, instead of waiting for the entire data to be available for before processing.
This prevents unnecessary data downloads and memory usage.


## Buffer
Buffer is an area where data that's yet to be processed/consumed is kept. i.e. waiting area.

- A buffer is used both if there is a lot (or too less) of data to process but we don't want to do it all at once (for some reason like capacity, efficiency etc).
- Examples - file larger than RAM capacity, streaming a video online - it's not very efficient to let the whole download complete, so chunking is preferred.
- Real life example - a roller-coaster ride with capacity of 30 people. There are two cases:
	1. Too much - 100 people arrive. 70 have to wait in the buffer.
	2. Too few - only 2 people arrive. The ride manager will delay (for atleast 10 people to arrive) or reject starting the ride since it's too expensive to run for so few people.


## Buffers in Node.js
- The server (so Node.js) cannot control the pace at which data arrives in a connection stream.
- It can only decide when is the right time to process the data.
- If there's data already being processed or there's too little data, Node.js puts the arriving data in the buffer.
- It is an intentionally small area that Node.js maintains in the runtime to process a stream of data

Examples: 
1. Playing a video online. The client maintains a buffer where video chunks are kept. These chunks are processed and played at their given timestamp. This has many advantages:
	1. The user doesn't have to wait for the whole video to download completely.
	2. The server doesn't have to load the whole video in RAM, as it sends chunks only.
	3. The user can start a video from somewhere in the middle, and doesn't have to download the part before or after. This also makes the server efficient.
	4. The client stops making requests when the buffer is full (say the next 5 minutes have been downloaded). It will start requests only when the buffer has 1 minute of remaining content. This is good for both client and server, since a user may stop watching a video after some time.
2. Working with large files. Over a network or even locally, there are a lot of files that are quite large (w.r.t RAM) like database files, media, files in general. This is an bigger problem for servers. Buffers help with this.


## Writing some code
`Buffer` is available globally without importing.

- Node.js internally uses buffers when required, and we may never need to work with buffers directly.
- We could have worked well with `fs`, `http` without the knowledge of buffers in this level of detail. But knowing fundamentals is a good thing.