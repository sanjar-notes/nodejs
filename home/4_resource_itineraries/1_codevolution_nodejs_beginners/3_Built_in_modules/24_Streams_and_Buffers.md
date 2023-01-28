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
- [Code](https://github.com/exemplar-codes/codevolution-nodejs/commit/c5623674cad1bdb19fbca5e00dc31bf22c703166): using the "Buffer" class.
- [Code](https://github.com/exemplar-codes/codevolution-nodejs/commit/147ee60013a120e8655c627e540f254a1cf65b85): Writing to buffers

- Node.js uses buffers internally when required, and we may never need to work with buffers directly.
- We could have worked well with `fs`, `http` without the knowledge of buffers in this level of detail. But knowing fundamentals is a good thing.


## Opinion - BLOBs are not common in core business servers (FIXME: guess)
Working with stream, buffers, receiving/sending large files is not a usual thing for most server side apps.

The reason is that core business web-apps (servers) work mostly with text data (JSON) etc. All images, videos, files in apps are not uploaded/downloaded from/to the server. Instead the server just provides "links" (text) with some authorization data to clients. Clients then download files from 3rd part cloud computing storage services, as needed. Uploads too, are handled this way, i.e. client side code directly uploads to the external service, and shows progress/success based on responses from the external service. Upon success, the client receives a URL and auth data from the external service, which is passed along to the core business server, which stores the link + data.

In other words, APIs in core business web-servers don't work with BLOBs. They offload all BLOBs to external services and just work with URLs and authorization data (which is text).


**Q1**: Don't we still need to work with streams since we do have to write client side upload code, based on which we show progress?
**A1**: Mostly no. External storage services provide a SDKs (for both client and server) that do the uploading and expose "scalar" values that we can poll against, or it provides events that do something equivalent. We use these for showing progress.

**Q2**: Why do businesses use 3rd party services for large storage?
**A2**: On prem-servers are rare, unless it's a very big business. I'll assume that the business is already using cloud services even for small "scalar data". 
There are many reasons for using 3rd party services for large storage:
1. Using a simple compute + storage service is expensive, compared to a storage service offered by the same platform.
2. Having a dedicated endpoint for BLOBs makes development easy, as compared to having both BLOB APIs and "scalar" APIs run on the same server, since a BLOB operation could significantly hinder even small "scalar" API requests.
3. Development/maintenance costs - writing custom BLOB APIs, using file databases means hiring more developers with niche experience - this can be very expensive, especially for small businesses. Maintaining the code is another task.

BTW, using cloud services also has it's own challenges - huge accidental expenses, large bills in general, vendor lock in, lack of customization, rate limits etc.

This is becoming even more common, as 3rd party services and cloud computing is becoming popular.
