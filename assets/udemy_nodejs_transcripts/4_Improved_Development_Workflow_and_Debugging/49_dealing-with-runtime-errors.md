## 49. Dealing with Runtime Errors

<strong><em>no description</em></strong>

The next category are runtime errors and a great example for this can be shown
with the res write method here. 

Now as I mentioned, you have to return here to prevent the execution of the code
after this statement otherwise and this is something node specific of course,
you would end a request here but the code execution would continue and
eventually we would reach this line and this is no syntax error, this is correct
but if we run our code here, seems to work right, there is no syntax error after
all. 

But if we now visit our page, eventually it breaks here and this is the point
where it should go back to your code and should find an error message there too.


And this error message is something you shouldn't just take and paste into the Q
& A section but actually read it. 

A lot of the error messages are indeed helpful, you just need to know how to
read them, at the bottom you always find uninteresting stuff I'd say but you
have to scroll to the top of the error message and all of a sudden, it should
get more meaningful. 

For example here, you see the error code which already indicates that it's
something with headers being sent and then here, you actually find a detailed
error message, cannot set headers after they are set to the client and then you
see that it was caused by a call to set header and unfortunately, the line
numbers don't help you, here at least but then it does help you here, you see
it's in the request handler and there it points at the routes.js file line 32. 

And now this is the point where you can dive in and see, ok I'm calling set
header here, now since it's complaining that I can't set them after they are
sent to the client, I should look well in the code before this statement because
it looks like I'm finishing my response there for this example. 

And indeed at some point you should find this statement and see I do actually
not finish my code execution after this statement which is not per se a problem
but it becomes a problem if in the following code, I then work on my response
again as I'm doing it here. 

So now this is the point where we can fix this by stopping the code execution or
by wrapping this in an extra if statement which is guaranteed to not run if we
make it into this statement. 

And now with that, we can of course restart our server or actually we don't need
to, we got nodemon now so you don't need to do that and now if you reload your
page, it will work again. 

---