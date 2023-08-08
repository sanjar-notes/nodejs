## 468. Testing the Auth Middleware

<strong><em>no description</em></strong>

Of course, it's now important to point out that these tests are totally
redundant. 

We're not testing our code, not our application code. 

At least we're testing some dummy code and we're defining everything our test
relies on directly in the test. 

Therefore, this test runs stand alone, totally detached from our application. 

And whether the test succeeds or fails, it only depends on the testing code
itself, which of course is a test you should omit. 

It's not a helpful test. 

This is just some JavaScript code. 

You're running nice if you have too much time to spend, but certainly not
helpful in reality. 

You want to test your application code and you want to test code that's not
entirely defined here in your tests. 

Instead, in your tests you typically only define your success condition. 

You can, by the way, also have multiple success conditions, multiple
expectations, and you might define any additional setup you need for that test. 

For example, user input, you're assuming for this test to simulate different
scenarios, but you don't want to have the actual code or the actual behavior
you're testing in your test. 

That is not the idea. 

And therefore, let's get rid of these dummy tests here. 

I'll simply comment them out and let's write a more realistic, a more helpful
test. 

Now, what could that be? 

Let's have a look at our middleware at our is off middleware and let's maybe
test something related to this function we're exporting here. 

We're exporting a middleware function and in the end we could test all kinds of
things there. 

So let's add a new file in the test folder D off middleware JS file, for
example, and you can name this whatever you want, of course. 

And here I now want to import this function and then test it. 

So I'll import my off middleware by requiring it, of course from the middleware
folder from the is off file. 

And then again we define a test. 

Now what could we test here? 

There's a bunch of stuff we can test and we will test different things here. 

But the first simple test could be that we want to make sure that we really get
an error whenever. 

This year does not have an authorization header. 

So back of the off middleware GS file where we define a test, we put the final
test where it say it should throw an error if no authorization header is
present. 

This is a valid description for our test here. 

And then I'll add a function where we actually add our testing code. 

And now we of course want to call our off middleware manual here because we're
not simulating a full request flow, we're not simulating a click of the user,
which then sends a request, which then triggers the middleware. 

We just want to test our middleware function. 

This is called a unit test, by the way. 

We test one unit of our application in this case, that is this function. 

Typically a unit is a function here. 

It's this middleware function integration test would be where we test a more
complete flow, so where we maybe test whether the request is routed correctly
and then all to the middleware and then also the controller function. 

But you don't test that too often because it's very complex to test such long
chains. 

There are multiple things that could fail, and by writing unit tests, it's way
easier to test different scenarios for each unit. 

And if all your unit tests succeed, you have a great chance of your overall
application. 

Working correctly and therefore writing unit tests is very helpful. 

If a unit test fails, it's all too easy to find out why it failed. 

If you have a lot of steps in, Wolf, that might be harder to find out which step
failed. 

So we're testing this middleware function only. 

And that, of course, means that we have to create a dummy request object we pass
in, because normally that's passed in by the Express middleware, just like
response and next. 

But now since we're directly calling our middleware function, we want to define
our own request object. 

And that is actually great because that allows us to define different scenarios.


So here I can create a request object and that object here should have a get
functional because in the off middleware, I'm calling this get function here and
this get function now in reality returns the value of the authorization header. 

Now in reality, this get method here provided by express is way more complex. 

Of course it does not only scan headers, it scans different parts of the
incoming request, but our goal now is not to replicate the express framework,
but to test one specific scenario. 

And here the scenario is that get authorization does not return an authorization
header because that is what we want to test here, that in this case we throw an
error. 

So here function dysfunction should simply return null. 

This means it does not return a value for our authorization call here. 

Now of course here we pass an authorization string to the get method here. 

I'm not expecting this argument. 

You could, of course add it here. 

You could expect your header name or whatever you want to call it. 

But I don't really care about this. 

I know that the code I want to test calls to get method and I know that I want
to return null to simulate that there is no authorization header because I of
course know the code I'm testing and I want to test different scenarios and this
is how you have to think about testing your testing different scenarios. 

You're not trying to rebuild the framework you're using, you're not trying to
rebuild some complex functionality. 

You want to force your code into certain scenarios. 

You want to test them under certain scenarios. 

And here the scenario is that the get method on the request object returns null
no matter what it does in reality. 

So here we return. 

NULL, which of course could be the case if in our real app that really runs, we
get a request where no authorization header is set. 

