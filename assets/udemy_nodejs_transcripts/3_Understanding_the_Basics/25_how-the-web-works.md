## 25. How The Web Works

<strong><em>no description</em></strong>

So let me quickly refresh our knowledge on how the web works. 

If you are totally aware of all of this, you can of course skip this lecture. 

Now the web works like this, we get got a user, a client, maybe you sitting in
front of your browser, visiting a webpage or already being on a webpage and
submitting a form, so you're interacting with webpages. 

Let's say you are visiting it, so you're entering some url into your browser and
what happens behind the scenes is actually that the browser reaches out to some
domain name servers to look that domain up because this domain is not really the
address of your server, it's basically an encoded human readable version of that
address you could say, your server itself has just an IP address but this is
just some technical thing behind the scenes, in the end you enter this url and
it will lead to some server. 

You therefore or the browser therefore sends a request to that server with that
given IP address I mentioned, so the IP address belonging to that domain. 

Now thus far that's all interesting but now we reach the part where nodejs comes
into play, where your nodejs code matters. 

You write the code that runs on that computer in the Internet which has that IP
address, you write the code that spins up that server which is able to handle
the incoming request and do something with it. 

Now you don't need to use nodejs for this, you could use PHP, asp.net, Ruby on
Rails, anything like that but in this course, we'll obviously use nodejs because
well it's a nodejs course. 

Now in this code, you can do all kinds of things and I already mentioned this in
the first course module, user input validation, communicating with the database
maybe which runs on a separate database server but which you typically reach out
to from your backend, so your server side code and once you're done with that,
you do one important thing, you send back a response to the client. 

This response can be some html text, some html code which is then handled by the
client but it could also be some other kind of data like a file, some json or
xml data. 

The response is more than just the content by the way, a response and also a
request also has headers, this is some meta information which is attached to
request and response describing what's inside it for example but we'll see this
too. 

So this is how the web generally works and nodejs is the part we will focus on,
it is the code that makes up that server in the end. 

Now that request and response transmission is done through some protocol, so
basically a standardized way of communicating you could say because obviously,
to correctly handle a request and send back a response the browser can work
with, we have to follow some rules and these rules are defined by the protocol
we use, http or https. 

Http stands for hypertext transfer protocol and there we simply define or it is
defined how a valid request looks like and how the data should be transferred
from browser to server and the other way around and https simply is the same
with SSL encryption turned on where all the data that is transmitted is actually
encrypted so that if anyone is spoofing your connection, they can't read your
data. 

Now towards the end of the course, I will show you how to enable https, for the
majority we'll just use http since we'll only be developing that code, we'll
only work on it locally but once we put it into production, I will also show you
how to turn on that SSL encryption. 

This is how the web works in a nutshell and how nodejs is related to it and this
is exactly where we will now continue working with nodejs and where we will now
finally create a server with nodejs. 

---