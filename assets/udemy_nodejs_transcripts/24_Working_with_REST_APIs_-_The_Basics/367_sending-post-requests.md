## 367. Sending POST Requests

<strong><em>no description</em></strong>

Now we learned about cors in the last lecture, now let me show you how it
affects our post requests. 

So I'll use my post button to also add an event listener there, click like this
and in there I'll also use the fetch method to send a fetch request to the same
url as before but it ends with /posts because I'm targeting this url here which
is just post, not posts. 

So if you name this differently, you should of course use your path. 

Here since it will be a post request, I need to pass a javascript object as a
second argument which allows me to set some options. 

Specifically I want to set the method to post here to send a post request and
then I will copy that code from up there for handling the response so that I
can, well extract the data or log a potential error. 

If I now clear that and I hit create post, I get post created successfully but
if we inspect the post object, we see that the title and content are missing. 

Now that makes a lot of sense because we didn't send that data. 

Instead on the post request in the client, we also want to set a body object and
that object will hold the title, a codepen post and content created via codepen,
whatever you want. 

If I clear that and now I click that button again, hmm I still don't see that
here. 

Now on the server side, nothing goes wrong here but actually on the server side,
if I would go to my controller and I would log title and content here or use the
node debugger to see their values, if we log that and I click create post, then
we see that undefined gets logged here. 

So we are not able to extract that data and the reason for that can be found if
we go to the network tab and have a look at this post request that was sent,
there in the request headers, we see that the content type was text plain and
that is the problem. 

It should be application json but we also see that the request payload was not
json data which in the end is just text but in a special format but that it was
a javascript object which just can't be sent or which can't be handled. 

So there are two things we need to do. 

First of all on the body, I will call json stringify which is a method provided
by default by javascript, it will take a javascript object and convert it to
json. 

We can see that immediately if I click create post again and we inspect that
request, the payload now is indeed text in the json format but we need to tell
the server that our content type is of type application json and therefore
besides setting the body, on the client I'll also add headers or one header, the
content type header, content-type which is application/json. 

And now with that, if I click create post again, now in the created post we see
title or title and content because now that data is sent and extracted correctly
because we send it in the right format and we inform the server about the
content type. 

Now this also allows me to demonstrate what happens if I would comment out this
header here, the access control allow headers header on the server side. 

If I save after commenting this out and I try to create a post again, I fail
because I'm not allowed to set content-type, I do allow this by adding this
header on the server side. 

So this is how you communicate between client and server, of course the client
code differs depending on the client you're using. 

This is javascript code using the fetch API, there are different ways of sending
asynchronous requests, for example you can send Ajax requests through libraries
like axios and if you are building a mobile app, you might have a totally
different object or helper methods for sending such requests in Android, in
swift and so on. 

So this client code differs, this is the javascript code using the fetch API,
the server side code does not really differ. 

You want to make sure your clients can communicate and that everything works
just fine there. 

Now before I conclude this though, one more word about the post request we're
sending with this click. 

You might see that I actually have two requests being sent, the second one is
our post request, what is the first request? 

If you have a look at it and we see the response is just post, ok, the headers
are interesting though. 

We can see that in the general part, the method here is options and that is this
last method I showed on the slide earlier. 

I mentioned it would be sent automatically by the browser and also for example
by many mobile app clients. 

What is the idea behind options? 

The browser simply goes ahead and checks whether the request you plan to send
which is a post request, that is why here in the request headers which are
generated automatically by the browser, it checks for the post request, it
checks if that will be allowed otherwise it will throw an error. 

This is simply a mechanism the browser and many other clients use and there is
not too much you need you to do to make this work, it just works out of the box,
you just want to make sure that you set the right cors headers here. 

You can add options to the allowed methods but as you see, it was able to make
this request before, this is not really something you need to do but you can do
it but the important thing is that you are not confused by that extra request. 

It's simply a mechanism the browser uses to see if the next request which it
wants to view, the post request will succeed if it is allowed. 

And this is all I want to tell you about cors and client server communication
for now. 

---