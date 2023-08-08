## 312. Using the Express.js Error Handling Middleware

<strong><em>no description</em></strong>

So we are redirecting to the 500 error page in this catch block and we can do
this in any catch block where we want to ensure that we do handle errors. 

Now the problem is we'll quickly duplicate our code a lot because we've got a
lot of catch blocks where we interact with the database and in every catch block
here, we should redirect to the 500 page, at least in a lot of them, we would
want to do that probably because for all these database failures or permission
problems, it seems to be a bigger problem so returning this page might be a good
solution. 

But replicating that code all over the place is rarely what we want to do, what
we can do instead is instead of redirecting here, we can throw a new error, this
built-in error object with the built-in throw function or keyword. 

We do that inside of the catch block, in this case here, of the post add product
action. 

So here I throw a new error and I can throw a new error with a bit more details
by first of all creating an error object with new error, I can pass my error
message like creating a product failed or something like that or simply keep
that error object which also has a message which you get returned by the catch
block here. 

So I'm creating my own object which is built up on that now and then we can also
add a new field here, http status code and set this to 500 for example

 

01:40.600 --> 01:44.320

and now here's something cool, we can return next and pass the error as an
argument to next. 

We didn't do that before right, before when we called next like in app.js here,
we simply called it without arguments to let the next middleware take over. 

Well when we call next with an error passed as an argument, then we actually let
express know that an error occurred and it will skip all other middlewares and
move right away to an error handling middleware and that's the middleware I'll
define now. 

So next error is the trick here with an error object being passed instead of
throwing it and now we can go to app.js and there at the bottom, let's add a new
middleware with app use and normally this could never be reached because we have
our catch all middleware down there but there's a special type of middleware
which we haven't seen before. 

All middlewares we added thus far, for example this get 404 action in the error
controller, all these middlewares use three arguments, request response and
next. 

Express also knows a middleware with four arguments, a so-called error handling
middleware and there, the first argument will be the error and then followed by
the other three arguments. 

Now express is clever enough to detect that this is a special kind of middleware
and it will move right away to these error handling middlewares when you call
next with an error passed to it, so it will then skip all the other middlewares
and move to that and therefore here I could now render my 500 page or simply
redirect to /500, I could do that. 

And now if I save that and I go back to my application and I try adding that
product which will still fail because I didn't fix that issue, I load my error
handling page but now with this central error handling middleware. 

Now that we added this error handling code, we can of course also repeat this in
other places and you could refactor it into one function of course which you
then just call in all these places, for example to also send an error here where
we fail to edit or load the data for editing a product. 

We can force this to fail by manually throwing a new dummy error in here, again
this is of course now kind of a set up scenario, you would never write this but
this allows you to force this to fail, it would be kind of hard to force the
database to fail right now because most of the time thankfully it works. 

But now I have this dummy error and hence if I now edit a product, I also see my
500 page because I throw this dummy error which I'll of course remove now
because it does not make any sense to add this but then we made it into catch
and there we created this error object and we called next with it and that again
will then trigger this special error handling middleware. 

Now in case you're wondering what the status code is doing here, well in this
scenario, I'm always redirecting to the 500 route here but of course we could
have a different scenario where we don't redirect here but we want to render a
page instead or we want return some json data, something we'll do later in the
course and then I would want to set my error http status code code here as a
response code. 

So this is not the solution we're using here but this is what you could do and I
just want to show that you can pass extra information with the error object so
that you can use it in this central error handler here. 

Now please note, the this error handler will not execute for 404 errors. 

There we still handle this manually because technically, the 404 error is simply
just a valid url which we catch with our catch all handler there where we then
just happen to render the 404 page, it's not a technical error object that gets
created at any point here. 

---