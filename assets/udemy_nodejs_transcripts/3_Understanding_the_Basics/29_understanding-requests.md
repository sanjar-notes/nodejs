## 29. Understanding Requests

<strong><em>no description</em></strong>

So let's go back to the request object we logged here. 

Now important just to keep that in mind, this request object is the object
nodejs generated for us with all the data of the incoming request when we
visited localhost 3000 which we in turn can do because we listen to requests on
that port. 

So this is the request object, if we have a look at it, we see it's a very
complex object. 

There's lots of data in it, it's not just data, these are also partly functions
we can call and so on, so this is quite a complex object but we also see that
for example we have some headers here. 

Headers as I mentioned earlier are metadata, meta information added to a request
and also to responses by the way and there we see for example the host, this was
sent too, the request was sent too. 

We saw some headers attached by the browser like for example how the response
data should be cached and stuff like that, which browser we used for that
request, which kind of response we would accept, that we accept some html, xml
and so on, that we would accept encoded responses, so where the response is
actually minified to well save bandwidth and so on. 

There also was a cookie attached even, we haven't learned about cookies yet,
we'll do so later but this was attached at some Google Analytics cookie. 

We saw which http version was used and so on, so there's a lot we can gain from
that request but a bit too much. 

Now there are only a few important fields you typically need. 

The first important or interesting field is the url, now let's output that and
let's also output, you can output more than one value by separating them with
commas, request method and also request headers here. 

Let's output these three values and restart the server with node app.js, so now
it's again listening and let's reload that page on localhost 3000. 

If we do so, now we see the output has changed, we still have all the header
stuff because we're outputting request headers but prior to that, we output the
method which you see here, it's get and you see the url and the url is just the
slash here because the url is basically everything after our host and we just
have localhost, well nothing and that basically translates to localhost slash. 

If I had /test, now we see another output and there we see /test being logged
here and then also get for the method and our headers. 

So this is basically how we can access some information about our request. 

Now one crucial thing that is missing here is the response, so let's have a look
at sending responses in the next lecture. 

---