# 34. Parsing Request bodies
Created Thursday 16 February 2023 at 09:10 am


# Situation
With the `http` module, the request param doesn't have anything like `request.data`. Instead, the incoming data is sent as a stream.

Technically, the `req` param is a modified version of the readable stream, and therefore has event listeners for the body part of the request.


## How (to parse request body)
There are two scenarios here - work with chunks or collate them in a buffer before working on them. In case the body is text, we'll need to have it fully. Code:
```js
 (req, res) => {
	const enteredMessageBuffer = [];
	req.on("data", (chunk) => {
	  enteredMessageBuffer.push(chunk);
	});
	req.on("end", () => {
	  const receivedRequestBody = enteredMessageBuffer.toString();
	  const bodyObject = JSON.parse(enteredMessageBuffer.toString()); // if JSON is received

	  // use the body here
	});
}
```
[Full code example](https://github.com/exemplar-codes/nodejs-server-academind/commit/588367749067dafd08aa677cc415627fe28799dc)