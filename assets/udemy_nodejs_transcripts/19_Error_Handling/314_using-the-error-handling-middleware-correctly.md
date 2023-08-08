## 314. Using the Error Handling Middleware Correctly

<strong><em>no description</em></strong>

Now that we learned about this express error handling middleware which we can
use, which we added, what exactly does throw new error in this catch block, in
this middleware in the app.js file do for us? 

I mentioned that this will become important. 

Now like this, it'll unfortunately not do anything. 

Let me start up our server real quick again and let me ensure that we do get an
error by simply throwing a new error, a dummy error here, again to simply
simulate that something goes wrong. 

I throw it here, if I throw it in a then block, the next catch block will catch
it and handle it, now let's see what this does. 

Now to see the effect, I have to log in to ensure that we do get a user session
and we can already see this crashes here, it loads infinitely because I have an
error here, my dummy error. 

So this is now not doing anything, the app is still crashing. 

So one important takeaway is throwing an error here does not lead to our general
error handling middleware being called and that is important. 

This is true because we're inside some async code, we're inside a promise here,
we're inside a then or a catch block. 

If you throw errors there, you will not reach that express error handling
middleware. 

The interesting thing is if you would throw an error outside of async code, so
in a place where the code executes synchronously, so basically outside of a
promise, then catch block or outside of a callback, so here if I throw my sync
dummy like this, if we do that, so this is now throwing in a normal function,
not nested inside a promise or a callback or anything like that. 

If I now reload this, you'll see that it tried to load the 500 page but it still
failed. 

The reason for this is really simple, we have our middleware in place here where
I retrieve my user and there I throw the error but this executes for every
incoming request. 

Now when we redirect here, we do send a new request so we kind of enter an
infinite loop here, we execute this again, it throws an error, we go to the
error handling middleware, we trigger a new request. 

A solution here can be to simply not redirect to 500 but immediately execute our
rendering code, so this code in our get 500 controller action and we could
absolutely do that. 

We could render our error here instead of redirecting, we could render our page
here and if we do that, you will see that now if I reload, I just get a problem
regarding my csrf token because that can't be generated based on the incoming
request because the request basically has issues here in our middleware before
we set up the csrf token. 

So the solution for that would be to switch the order to make sure we set this
token before we actually do something with the user which we tried to fetch, so
now this works and now we get an error handling in place. 

The interesting thing is not just that we had to switch the order though and
that we should avoid infinite loops but the interesting thing here also is that
here I'm just throwing an error and we still reach this global error handling
middleware. 

The reason for that is that in synchronous places, so outside of callbacks and
promises, you throw an error and express will detect this and execute your next
error handling middleware. 

Inside of async code, so inside of then, catch or callbacks, this does not work
however. 

Inside of that, you have to use next with an error included. 

So this is then detected by express again and this is what we used in the other
files and inside of async code snippets, you need to use next wrapping that
error, outside you can just throw that error. 

And so if I now uncomment this, you will see that if I try to reload my page, I
get this error no matter what I do because I still have this dummy error being
thrown in my promise, hence the catch block executes, hence  this line executes.


So now I will get rid of that but I will leave this catch block as it is and you
have to understand that for one, you should avoid infinite loops triggered
through your error handling middleware as we had it initially here and second,
that you can throw the error in synchronous code places like this one but inside
of promise, then or catch blocks or inside of callbacks, you have to use next
around the error. 

---