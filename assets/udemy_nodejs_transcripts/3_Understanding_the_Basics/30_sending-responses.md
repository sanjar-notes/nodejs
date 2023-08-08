## 30. Sending Responses

<strong><em>no description</em></strong>

In the last lecture you saw how to handle requests and how to read some data
from the requests like for example the url and which http method we used. 

Now we'll learn about different http methods throughout the course, by the way
get is default method used if you just enter a url into your browser. 

Let's now shrink this again, let's quit the server, you always need to quit and
restart if you edit it because otherwise your changes will not be reflected
because the old process will still be running and let's now also use that
response object. 

Now we could log that with the console but actually this does not hold any
interesting data, instead we can use it to fill it with data we want to send
back. 

We do this by calling res and now what? 

There are a couple of methods we can use, for example set header, this allows us
to set a new header. 

For example content-type and that is a default header which the browser knows
and understands and accepts and then as a second value here, as a second
argument, in set header, we set a value for this header key, and we can send
this to or set this to text.html . 

Now what this will do is it will attach a header to our response where we
basically pass some meta information saying that the type of the content which
will also be part of the response is html. 

Now there is of course only a certain set of supported headers the browser
understands and after this lecture, you'll find another lecture with some link
where you can learn which headers you can set. 

Now you don't need to set that many, let me say that and later we will even
learn about a package that does this for us so that we don't have to set the
content type on our own. 

But here I will set it, now one important thing is missing of course and that is
the html code, right. 

Thus far I'm saying we have html code but I'm not sending it. 

Now we do this by setting response and now we can set write here, write allows
us to write some data to the response and this basically works in chunks you
could say or in multiple lines, this would be a good picture to look at this,
you write multiple lines of response. 

For example if we write html code like this, res write and if this looks super
strange now, it is, we'll learn about a way easier way of sending html later, no
worries. 

So here I'm just sending html and you can also put longer html in there, of
course you could now have your head where you set the title, my first page like
this and you could put even more into that line but to make it easier to read
I'll write a new line where I now have my body. 

So I'm basically writing a whole html document here in a very complex way and
there I'll just add a h1 tag saying hello from my nodejs server. 

Ok so this is now some html code and it will be written to the response line by
line. 

We now also need to tell node once we're done with creating that response and we
do this by calling end, so after we set all the headers and wrote all the data
to the response body, we call end and now is the point where we must not write
anymore. 

We can still call write but this will result in an error because we must not
change the response after we ended it because this is basically the part where
we will send it back to the client, nodejs will send it back to the client. 

So here it should send back a response with some html code inside of it where we
also tell the browser that it's html code, the browser wouldn't know otherwise. 

And with that if we save that file, make sure you never forget to save your
changes and we re-execute it, we again have that running process and now if I
reload my localhost 3000 page here, we see hello from my nodejs server. 

And if I open the chrome developer tools here which you can also do from the
menu, I use the shortcut, you can also use view developer, developer tools or
that shortcut you see here. 

Now if you do that, let we reload, in the network tab here you will see this
request, this first request and there you see headers, like for example in
response headers, there you see my content type which I set right, this is the
header we set here and if we click on response itself to see the response body,
we see that html document code we wrote with the head section, with my first
page and so on. 

So this is now how we can send a response, we'll later also learn about a way
simpler way of doing that by using the expressjs framework but it's super
important that you understand all the nitty gritty details that go on behind the
scenes and in this case, we simply understand it by writing all the nitty gritty
code on our own business. 

This is how we can work with requests and send responses, now let's connect both
the request data we can get and the response data we can send. 

---