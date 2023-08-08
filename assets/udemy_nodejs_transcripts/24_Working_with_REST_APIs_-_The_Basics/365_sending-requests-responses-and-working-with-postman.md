## 365. Sending Requests & Responses and Working with Postman

<strong><em>no description</em></strong>

So I defined my basic set up for a new node express rest API. 

We have a route in its controller and now of course we need to return some data
there, so instead of the controller, in get posts we want to return some data
because you learned rest APIs are all about data. 

We will not call res render in here because we will not render a view, you will
not see me call res render anymore again because rest APIs simply don't render
views because they don't return html and a rendered view is html. 

Instead we'll do something we already saw in the async request module of this
course, we will return a json response. 

Json is a method provided by expressjs that allows us to conveniently return a
response with json data, with the right headers being set and so on. 

We can pass a normal javascript object to json and it will be converted to the
json format and sent back as a response to the client who sent the request and
there, we can send anything you want, like post which could be an array of posts
where we have a title, first post and some content, this is the first post and
of course I'm just making up things here, this is of course just some dummy
data. 

So we call res json and this will send a json response. 

Now when sending json responses, we also want to send the status code
explicitly, 200 would be the default but we'll also work with different status
codes throughout this module and we want to be clear about the status code our
response has so that in the client we have an easy way of handling it because
you always have to remember that the client now has to render the user interface
based on your response and therefore especially error codes are super important
to pass back to the client so that the client can just have a look at the status
code and find out should I render my normal user interface because the requests
suceeded or did I get an error and I want to render an appropriate error
interface. 

Previously in the course we sent the whole interface so the client didn't have
to worry about that, now the client has to and therefore setting the right
status code is important. 

Now with that, we have some logic in place to return some dummy data, with npm
start we can now start up our server here and now we have it running and now we
can visit a browser and for now we can simply enter localhost 8080/feed/posts,
so this path we defined and you should get some json data here. 

If you open your developer tools and you go to the network tab in there and you
reload that page, you also see that request here and if you inspect it, you of
course see the response body but if you have a look at the headers, you see that
in the response headers we see that application json was set automatically by
our server because we used that json method and we indeed get back the content
we defined here, we can see it here too. 

So this is a quick and easy way of testing this. 

Now obviously our users would never visit it like this, they could if we don't
require authentication at least but this is of course not how we intend our API
to be used, instead we'll build a user interface that will then use this behind
the scenes and render a beautiful UI automatically with that data. 

So directly accessing the data like this is of course not the plan. 

Now before I come back to the user interface part though, let me show you how we
can easily and conveniently test our rest API even without entering this into
the browser and for that let me do something which you couldn't enter into the
browser, let's define a post route. 

So besides being able to get posts, we typically would also have some routes
that allow us to add new posts. 

Now if we quickly think about our different http methods, then for posting new
posts, post would be a great http method. 

We could also use put, that would not necessarily be wrong, put would also be a
valid method to be used for creating a resource but especially when we're
talking about posts and not something like user data which only exists once but
posts, there might be multiple posts and therefore adding or appending sounds
good to me and hence I want to use the post method instead of put. 

If we were to manage the user data here, then maybe put might be better because
there we indeed create or overwrite the resource. 

So post it is and hence I will name this post post which sounds a bit strange,
it's just my naming convention, I have the http method first and then basically
the object that's gets created. 

You could name this totally different, you could name this create post if you
want to, let's maybe name it like this because it's clearer then I have my
normal function, that of course does not change and here, we would of course
reach out to the database. 

We'll do so soon, for now I'll just note that we have to create that in the
database and I will just return the response assuming that we did create a post.


So I'll send back a json response and there we might be having a message like
posts created successfully and we send back some post data and now that is at
least data I want to parse from the incoming request. 

So I expect to get a title let's say and I still parse that on the request body,
so essentially what we always did throughout this course and I might be
extracting a content too, also from request body, just what we did throughout
the course. 

And here I return the created post with an ID that was generated automatically
let's say as mongodb does it for us, here I'm just doing it with some dummy code
and the title which I received and the content and this could just be the
confirmation that it was stored in the database successfully which of course it
wasn't thus far but which we'll add. 

