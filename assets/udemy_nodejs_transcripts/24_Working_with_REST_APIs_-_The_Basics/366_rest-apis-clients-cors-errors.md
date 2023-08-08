## 366. REST APIs, Clients & CORS Errors

<strong><em>no description</em></strong>

Now before I conclude this very basic starting module with rest, let me show you
something important which you need to configure on any rest API or building
which will not only be used by tools like this one or by code that runs on the
same server and I can demonstrate what I mean by going to codepen. 

In case you don't know codepen, it's basically a service which you can use for
free to write simple html, javascript and css snippets or projects, you can
share them easily with other people and we can simulate a very simple frontend
application here. 

We can create a new pen for that and here you can write as you see html, css and
javascript code. 

Now I'll not need css because I want to keep it simple and this is a great
playground here now because we can simulate a frontend app here because a
frontend app if it is a single page app will only use html, css and javascript
because we don't write any server side code in there, right. 

So in here, we might have a normal button, a button we use to send a request to
the backend, here we could get our posts and I'll copy that button and also
duplicate it to create a post and this is of course just a very basic dummy
code, we'll build a different project for the rest of this course. 

But now I have these two buttons here in my pen as you can see. 

Now let's add some javascript code to do something with them and for that, I'll
need to get access to these buttons so I'll give the first one an ID of get and
the second one an ID of post, just to keep this really simple. 

So my get button can be accessed with document get element by id and then it's
get and the second button of course is the same with post, so I'll name it post
button and I'm looking for the element with the id post. 

So I just want to get access to them so that I can register a listener, so on
the get button I can add an event listener for the click event that should in
the end make a request to my backend. 

So I'll define an anonymous arrow function here and in there, I'll use the fetch
API which is built into modern browsers with the fetch keyword where I can
define a url to which I want to send a http request and in my case that is
http://localhost8080/feed/posts, remember that is simply this route I defined
here. 

So I want to send a request to that route or to that endpoint as you learned, by
default this is a get request when using the fetch method and then we might have
either a success case which we can handle in the then block or we have an error.


If we have an error, I'll just log my error here, in the then block we actually
get back a response object where we still need to wait for the body to complete
because it will be streamed in. 

So with res json we can wait for this and then automatically convert it to json
content or to a javascript object and then we chain another then block where we
will have that javascript object because as I mentioned on the slides, json can
be converted really well to javascript and the json method does just that, the
conversion and it waits for the body to be streamed in and then I can console
log my response data here. 

Now let's open up the developer tools, clear these existing errors here which
were only created whilst I was still typing and you don't need to save anything,
it saves automatically and click get posts and you should get a no access
control allow origin headers present error. 

This is an error you see a lot when building modern web applications, modern
single page applications and it often leads to a lot of confusion. 

This error is also called a cors error and you see the word cors down there, now
what is cors and what's causing it and most importantly how can we solve it? 

Cors stands for cross origin resource sharing and by default, this is not
allowed by browsers. 

So if we have our client in the server and they run in the same domain and the
domain could be localhost 3000, important the port is part of the domain, if
they run on the same server, we can send requests and responses as we want to
without issues and that is why we had no issue before in the course. 

We rendered our html files on the server and therefore they were served by the
same server as you send your requests to so we never had any issues, so this
works. 

However if client server run on different domains like the client on localhost
4000 which is a different domain than, 3000 then we'll have issues and of course
in production, you would run on my app.com and let's say myAPI.com. 

If you send requests and responses here, you get problems, you get a cors error
because it's a security mechanism provided by the browser that you can't share
resources across domains, across servers, across origins as it's called here. 

However we can overwrite this because this mechanism makes sense for some
applications, for rest APIs, it typically does not. 

We want to allow our server to share its data, we want to offer data from our
server to different clients and these clients will often not be served by the
same server as our API runs on. 

Take Google Maps, you're not running your app on Google servers, still you can
access it and the same is true for your own API and even if you build both the
frontend and the backend, you will often serve the two ends from different
servers because you can choose a server for the frontend that's optimized for
frontend code that really serves that really well and you serve your server side
code, your node code from a different server, so you will have different
domains, different addresses there too and therefore we need to solve such a
cors error or we need to tell the browser here which runs on codepen in this
case here, we need to tell that browser that it may accept the response sent by
our server. 

And to tell the browser, we have to change something on the server and this is a
common gotcha. 

A lot of people see that error and want to solve it in their browser side
javascript code, you just can't, you can only solve that on the server. 

So if we go back to our server side code, we just need to set some special
headers, we want to set these headers on any response that leaves our server, so
the app.js file and a general middleware is a great place. 

So here before I forward the requests to my routes where I will ultimately send
the response, I want to add headers to any response. 

So I'll set up a general middleware in app.js which gets my request response
next function and there with set header, we can conveniently add a header to the
response. 

We don't send the response yet, set header does not send it, json does render
that but set header does not, set header will only modify it and add a new
header and now there are a couple of headers we need to set. 

The first one is the access-control-allow-origin, all separated with dash, so
access-control -allow-origin, that is the first header we need to set and we
want to set it to all the urls, all the domains that should be able to access
our server. 

So we could add codepen.io here but often you will just set this to start, to a
wildcard that allows access from any client. 

You could lock it down to specific domains though if you wanted to, if you have
multiple domains, you can separate them with commas but I will go with the
wildcard. 

I will also set another header and that is the access-control-allow-methods
header. 

Here we allowed a specific origin to access our content, our data, now we allow
these origins to use specific http methods because by just unlocking the
origins, it would still not work, we also need to tell the clients, the origins
which methods are allowed and there you can allow get, post, put, patch delete,
you don't have to allow them all, you can only allow what you want to be usable
from outside. 

Now there's one last header I want to set or I should set and that is
access-control-allow- and now I'm talking about the headers our clients might
set on their requests. 

There you could also use a wildcard where you can specify specific headers. 

Now there are some default headers which are always allowed but you especially
want to add the content -type header and the authorization header so that your
clients can send requests that hold extra authorization data in the header which
we'll need later and that also define the content type of the request and that
will become important soon too. 

With that added we need to do one last thing, we need to call next so that the
request can now continue and can be handled by our routes but now every response
that we send will have these headers and therefore if we save our server side
code and we restart the server therefore and we go back to codepen, if I clear
these errors and I click get posts again, now it just works as you can see
because now we set the appropriate cors headers on the server. 

---