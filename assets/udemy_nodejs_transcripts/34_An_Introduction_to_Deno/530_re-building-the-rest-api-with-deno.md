## 530. Re-building the REST API with Deno

<strong><em>no description</em></strong>

<v ->So let's now rewrite this with Deno.</v> For that, I enabled my Deno
extension again to get a better IDE support. 

And now in the Deno folder, I'm going to add my app.ts file ts because we're
going to use typescript. 

I'm going to add a routes file, and in there my todos.ts file. 

So really the same structure as in the Node case, just now with typescript and
Deno. 

Now, one key difference will be that now, we don't need to run npm in it, and we
won't need to install any third-party packages or modules because with Deno we
use these import syntax as you learned. 

So we can actually copy the code from the old apt.ss file, which sets up a basic
Oak application, and we can copy that into apt.ss here. 

Note there, I do register a middleware, and that middleware sends back a
response, but I'll get rid of that. 

I'll actually comment out the entire middleware for now. 

Because, whilst, listening here is fine, and I wanna listen on port 3000
actually, so change this, Whilst that is fine, I of course, want to handle my
request in the routes file. 

Now for that, we can import something from that Oak module. 

If I copy the import path, the import statement over to todos.ts, we cannot just
import application from there, but also a router. 

So that's quite similar to Express, we can also set up a router with the Oak
framework. 

We can instantiate our router like this, and then on the router, indeed we also
have GETs, and PUT and POST message available. 

So that's very similar to Express, while migrating from Node to Deno isn't too
hard. 

You see it here. 

So we can just also register GET route, like this, by specifying a path for the
get('/'). 

and then the second argument should be your middleware function, and there a key
difference is that you don't get request/response and next, but that you get a
context object and then, optionally, all your next function. 

But here we just need to context, because the context will give us access to
both the request and to the response. 

And now we can replicate this '/todos' of course, all the forward posting, but
then also with a replicate this two more times for a putting. 

And you can also specify dynamic segments, just as you do it with Express, with
a colon and then any name of your choice. 

So that works just like it does in Express. 

So it's really not too hard to get used to that. 

And in the end, we export it, but now here with typescript and Deno, not with
Node's module system, but instead with the ES module system, which you all have
learned about in the modern Java Script for the Node JS section in this course. 

Here we can set up a default export, and export our router like that. 

And this allows us to go to app.ts, and here we now import our own file all the
with import from, but of course now, not from a url but from ./routes/todos. 

Here, however, always with the file extension. 

You must not omit it when working with Deno, that is an important difference to
Node. 

And now here we have a default export, so when we import it, we can just name
this todosRoutes, if you want to, and now we can register this. 

However, that's another difference to Express, not just like this, instead
todosRoutes now is an object, which has a routes method, which we need to call,
and that's the actual middleware we then register. 

And there is a second middleware we should register, and that's
todosRoutes.allowedMethods. 

You should register both to make sure that Oak properly handles incoming
requests to your routes. 

With that however, this routes should be reached by incoming requests, and
besides these tiny differences, which I highlighted, it really doesn't look too
different when we compare it to the Node Express code. 

Does it? 

Well, let's add some logic here now. 

We have our todos and that should be an array, but since we used typescripts
here we can and we should be more specific regarding the kinds of data that end
up in this array. 

I also do talk about this in the typescript section of this course. 

So we can assign a type to todos here, and make it clear that in there we want
to have an array of specific kinds of objects. 

And for that I'll define a so called interface here and I could do this in a
separate model, file or anything like that, but I'll do it in line here. 

And I'll name this todo, and a todo will have an id which is a string, and a
text which is a string. 

This is how you define the type of an object in typescript, and how you make it
clear how data of type todo should be structured. 

We can now use this type here to make it clear that this should be an array full
of todo elements, full of todo objects. 

This is typescript syntax for a saying that this should be an array full of
todos. 

So full of objects that each have an id field which holds a string, and a text
field that holds a string. 

Well, and now we wanna send back a response here for the GET request. 

We do that by calling the response object, or by reaching out to the response
object on the response property. 

And we can simply set the body to something, we can set the body to an object,
where we have a todo is field which holds our todos. 

Now with Express, we always have to call JSON, to attach some JSON data, to tell
Express that what we attached should be handled as JSON data and to basically
also tell Express to send back a response. 

With the Oak framework, with the Oak module, it is a bit different. 

We just set the response body, and if we set it to an object, Oak will assume
that this should be added as JSON. 

So it'll automatically parse it as JSON or transform it to JSON, I should say,
and set the appropriate response headers. 

Oak will also always send back a response, so therefore, here we just have to
set a body for that automatically send back response. 

So that's all we need to do in Oak to send back our todos. 

Now, before continuing, we can test this by saving all the code, and then we can
navigate into the Deno folder, and now Deno run with --allow <v ->net</v>
app.ts, this compiles the code and springs up the web server, and if we now go
back to Postman, and we try sending a GET request to localhost:3000/todos you
see we get a 200 response with an empty array of todos. 

So that route is reached and that clearly works. 

Now, what about the other routes? 

How do we implement this with Oak? 

Well, for the other routes, let's continue with posting. 

