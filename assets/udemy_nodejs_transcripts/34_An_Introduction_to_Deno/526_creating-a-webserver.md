## 526. Creating a Webserver

<strong><em>no description</em></strong>

<v Instructor>So how would the Node equivalent</v> look like for this server? 

For that, I quit the server. 

And now in app.js let's see the equivalent. 

Now to get the proper IDE completion and support I will go back to the
extensions and temporarily disable my Deno extension again. 

You might not need this, at the moment it's clashing with Node development, so I
will do this. 

And, with that done, here in app.js, I first of all will import the http core
module. 

So we're going to write some Node code. 

Now, this is what we do. 

Now, with that imported, we create a Node server by calling http.createServer
and createServer now does not want an object with a port, it just wants a
function that gets the incoming request and that gets a response object which
will be executed for every incoming request. 

So this is how we deal with incoming requests in Node world. 

We don't have a async iterator there, instead there we really just have this
callback function. 

And there we also don't send back a response by calling some response method on
the request, but instead we have this extra response argument which we get and
there we can call the end method to complete the response and send it back. 

And to end we could add our response body, for example, the Hello World (from
Node!) text. 

Now this alone will not spin up the server though, it will just create it. 

Now to spin it up we need to call listen and to listen we then pass the port
number. 

And that's our Node server. 

Now we execute app.js with Node and we don't need to specify any permissions
because, as I mentioned, Node doesn't have this permissions system. 

If we do this however, the server starts running and this process is therefore
not ending because it keeps on listening for incoming requests. 

And if I now wizard localhost 3000 I see Hello World (from Node!). 

So that is how we would spin up a server with Node. 

And it's not too far off from Deno, but of course we see core differences like
the import syntax, the fact that here we a locally available module, whereas
here we reach out to a server. 

And we then of course create a server and listen like this, instead of creating
it like this and listening automatically and then having this way of processing
requests. 

It's up to you which approach you prefer, they're both relatively short, not too
much code I would say, but this is how you would do it in Node and Deno. 

---