Now first of all, I also want to set a special status code here with the status
method, I want to set it to 201. 

The default would be 200 and this would not be horribly wrong but 201 is the
better status code to use if you want to tell the client success a resource was
created. 

Just 200 is just success, 201 also indicates that we created a resource and of
course we did here at least in theory so manually setting this makes a lot of
sense. 

With that we're sending this success code, now what is missing? 

Well a way of parsing that data. 

I did install body parser in an earlier lecture but we also need to set it up
and now here's one important thing. 

You need to remember that we are working with incoming json data, we expect our
clients to communicate with our API, with requests that contain json data just
as we return json data. 

Json data is the data format we want to use both for requests and for responses
and therefore I will use my body parser of course, that's why I installed it, so
let's require it here in our app.js file but when I initialize it, I initialize
it differently than what we used it for in the majority of the course because
there I initialized it by calling url encoded and configuring that. 

Now this is great for data formats or for requests that hold data in the format
of xwww form url encoded, you might remember we saw that in earlier lectures
too. 

Now this is the default data that data has if submitted through a form post
request. 

We don't need that here however, we don't need form data, we have no form data
instead we want to use body parser with the json method which is able to parse
json data from incoming requests. 

So this is good for application json as is the official name that you will find
in the header and this is how the data will be appended to the request that
reaches our server. 

So we need this middleware to parse incoming json data so that we are able to
extract it on the body because that will be added by our body parser, this body
field on the incoming request. 

With that we can extract all that data but how can we now test this? 

We can't create a form in which we submit because then we would be back to xwww
form url encoded data and it would not be a realistic test because you just
don't use forms like this when working with rest APIs, instead you can use a
very handy special tool and that is postman. 

Now we will build or work with a real frontend very soon, no worries, so we'll
not be stuck to some helping tool for the rest of this course but it's still a
very useful API development tool which you should be aware of. 

It's free to use and you can simply google for it to get it from getpostman.com,
there you can just download postman and walk through the installer. 

Again you don't need to pay, you don't need to sign up, it might ask you for
that but you don't need to. 

Once you did load it, you'll end up on a starting page like this you can just
close that window and you'll then end up in a user interface like this one. 

Now you can read the official postman docs to learn about all the things you can
do but in the end what you can do is you can enter a url here, then choose your
different http methods and you see more than I showed you but you won't need
most of them, they're not required for typical crud operations. 

So you can choose your method here and then send a request, you can also add
your own headers and you will see the response in the area below this. 

So here I can send a request to localhost 8080 which is where my node server
runs on and then feed/host, this should be the route I want to reach this
controller on. 

Now for that I first of all need to create the route. 

So in my feed routes file, I'll add a post route for /posts where I use the feed
controller create post action, so this will be reached through a post request to
feed/posts. 

Let's configure such a request here, feed/posts, this is exactly where I'm
sending it to and now I just need to switch to the post method. 

Now with that switched, I also need to be able to send some data and you see
that the body tab now got enabled, with get it was disabled because get requests
can't hold a body, post requests can. 

Here you can now choose your format and we don't need any of these, instead I'll
choose raw  and then there in the dropdown, json, application json. 

So now here we can write some json data and json has a format where you have two
surrounding curly braces and then you have key value pairs where if you're
writing it manually, the keys have to be wrapped in double quotation marks. 

So here we can see what we expect to get, we expect to get a title and we expect
to get a content, so we want to pass these two fields to our server. 

So here we can pass the title and this can be my first post or actually my
second post because we use the first one as a dummy post in our get route and
then here, we have the content, this is the content of my first post or of my
second post of course. 

So this is now my request, we can now click send and we get back a response
which looks good because it's the response I defined in my controller action
with this message and the post that was created and this is now the data we
would typically use in our receiving client. 

You also see the headers that were sent on the response, these were set
automatically by express especially application json matters of course and this
is now how we can test all our endpoints because we can just enter them here and
then switch the http methods, pass any extra headers or bodies we might need and
therefore we get everything we need to test our API. 

Still we will also work with a real frontend so that we have something beautiful
to look at and to see that in a real app but this is a tool you will use a lot
when working with rest APIs. 

---