I want to create a new todo, and that should be of type todo. 

So here I'm assigning the todo type, so that typescript basically complains when
I try to assign anything that does not meet this object type. 

That's why currently, for example, it's giving me an error here because an empty
object it's clearly not following that structure. 

Now we can add id for, again, I'll just generate a new Date to ISOString here,
and set the text to the text we get from the incoming request. 

And now here is an important feature built into Oak, it'll automatically look at
the request, at the request body, and all the request headers, and if the
request signals that the request carries JSON data, by setting the appropriate
request headers, then Oak will automatically parse that body and gives access to
the parsed body on the context request body field here. 

However, body now is not an object with the parsed body like this, instead, body
actually gives me a promise now. 

So therefore, we can now get our data by reaching out to ctx.request.body and
now we can use async await, for that we need to convert this into async function
though, then we can use await here and we get the ctx.request.body data at this
point. 

And body is a method we should execute though. 

And now on data, we actually have a value property and that's then the actual
parsed object, so that's what we then find the text property, if we expect to
get a text key on the incoming JSON data, which we can read and use. 

So extracting the body is a little bit different, but generally, the Oak
framework does it for us, we then we just have to access the extracted data like
that. 

And once we get that, we can reach out to our todos, and push the new todo onto
that array. 

And then often we can set the response body, of course, for example, to an
object where we have a message key of created todo, and where we add the new
todo that was created. 

And if we now save it, quit that server and rerun this server by repeating that
command, if we now go to the POST route, send the request, a POST request to
localhost:3000/todos with this given body, you see we get back to success
message. 

And if I now GET all todos again, we see the todo here as well. 

So that works. 

Now let's work on putting and deleting. 

Now, let's work on PUT. 

And here we have to extract data from the params, for that on this context
object which holds request and response, we also have a params object, and
params, in the end, gives us access to route parameters. 

Here we can simply access todo id like this, and store it in a concept. 

This gives us access to the todo id from the incoming request url. 

Again the key name you choose here, of course, has to match the name we have
here. 

Now, we can find the appropriate todo index, and we can actually copy that
updating code from the Node Express port function. 

We can copy this code, these lines of code here, over into this file, because
it's exactly the same logic. 

The only part that differs is the request body, there we should parse it just as
we do it in the POST route, with this line here. 

And, of course, for that we should turn this into async function. 

And then we extract the text also like we do it in the post route with
data.value.text. 

With that we update our todo DAO, and then we can send back our response, by
setting the body equal to an object where the message could updated todo, like
that. 

And if we now save this and restart the server again, our old todos will be
lost, because it's only stored in memory, so let's first of all create a new
todo, let's then grab the id of this new todo, and go to the PUT route and plug
that id into the url, keep the body as it is and send this request and I get
back updated todo here. 

And if I get all todos, I see that one todo with the updated text indeed. 

So this also works. 

Last but not least, for deleting, here we also need the todo id, which we
extract just as we're doing it for the PUT route. 

And then the logic again is the same as in the Node Express case, I'll copy that
line where we filter our todos, copy that over into this DELETE route and then
just set a response body where I say 'Deleted todo'. 

Now before we rerun this, there is also on other thing I wanna show you because
that can be tricky, and that's another difference between Oak and Node Express. 

In app.ts if you also want to run other middleware, like this one here, we can,
of course, console log middleware, but, of course, just as in Node Express, we
need to let Oak know that we want to continue thereafter. 

Therefore, we get a next function and we can call this next function, but now
here is the tricky thing, I mentioned that Oak always automatically sends back a
response, it basically does so whenever it's done executing a middleware, any
middleware. 

Not all middlewares, that's a key difference. 

So when this middleware is done, it'll send back a response, now because we're
calling next, you might think that this middleware is only done once these route
middlewares also ran. 

Well, we start running these middlewares, these route middlewares, with next,
but with next we don't wait for that. 

Now in the route middleware, were doing some async stuff view. 

We got the async keyword because we're parsing request bodies, for example. 

So our route middlewares, actually, will return promises which only are done
once the async stuff in there finish. 

And next will not wait for that, therefore, at the moment, we would actually
have the scenario where we often send back a response too early, before the
route has been able to process the request. 

Therefore, whenever you have any middlewares that do async stuff, you should
make all your middlewares async and always await next. 

So this tells Oak that we don't just want to start the next middlewares in line,
but that we also want to wait for them to finish before we send back that
automatically generated response. 

Otherwise, the response bodies set by our async route middlewares, will not be
taken into account. 

That's a gotcha of Oak, and therefore, something you should be aware of. 

With that change made, however, now to restart, we also have to done the
middleware, and we have to delete routes, and now with that, if we go for the
routes again, and I create a new todo, I copy that url, and I try updating it,
that seems to work. 

If I get my todos, you see the one updated todo there and if I now delete that
todo by sending a delete request to the route with this correct id, if I send
this, this also works. 

We see the todos are gone now, and we see the middleware log all the work. 

And that's how we can build the same kind of application with Deno and Oak. 

Now it's time for a final comparison, and also, probably, for a judgment from my
side. 

Whether Deno is better, whether you should switch, of if Node is everything you
need. 

---