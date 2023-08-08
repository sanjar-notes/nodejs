## 472. Testing Controllers

<strong><em>no description</em></strong>

Now, of course, there is more we could test on our off middleware, but I'd say
we tested it quite extensively thus far, and therefore I want to move on and I
want to move on to our controllers, which of course also has a lot of our core
logic there. 

We have that off controller, obviously we have that feed controller. 

Now for that feed controller, we have routes where we need to be authenticated. 

If we have a look at our routes here for getting posts, for example, we need to
be authenticated for creating posts. 

We need to be authenticated essentially for all our post related routes. 

We need to be authenticated. 

And before we take care about that, let's have a look at our off controller. 

Therefore, because these routes don't require us to be authenticated though,
does it really matter too much? 

Just the question. 

Well, let's have a look at how we reach our controller functions here, like sign
up or log in. 

We of course reached them through our routes, which are defined in the routes
folder where we send requests to in the end. 

So these are the API endpoints we're exposing here and now. 

What did I mention earlier? 

What what are we testing? 

Well, we are writing unit tests. 

We are testing units in our code just as the middleware, the off middleware. 

And therefore, what we will not test is the routing here. 

We will not test whether we can send a request to log in and we execute the log
in function in the off controller because that entire forwarding of the request,
the execution of this method here, that is all handled by express. 

And as I mentioned earlier, you don't want to test our libraries, you want to
test your own code. 

So we absolutely don't need to test this flow. 

And therefore we'll just test these controller functions we export here like the
sign up or the log in function. 

These are the things we want to test now in there. 

There, of course, again, a broad variety of things we can test. 

We can test whether we're able to extract the email and password from the
incoming request, though that's a test that's not too useful because we will
simulate the request that's coming in so we decide whether that is set or not,
but we can then test if it behaves correctly, if no email is set, for example,
or if we already have a user with that email. 

However, there is one new complexity added. 

Now we have a database. 

Now we're interacting with the user model here. 

And the user model, of course, is based on our mongoose models here. 

That's our user model and that behind the scenes uses MongoDB. 

And that of course brings one important question into the focus How can we test
our database? 

How can we handle this now? 

And turns out there are two main strategies we can follow. 

So let's have a look at both. 

Strategy number one, for a testing code that involves database operations is
that we stub or mock the parts that actually rely on database access. 

And what would this mean? 

This could mean, for example, that here when we execute find one, we again
create a step that returns a predefined result and we then test if our code
behaves correctly. 

So for example, we might be interested here in finding out how our code behaves
when find one frozen error. 

So if we're having trouble interacting with the database or how our code
behaves, if we don't have a user with that email address when logging in, these
are two different scenarios and we can write two different tests for that. 

Both scenarios should actually throw an error. 

Eventually. 

Here we throw one manually and if find one fails, it also will throw an error. 

But the status code, for example, should be different. 

The status code should be 500. 

If the database fails because we use our default code then or we set our own 401
code. 

If we have no user. 

Now to test this, I'll first of all create a new file in the test folder and I
will name this off controller JS. 

And in there, just as in the off middleware file, I'll import expect from Chae
and I'll also import sign. 

And because I will start with stubbing that post, find one method that of course
that user find one method. 

Therefore I will also import the user by requiring it from the user model file
just as I'm doing it here in the off controller there we are also importing the
user model. 

So now I want to test that log in function and since I want to tested that
function, we need to import this here as well. 

Or in general, I'll import my off controller by requiring it from the off file
in the controllers folder. 

Now let's edit this gripe block maybe where we test our off controller log in
process, because even if we're only testing the off controller in this entire
file, we might be testing different parts of that controller, like log in, sign
up and so on. 

So here I'll start with log in and then here I want to start by. 

Stopping my find one method because that is the first tactic we can apply. 

We can simply stop that a way so that we don't make a real database access. 

So here what we can do is of course I can again use sign and create a stub
created on the user object for the find one method. 

Now, if I want to force this to throw an error, I can then call user find one. 

Froze. 

Now here, this will throw an error. 

Now, by the way, of course, one issue I have here is that I'm in the described
block. 

This should go into an eight block, though, so into an actual test case. 

So here it should flow an error. 

If accessing the database fails, for example. 

So now here in that function, we define our actual test code and there we set up
that step. 

And the important thing here, of course, is I'm faking that database fail
because I completely replace the find one method with a stop that will throw an
error. 

Because the actual thing I want to check is of course that we should throw an
error with code 500. 

So I want to check whether our default status code down there really gets
applied correctly. 

Now back in the off controller. 

In the end. 

I also want to call Restore here, but in between I of course want to define my
expectation. 

And the expectation here is that for my auth controller, the login method, when
that gets called that, it actually throws an error. 

Now for that, let's have a look at the off controller again and you should now
recognize that we have the async keyword in front of that. 

It's not a normal function, it's an ace function. 

And that means in the end we use promises in there. 

You might remember async await is just a more elegant syntax for using promises.


So actually we have asynchronous code in here, which is another complexity we'll
have to deal with because the execution of that code will not happen
synchronously. 

And that means that by default our expectation won't work the way you might
expect it to work. 

---