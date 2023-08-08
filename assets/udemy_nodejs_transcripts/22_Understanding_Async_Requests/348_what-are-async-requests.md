## 348. What are Async Requests?

<strong><em>no description</em></strong>

So what are asynchronous requests? 

Well we have our client and our server, so the browser and our node application
and that's the setup we had for this entire course, this is the set up you have
with any web or even mobile project that you build these days. 

You have your backend, you have your frontend. 

Now typically, you send a request from your client to the server and you get
back a response and as I mentioned, thus far in this course, the response always
was a html page or a redirect to another route that then returned a html page. 

Now there is nothing wrong with that but there are tasks where you don't want to
reload the page just to for example delete an item and actually in modern web
applications, the portion that happens behind the scenes grows since we can do a
lot with javascript in the browser where we never need to fetch a new html page
but where we constantly change the existing page as this is faster than loading
a new one but that's something I'll cover in the restful API modules. 

Now the idea behind asynchronous requests is that you do send the request but
that request typically contains just some data in a special format named json
and that data is sent to the server, to a certain url or a route accepted by
that server, so that logic doesn't change. 

The server can do whatever it wants to do with that and then we return a
response and that response is also returned behind the scenes, so it's not a new
html page that needs to be rendered, it's instead again just some data in that
json format typically. 

And that is how client server can communicate through javascript, so through
client side javascript and the server side logic without reloading or rebuilding
the page, without exchanging a new html page. 

And that allows you to do some work behind the scenes without interrupting the
user flow, without reloading the page. 

Now let's have a look at how that would work in this module. 

---