In this case, this would all the returned null or undefined. 

So here we return null. 

Now we can call off middleware and pass in our own request object here, which
has nothing else. 

It has nothing else. 

The request object normally has, but it has everything we need for this test
there. 

We only need this get method and it has that. 

Now for the response object we can pass in an empty dummy object because we're
not testing anything related to this response object and the code we're testing
all that doesn't rely on it. 

It doesn't even use the response object in this entire function. 

And therefore we don't need to spend any time on adding any logic to this
response object. 

And now the next function which is called at the end, well, we want to pass it
in, but we don't care about what it does because we're not really executing our
next step here anyways. 

So here I'll just pass in an empty arrow function so that it is able to call
that without. 

Brilliant error, but that it also doesn't do anything because it's again, not
what I want to test. 

I only want to test the behaviour when get returns null. 

So now we're calling this. 

But of course we wanted to test something, right. 

So let's now import expect again by requiring Chae and then expect and now let's
expect the result of that off middleware call here. 

So of that entire call to be something where in this case to throw that's all
the just in our utility method you have here you can find this in the official
docs of course here if you scroll down or if you as I do here, search for flow,
you'll find detailed explanation. 

So now here I expect this function call for a request that returns null when we
try to get something for a given header name, I expect that to throw. 

An error with the message. 

And now the message, of course, is to find in our real code we should have a
message of not authenticated. 

So this exact message here. 

So I expect this to be thrown. 

Now let's rerun NPM test here. 

And. 

I actually get an error. 

And that, of course, is strange. 

Why am I getting the error I'm trying to test for? 

Actually, this should pass without an error because the function frozen error. 

Because that's what I'm expecting. 

Well, the reason is simple. 

I am calling my middleware function here, and this middleware function just
happens to throw an error. 

I don't want to call it myself. 

I want to let my testing framework. 

So I want to let Mocha and Chai. 

These two tools. 

I want to let these call this function for me so that they can handle the in
error. 

Here I would have to handle it myself and that would defeat the entire purpose
of testing this. 

So instead of calling off middleware directly ourselves here, we instead only
pass a reference to this function here to our expected function, and we only
want to bind the arguments we eventually want to pass in when our testing set up
calls. 

This function by and first of all requires an input for this keyword that can be
this, and then it has the free arguments that will actually be passed into the
off middleware function once it gets called. 

So we're not calling it ourselves here. 

We're instead passing a prepared reference to our function. 

You could say prepared in the sense of we're defining which functions get passed
in or which arguments get passed in. 

So we're passing that prepared reference to expect. 

And now if you rerun NPM test, you should actually see a passing test. 

Now, if you're expecting a slightly different error message and you rerun NPM
test, you actually get a failure because we expect it to throw an error,
including not authenticated. 

Right. 

That is what we're expecting here with an exclamation mark. 

But we got no authenticated with a dot. 

And that's the idea behind testing. 

You have to be clear here, because you can test for all kinds of different
things. 

And here we're testing for the correct error message being thrown. 

And therefore this test only succeeds if we a have an error. 

If we are not throwing an error in here, if we're indeed if we're instead
sending our own error response and we're not following an error, then this test
would not succeed. 

Or if we throw an error with a different error message, as you just saw, this
all doesn't exceed. 

Now, the cool thing is, if we now ever change something about this code, for
example, we decide to remove this check here where we check for the off header
and I now run my test again. 

I get an error and that tells me, Oh, I need to do something because my test
failed. 

This test where I want to make sure that not being able to retrieve the head or
actually frozen error, that does not pass anymore. 

And therefore now I should have a look at my middleware and I can find out, Oh,
I commented this out or maybe I never added this functionality in the first
place, or I tweaked it in some way that this error is not thrown anymore. 

Maybe I should just check and change this condition accidentally. 

I'm checking for the existence of a header to throw that error because I have a
typo or because I needed that in the past or whatever. 

Then my test fails as you can see, and I can look into my code and find out why
it failed. 

And here I see. 

I expected it to throw an error, but actually I got a different error. 

And since I got a different era, well, it's probably something wrong with this
code here. 

And I can look into that code and eventually find out that here I'm missing an
exclamation mark, for example. 

So that's the idea behind testing. 

Whenever we then change something in our code, as long as we have tests for it,
we get a warning, we get a chance of tweaking our code and fixing the issue we
introduced. 

---