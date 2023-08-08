## 535. Handling CORS Errors

<strong><em>no description</em></strong>

<v Instructor>So what's that CORS thing,</v> and that course problem,? 

As I mentioned, I did already cover a CORS earlier in the course in their rest
API section. 

So there you'll all define that same information. 

In the end CORS, short for cross original resource sharing is a security
mechanism and forced by the browser that makes sure that server A can't just
send a request to server B and get data from it. 

Server B instead needs to allow that. 

So if you have a front end application, running on server A, let's say our react
single page application running on local host 3000, and we have our other
application, our backend, let's say, running on server B in this case, our Rest
API, then the communication from A to B will not be possible just like that. 

By default browsers prevent GET, POST, PATCH and so on requests, if frontend and
backend server are not the same one. 

And here on local host, even different ports, imply different servers. 

So local host 3000 is not the same as local host 8,000. 

Now this is a default security mechanism however, we can tell the browser that
we do want to allow access, and we have to set this setting on the server where
we do host the data. 

So on the backend, on the Rest API there, we can set specific response headers,
to responses we sent back to the front end application that tell the browser
that serves the front end application that getting that data is okay, and the
front then should be able to proceed. 

And it's really important to also keep in mind that this is just a browser
security mechanism, which is why we had no problems fetching and storing data
with Postman. 

This simply doesn't care about this CORS thing. 

The browser does, however, and that's where we're getting a CORS error here. 

Now, how can we manipulate our Deno code to make sure that such requests are
possible. 

Well, we need to switch to our Deno code and for that, I'm going to make sure
that my Deno extension is turned on again, to ensure that I get proper IDE
support and now here, on the backend and the backend code, I wanna add a new
middleware, which essentially makes sure that every outgoing response has the
proper headers attached. 

So for that here, we have our middleware function with context and next, and
with the context object, we can get access to the response object and there we
can get access to our headers. 

And on this headers optic, there is a set method to set a new header on that
outgoing response. 

And now there are three essential headers which we should set on the outgoing
responses. 

The first header is the Access-Control-Allow-Origin header. 

This controls of whichever domains will be allowed to access our resources. 

And here we can set this to star, which means every domain is allowed to access
our resources. 

So every other domain may send the request. 

Of course, we could also restrict this to the domains we own. 

The other important header, which we need to add, the second important header,
which we set in the same way is the Access-Control-Allow-Methods header. 

This controls, which kind of HTTP methods can be used for requests being sent to
this backend and here for this API, I want to allow get, post, put, and then
also delete requests, because these are the four routes we registered. 

So here we can add, get, post, put and delete comma separated to allow for those
requests. 

Now, the last header which we need to add with headers set is the
Access-Control-Allow-Headers header. 

This allows which headers may be set by the frontend when it requests data. 

And there we should allow the content type header, why? 

Because on the front end app, so in the frontend app folder, under source
components Todos, we can see that actually for put and for post requests, we do
a set to content type two application Json, this is important because this
header on the request that's being sent to our Deno server, will tell Deno and
the Oak framework that the data attached to this request will be in the Json
format and that matters because this allows Oak on the backend to automatically
parse that when we try to get access to the request body. 

So to get to this parsing and to make sure that the incoming request data is
transformed from Json to JavaScript object for that to happen, we need to add
the content type application Json header on the request sent from the frontend,
and that end turns there for something we need to allow with the appropriate
CORS header here. 

And with all of that, we of course need to make sure that they're after the next
middleware in line is reached. 

And we do this by calling next, but again, important I mentioned it in the last
course section in the Oak framework, you should await next and there for add
async here. 

If the next middleware in line is a synchronous and our route middlewares will
be asynchronous because our route middlewares do use async keyword as well we do
have promises in there. 

So we should await for those actions to complete before the response is sent
back, and we do this by awaiting next. 

With this out of the way, we can restart our backend server by repeating does
run command. 

And if we now go back to the client site application and we reload local host
3000, you see the error here has gone. 

And if we now add Todo, learn Deno, this is being added here. 

If you click edit, it's loaded here for editing, and I can add more exclamation
marks for example and here we go. 

I can add another Todo like also learn Node and that's gonna also edit. 

And of course I can also delete a Todo, if I reload the app that also is
maintained. 

Of course, if I ever shut down the backend server, all the data is lost though,
because we currently still only save our data in memory. 

In this Todos array into Todo routes file here. 

Now that's something we'll change next. 

How about adding an actual database? 

Wouldn't that be more realistic? 

---