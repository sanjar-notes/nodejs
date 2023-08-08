## 351. Sending & Handling Background Requests

<strong><em>no description</em></strong>

We have some basic code in place to extract values about the product which we
want to delete, now to continue, we need a route on the backend to which we can
send our javascript request. 

For that let's go to the routes folder and there to admin.js. 

Obviously we already have a delete route here, a delete product route and we can
build up on that route, there is nothing wrong with that but now since we'll
send the request directly through javascript, we can actually use a different
http verb. 

Thus far we always use get and post because the browser natively supports these
for the requests sent by the browser, by form submission and by clicking links,
it only knows get and post. 

When we send requests through javascript, so through browser side javascript, we
have access to other http verbs too and you'll learn more about the different
http verbs in the rest API section. 

One of them is delete and this is a http verb, so http method which makes a lot
of sense for deleting. 

Now it's only a semantic thing, we could use post, you can in general use any
http verb to do anything because you define with your server side logic what
will happen but it makes sense to try to be clear about your intention and there
is a delete verb, we can now use it so why wouldn't we use it. 

So now this is a delete route to delete product, now I can also change this a
bit and may be name this product- and then the product ID as a dynamic parameter
because delete requests can have dynamic url parameters. 

So now we can extract that information from our url and I'll leave the
controller action as it is but I will now name it delete product like this
because we are not sending a post request anymore so I guess this name makes
more sense, isAuth is a middleware I will keep in place though. 

So now with that, let's go to the admin controller and here, I'll rename that
function, that handler here to

 

02:10.460 --> 02:15.920

delete product because I renamed it in the routes file too and now the product
ID first of all is not extracted from the request body anymore because delete
request as it turns out also are not allowed to have a request body  but
instead, we now have that url parameter product ID, so I can extract my ID from
there. 

So I simply change body for params and that's it, so that gives me my product
ID. 

And then this logic here will still work, I only need to change the response
I'll return. 

I will not redirect anymore because I'll not load a new page. 

Remember that the request triggering this action will be sent behind the scenes
for the existing page, so I want to keep that existing page and therefore my
response will be a response where I send json data. 

Json data is a special format and with expressjs, I can use a json helper method
to conveniently return json data and json is simply a data format that looks
like a javascript object, so with curly braces and then key value pairs, the
only important thing about json is the keys have to be wrapped between double
quotation marks. 

This is json data and this is what we can return here and now we can also set a
status here of 200 maybe because for json data, this would be the default too
but there since we don't redirect it and so on, where we get a status code set
automatically, it would make sense to be very clear about the status code we
have. 

And therefore here, I'll also not to use my default error handler where I would
load the 500 page, instead here, I'll also return a response with status 500
now, that is what I mean about setting that status on your own and there, I'll
also return some json data, the question is of course which data. 

You simply pass a javascript object here which will then be transformed to json
automatically for you. 

So here you can pass your normal javascript object, you don't need double
quotation marks around your keys there and here we could have a message where I
just say success, of course not that interesting but we could do that. 

And here I could have a message where I say deleting product failed. 

So now I have that in place and now we have two important changes, this is how
we extract the params or the product ID and now we return json responses because
we don't want to render a new page, we just want to return some data. 

Obviously we now have to continue in admin.js and make sure that we send the
request and then work with the response data. 

Whoops, not this file though, I mean the one in the public.js folder, here. 

We worked on the server side and we added a new route or we changed the route to
use the delete http verb and to look like this and now we need to send the
request there from inside our client side admin.js file, so in the public
folder. 

Here we can use the fetch method which is a method supported by the browser for
sending http requests and it's not just for fetching data as the name might
suggest, it's also for sending data. 

Here if you can pass a url, so we want to send a request to /product and then
this of course needs to be replaced with the Product ID and this will send that
to the same server if you don't specify a different host with http and then
something, so if you have nothing like that, it will send it to the current
host. 

Here I will add my prod ID of course and then the second argument is an object
where you can configure this fetch request. 

Now here you can set a bunch of things, you could add a request body but not for
a delete request as I just explained in the last lecture but for a post request
which you can also send with that, you would set it and first of all let's
define that this is a delete request. 

So I'll set method to delete here, doesn't have to be uppercase but it's a good
convention. 

Now with method set, what else can we set? 

Well we can set headers and in the headers, we could encode our csrf token
because we still need to attach this to our request and right now we are not
doing that. 

We cannot send it in the request body because delete requests don't have a body
but the good thing is the csurf package which we are using on a server does not
just look into request bodies, it also looks into the query parameters and
therefore we could add it there and it also looks into the headers. 

So there we can add a csrf token header, it will look for this key, you'll find
all the keys for which it will look in the official doc. 

So you can add csrf token and then csrf as a value to attach this to your
outgoing request as well. 

Now this will send the request and it will return a promise that allows to
listen to the response and here I will console log any error I might be getting
and here, I'll be console logging any result I might be getting, let's see what
we have there. 

Now one important note by the way, I'm not sending any json data with my request
here because it is a delete request without a post body. 

If it were and that is something we will see in the rest API section, then I
would have to parse json data in my backend because there right now and that's
just an important note, in app.js, there right now we only have two parsers, one
for url encoded data which we don't have when we send json data and one for
multipart data which we also don't have there. 

We would have to add a new body parser that is able to handle json data and
extract that from incoming requests. 

I don't add it here because we don't need it here but we will add it later when
we need it. 

So with that all in place, with our client side code adjusted, let's save all of
that and let's simply click the delete button after reloading the page and see
what we get. 

Let's click delete and I first of all get a 404 error that this route is not
found, product with some ID and this makes sense because my route, product
product ID is in the admin routes folder, of course we only get there if our
request path starts with /admin, that is what we configure in the app.js file. 

So in my client side admin.js file in the public folder, I should of course
point at /admin /product/product ID, so that's a little mistake on my side. 

Let's now reload after changing this and now this is looking good, I get a
response with a status code of 200, with request body which is a readable
stream, I'll show you how to get to that request body in a second and if I
reload the page, the product is indeed gone. 

Now that's a step forward but of course I don't just want to reload the page, it
should be gone immediately, that would be the main idea of doing this behind the
scenes. 

So how can we make this work? 

---