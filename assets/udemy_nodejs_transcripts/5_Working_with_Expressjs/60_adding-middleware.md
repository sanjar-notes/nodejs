## 60. Adding Middleware

<strong><em>no description</em></strong>

Expressjs is all about middleware and you see a diagram here, in the end
middleware means that an incoming request is automatically funneled through a
bunch of functions by expressjs, so instead of just having one request handler,
you will actually have a possibility of hooking in multiple functions which the
request will go through until you send a response. 

This allows you to split your code into multiple blocks or pieces instead of
having one huge function that does everything and this is the pluggable nature
of expressjs, where you can easily add other third party packages which simply
happen to give you such middleware functions that you can plug into expressjs
and add certain functionalities but more on that later. 

So this is a core concept of expressjs, the middleware and we can use that by
going here after we created the app object but before we passed it to create
server and then we can use the app and call a method which is defined by the
express framework, use. 

Use allows us to add a new middleware function, now the use method is pretty
flexible, it accepts an array of so-called request handlers here and it has some
other use cases too. 

Now one easy way of using it is that you simply pass a function to it and this
function here, this function you pass to app use will be executed for every
incoming request and this function will receive three arguments, the request and
the response object as you already know it basically with some extra tricks
learned though and a third argument which is the next argument. 

Now you can rename any of these arguments but what do they do? 

Request and response as I just mentioned are basically what you know with some
extra features. 

Next is actually a function, a function that will be passed to this function by
expressjs and this can be confusing because you are passing a function as an
argument to the use method and this function you're passing is receiving yet
another function here on the next argument and this next argument, basically
this function you're receiving here has to be executed to allow the request to
travel on to the next middleware. 

Now let me show you what I mean. 

We can simply console log in the middleware here, like this, now since I have
nodemon this automatically restarts the server and let's now go to the browser
and reload localhost 3000. 

Now actually this will keep on spinning, you see, so we don't get a response
which makes sense because we've got no logic where we would send one, in the
console here at the bottom, you see in the middleware though, so this did
execute, this is what I meant, this allows us to hook into this funnel through
which the request is sent. 

If I duplicate this and I add another use statement here in another middleware
and I save this and let it restart therefore and I now reload this page here on
localhost 3000, then I see in the middleware here again and I see it twice
because I pressed reload twice in my case here but I don't see in another
middleware. 

Now the reason for that is that we have to call next here to allow the request
to travel on to the next middleware in line. 

So it basically goes from top to bottom through that file you could say, through
all the middleware functions but only if we call next, if we don't call next it
just dies, so if we don't call next, we should actually send back a response
because otherwise the request can't continue its journey, so it will never reach
a place where we might send a response but if we also don't send one here, well
then we never send one. 

So now with this next call added, we actually make it into this middleware and
we should therefore see this console log and here we could then even send a
response. 

We'll do this as a next step because sending responses also changed a bit. 

So restarted the server, reload that page and now you see in the middleware and
in another middleware thanks to next. 

So this allows the request to continue to the next middleware in, whoops
middleware in line which is the middleware below this one. 

So this is a crucial concept, this ideas of middleware and you can use any
function that has this format, so that receives request, response and next. 

And you should call next if you want to allow the request to go to the next
function, you should send a response if you got other plans, so let's send a
response in this middleware in the next lecture. 

---