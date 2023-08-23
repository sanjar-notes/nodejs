# Creating the error *sink*
Created Wednesday 23 August 2023

It's very easy to create the "error sink" (discussed in app wide structure) using error handling middlewares of Express.

Make sure that a response is sent.

```js
// 'express' import, app code, routers etc

// error sink
// add as the last middleware (after 404, even)
app.use((err, req, res, next) => {
	console.log('Error sink reached');


	// responding is mandatory here, or the app will hang
	res.send();
});


// app.listen here
```