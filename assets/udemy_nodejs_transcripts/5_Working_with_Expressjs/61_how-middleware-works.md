## 61. How Middleware Works

<strong><em>no description</em></strong>

We added middlewares and I mentioned that this is a crucial concept of the
express framework and that we should call next if we don't send a response
because otherwise, the request will just die and will not continue to the next
middleware. 

Now in this middleware, we're not calling next and there also wouldn't be a next
middleware in line, this is our entire script right, there is nothing to come. 

Expressjs and that's important doesn't send a default response or anything like
that, so instead we should send a response here. 

So we can use the response object and now sending responses actually gets
easier, thanks to expressjs . 

Instead of setting a header which we still can do and writing which we also
still can do, so we can still send responses as before but instead of doing
this, there is a new utility function we can use, send. 

Send allows us to send well a response and actually this allows us to attach a
body which is of type any, now let me show you what this could be. 

We could send good old html code here, just h1 tag, hello from express, like
this. 

If we do that and we now reload this page here, we see hello from express, by
the way one thing you'll notice is that if you open your network tab here and
you inspect that request you got, you will see that under headers, the content
type is automatically set to text html here. 

So this is done for you, this is another feature provided by express here. 

The send method by default here since we send some text here simply sets an html
content type, you can still set one manually with set header of course, so you
can always override this expressjs default but you can also rely on the default
where the default response header is text html. 

And now with that, you see that we also get no dying request anymore because
even though we're not calling next here and we shouldn't, we're doing the
alternative, we're sending a response with send and this is of course easier
than using all these write chunks and it will be particularly easier once we
start sending back real files or the content of files, something we haven't done
at all thus far. 

Now this is something we'll also do in this module but for now, make sure you
understand this basic middleware concept, that you add functions that are hooked
into this funnel through which the request goes and you either have next to
reach the next middleware or you send a response to, well not do anything else. 

And of course if we would send a response here instead of calling next, we would
never reach that middleware, so you really just travel from middleware to
middleware, from top to bottom by calling next. 

---