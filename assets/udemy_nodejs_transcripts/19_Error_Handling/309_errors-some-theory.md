## 309. Errors - Some Theory

<strong><em>no description</em></strong>

So let's dive into throwing and handling errors and here I do have an error in
my custom validator. 

Now this will be handled behind the scenes by the express validator package, so
let's add some code that is not handled behind the scenes. 

And for that, I'll first of all take a step backward, I even quit my development
server and I'll temporarily add a new file here, errorplayground.js . 

I will remove that, it's not related to the app but there we can execute
javascript code and we can execute it with the node runtime of course and in
here, let's create a new constant, sum where I take two values, A and B, whoops,
so sum will be a constant that holds an anonymous arrow function, A and B and I
return A plus B and then now there I call sum with 1 and 2 and I console log the
result let's say. 

Now if I do this, we can execute this file with node error playground.js like
this and we get three in the console down there. 

Now that's of course nice but now let's add an error. 

Let's say I only pass one argument instead of two, now if I execute this again,
I get not a number but not an error, not a technical error object. 

Now let's say here I check if A and B, so both has to be true-ish, then I will
return A plus B otherwise I'll throw, that is a built-in keyword, a new error
and that's a built-in object node ships with where I say invalid arguments,
something like this. 

Now let's execute this file again and now we see such an error message which we
saw before in the course as well. 

Here we have our own error message and then we got a callstack which allows us
to find out at which function and which line number this error was thrown and
what was called before that error. 

We saw that before because that is an unhandled error. 

We throw an error and that is a built-in functionality, throwing such errors and
node and a lot of the packages we use also throw errors behind the scenes, for
example mongodb will throw an error if it can't connect or if an operation
fails. 

So such errors can be thrown and if we don't handle them, then our application
just crashes and that's what we saw earlier in the course too. 

You might remember cases where I did something and we got stuck and that refresh
icon in the browser kept on spinning and nothing happened, that was because our
server crashed because we had an error which we did not handle. 

Now how can we handle errors? 

Well one solution for synchronous code, so code that executes line by line
immediately and does not wait for anything, so for example where we don't
interact with files or where we don't send requests, well such code can be
wrapped with try catch, another built-in language feature. 

We try a certain code and then we have to add catch where we catch a potential
error that might have been thrown and in catch we can now handle it, for example
here I could output error occured and then I console log my error like this. 

Now if I re-execute myerrorplayground.js file, I still get this error here but I
get this additional error occured message and if I not log my error object here
and I execute this, then I actually get just this, so then it does not crash and
log it automatically but we could do anything we want. 

We could continue with other code after this, so here I could have this works. 

I could execute this line and we see this works being output here. 

Just to demonstrate this, if I comment out try catch and I just try to console
log someone, so I call this with an error being thrown, then we don't see this
works anywhere because it crashes with our error that is being thrown and it
does not continue with other code. 

So this is why handling code like this is a good thing to do because this
ensures that we can continue with code, that we can handle this gracefully, in
our node express application we could send an error response here which renders
a valid page without crashing everything but which informs the user that
something bad happened and in the end, this is what the express validator
package does for us with our thrown error. 

In auth.js where I throw this error, in the end express validator catches this
and then just adds it to its own error array and allows us to read that list of
errors it caught, so that is what happens behind the scenes you could say. 

Now here we have a look at an error and synchronous code throwing an error which
we can handle with try catch. 

Now we also have async operations that can fail of course and such operations
when using promises are handled with then and catch and that is what we can see
a lot in our code. 

Here where I do something, where I find a user, I have my then block where I
handle the case that the database operation succeeded,  then I here still have
my custom case to see if we did get a user because the database operation can
succeed even without retrieving a user but I then also have a catch block here
where I catch any errors that happened. 

So here for example that would be the catch block related to my find one method.


So if the database operation fails because we don't have read access because the
database server is down temporarily, anything like that, then we make it into
this catch block. 

So this is try catch, just with async code you could say, then is your success
case and catch allows you to execute code if that fails. 

Catch by the way collects all errors that are thrown by any prior then blocks,
so if we had more than then block in our chain here, catch would fire on any
error thrown in any then block or any operation executed in a then block, that's
just a side note. 

So this is how we can work with errors, how we can handle them. 

I'll now get rid of the playground file, you find it attached to the video if
you want to explore it a bit more, let's now see in our application how we can
improve error handling. 

---