# 30. Sending Responses
Created Monday 13 February 2023 at 10:07 pm

- The response (second param) in an `http`'s server callback is not very interesting from a read POV. It's meant to respond (i.e. do an action), so we mostly use functions attached to it.
- It's actually a writable stream.
- Some common functions:
	1. `res.setHeader(headerName, headerValue)`. Header names and values follow a specification, i.e. they're not arbitrary.
	2. `res.write(stringOrBuffer)` - used to send data to the client. If data is large, it'll be sent in chunks automatically. <details><summary>TCP abstraction</summary>`write`, I guess, is an abstraction for sending TCP packets. The exact number of TCP packets will depend on the agreed MSS (Maximum Segment Size) of the connection. Since it's a abstraction over TCP, `res.write` works within the existing HTTP connection without creating a new one.</details>
	3. `res.end()` - finishes the response. Use this at last, as subsequent use of `res` will now in an error.