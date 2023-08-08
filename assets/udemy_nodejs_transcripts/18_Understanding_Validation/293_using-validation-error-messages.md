## 293. Using Validation Error Messages

<strong><em>no description</em></strong>

So we added a very basic validation and we get back a message which we want your
output. 

So this already shows us how we can work with that validation middleware, we see
it rendered that page again and now we just need to make sure we don't output
object object here but a real error message. 

We can do that in our sign up view of course, here we got our error message
thing and the error message which I am outputting here is simply an object
because it's that array and not a single field in there. 

Now we just need to adjust something and in the controller instead of returning
an array, let's say we always want to return the first error message. 

Now obviously you could change this to change the overall logic and you need to
change it in other controller actions then too to output all messages but for
now let's say we simply take the first one which we are guaranteed to have
because we'll have at least one error and then there, the message. 

And now if I save that and I do send just test again, now I get invalid value,
so this is how we could output that message. 

We cannot just output the message, we can also customize it and we have to do
that in the place where we added our middleware, so in the routes file. 

After isEmail, you can add do you with message function and this will always
refer to the validation logic that was right before it because you could add
multiple checks here, you could also add isAlphanumeric to check that it only
contains numbers and characters, number and characters, so you could add
multiple ones but with message, we'll always refer to the validation method
right in front of it and there you could add please enter a valid email,
something like that. 

And if you add this with message here, you will see that if I enter just some
text here, I get please enter a valid email. 

So this is a way of working with the messages and also of customizing it and I
also mentioned that you can add more validators. 

So let's have a look at this in the next lecture. 

---