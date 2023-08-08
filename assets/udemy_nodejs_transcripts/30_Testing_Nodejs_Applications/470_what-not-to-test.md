## 470. What Not To Test!

<strong><em>no description</em></strong>

Before we actually move on to the controllers let's now test something more
complex here in our is off middleware. 

Thus far we tested whether we have a valid header and that we get an error if we
don't. 

So if we have no header at all or if it's not applicable, that is all nice. 

But what about our actual token verification now? 

How could we test this? 

How can we make sure that this fails for incorrect tokens? 

Well, there are a couple of important things to consider. 

First of all, now this is really something you have to memorize. 

You should not test whether the verify function works correctly. 

You should not test whether this really verifies a token correctly. 

So whether it is really fails for incorrect tokens that were not created with
that secret. 

Why should you not test for that? 

Because this is not a function or a method owned by you. 

This is coming from a third party package, from the JSON web token package, and
it's the job of the package offers to test their own code and to make sure it
works correctly. 

So you don't want to test external dependencies. 

You don't want to test if verify works correctly or if it has bugs. 

Of course it could have. 

But it's not your job to test this as part of your application. 

If you want to get involved with the development of this package, you can
absolutely do so in that package, but not in your application. 

So therefore, we're not testing whether Verify works correctly. 

We only want to test if our code behaves correctly when verification fails, for
example, or when it succeeds. 

So when we don't get back an object that has a user ID, for example, which we
actually do get back, right. 

We get back decoded token with the user ID. 

Well, we only get this if this does not fail. 

So we don't want to test if verification works correctly, we want to test if our
code then behaves correctly, depending on what verify does. 

This introduces one new problem, though. 

Verify, of course, comes from a third party package and therefore it does its
job. 

And now if we want to test, if our code works correctly, it's easy to test for a
failure. 

We can easily pass on a token that's not verified by this package because we
don't actually know which tokens it creates for us. 

You might remember tokens are these super long strings. 

We can't guess them. 

So whatever we pass into our function here, we'll probably fail here in the
verification step. 

And indeed, let's actually start with such a test. 

It should throw an error if the token. 

Cannot be verified. 

Let's add our function definition here. 

And now again, let's create a dummy request object for this test. 

Here I have barer. 

And then x, y, z and x, y, z is the token that will actually be used. 

And it certainly will be an incorrect token, certainly not a token created by
the JWT package. 

And therefore now if I expect my middleware. 

With my request object, empty response object and this empty next function. 

If I expect this to flow, then this test should absolutely succeed. 

It should pass because this will throw an error. 

And indeed it does. 

Of course, if we wanted to test the opposite. 

So if we add yet another test. 

Where we want to check. 

Well, if this is a valid token, then decode it token. 

So this object that returns us should have a user ID. 

Well, if we test this, it should. 

Yield a user ID after decoding the token. 

If we want to create such a task and we pass in our token, we hope that this is
a valid token, which it certainly is not. 

Well, then we could write our exact function here and now. 

We just need to make sure the user ID gets added to the request here. 

Write to the request object we pass in. 

So now we'll change our code a little bit. 

We'll call off middleware manually here. 

Now passing a request empty response object empty next function. 

But we call it like this request now is our dummy request. 

And we now, after we executed this middleware, we now expect our request object
to have a new property because we add a new property in the middleware user ID
property and we expect request user ID to be equal to a certain value or we
expect request to. 

And that's also something you can test for to have a property which is named
user ID, right? 

That is something we could expect for a valid token because if the token is
valid, if it is verified, then we make it past destroy catch block, then it just
checks again if it really is defined and yes, we expect it to be defined and
then we do get the user ID from the decoded token and we store it in the
request. 

So expecting that user ID property to to exist on the request seems valid. 

But of course, as you might already guess, if we now run our tests, we'll have a
failing test. 

And that will of course be our last test. 

It should yield. 

The user added after decoding the token. 

But actually what we do get here is simply an error. 

We get that error because our token is malformed because it's too short. 

It's basically not fulfilling the criteria of the JWT Verify method and
therefore it's throwing an error. 

It's throwing an error that the token is malformed. 

What can we do in such cases? 

We can't of course always test if it fails. 

But we also want to test the success case because maybe we have scenarios in our
application where it's not failing with an error and still the user ID is not
getting stored in the request because we simply don't have that code here. 

Then we would have a bug in our application which we want to detect with tests
and this would not throw an error at any point here. 

It would later in the controller when we try to get that user ID, but it would
not throw an error here. 

And still we want to detect this error here already. 

And therefore a test like this one would be super important because here we test
whether we have a user ID stored in the request object after running the
middleware. 

So to find that we need some way of shutting down that verify method though we
know that this is not a valid token, but for this test we don't care. 

We want to test a scenario where we do have a valid token, right? 

We don't want to test whether verification works correctly. 

We know that this normally would not be a valid token, but this is not important
to us here. 

We don't care about whether this is valid. 

We know that verification will work in the actual app. 

We don't need to test whether it is really fails for a random token here. 

We want it to succeed for a random token because we then want to test something
totally different. 

We want to test if our app works correctly for valid tokens, no matter if this
really is a valid token here or not. 

I hope this is clear because it is an important part of testing that you think
about testing this way that you are fine defining your own scenarios and
overwriting certain functionalities to test something else. 

So how can we now shut down, verify and make sure it simply gives us an object
with a user ID so that we can pull that user ID from that object. 

---