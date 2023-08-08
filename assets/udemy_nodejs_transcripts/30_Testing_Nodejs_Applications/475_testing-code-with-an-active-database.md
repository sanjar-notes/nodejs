## 475. Testing Code With An Active Database

<strong><em>no description</em></strong>

With that dummy user set up, we can now do our actual testing logic. 

So if we have a look at our off controller here at the off controller file, so
in the controllers folder, we need a request that has a user ID field because
we're finding a user by that user ID and then we alter the response object by
calling a status method on it and adjacent method. 

So we need to pass in a request object that has a user ID and the response
object that has a status method and adjacent method where we then can set some
status data. 

And again we can of course pass our own response object here instead of using
the real one to fine tune it to our needs so that we can easily test this. 

So I'll create my request object here first of all, where I have a user ID and
of course that user ID should be the idea of the user we're creating here now to
simplify this. 

We can give this user an ID, you can explicitly set one and here that can be a
string. 

Now the format of the string matters. 

You can use the one you find attached to this video here, which is a string
considered to be a valid ID by MongoDB. 

So I'll give this user my own ID so that I can pass the user ID here in the
request so that I do really find a user that exists. 

Of course we could all to test our code for cases where we don't find the user
with the wrong ID. 

But here I want to get a real user and I want to test if this response is set up
correctly. 

Right, because that is what we're testing. 

We should send a response with a valid user status. 

For an existing user. 

So. 

This is the request now for the response. 

I will no longer just send an empty object, but instead the response object will
need a status method and adjacent method and some place to store that user
status and the response status code. 

So I will have an object here. 

With a status code field of 500, let's say initially of. 

A user status of null initially, then a status method. 

So a function here where I get a status code and I then set this status code
equal to code and then I return this here so that status returns this response
object again so that here. 

I can actually call Jason on this object because here I am able to change these
methods. 

So to be able to do this, I need to return this here and then I'll add this. 

Jason. 

Function here. 

Where I have some data which I get as an argument. 

Now the data, of course, will be here an object where we have a status key,
which is the user status. 

And therefore here I will then set this user status equal to data status because
again, the data we're getting will be an object with a status key. 

So I'm extracting that and storing that here. 

And therefore, we now have a response object with which we should be able to
interact just as we do in the off controller. 

Now it's the time to actually run our test code and use the off controller. 

Get user status. 

And then here, because this still is async function and therefore it implicitly
returns a promise. 

So here I then need to of course pass in my request response and then this empty
next function. 

And then in here, in this function which executes once our controller is done
there, I can define my expectation. 

And my expectation is that this response object now has a status code. 

Which is equal. 

So with to be equal, for example, which is equal to 200 and not 500 anymore
because we should set it to 200 here if we succeeded extracting that user. 

And of course, that the status is extracted correctly so that our user status
field is populated. 

To the default status we have in our user model, which is IMU with an
exclamation mark. 

So this is our default status. 

Since we don't set a different status here in our dummy user object, we should
have that default status. 

So I expect it to be set and thereafter I call done because this is when I let
Mark finish this up. 

Now let's give this a try and let's run NPM test. 

And we have six passing tests, including this one here. 

It took quite long, which is okay. 

By the way, if this times out, you can define a longer time out period by going
to your scripts and adding dash dash time out here after mocha and set this to 5
seconds, for example, with 5000, because this is in milliseconds, the default is
2000. 

And if you're timing out here, set it to 5000. 

But now this seems to work. 

Let's also have a look at the database now and see if the test database exists
and if the dummy user exists there. 

So we'll look at our collections here. 

Now, if I have a look at my database, I have a couple of collections. 

I do have that text messages database and there I have a user's collection. 

And in there indeed I have that dummy user. 

Now, just to really be sure, if I check for a different status and I rerun this,
you can quit that process, which was still running with control. 

See now indeed, we get a timeout error here because we got one failing test
where we have that test up there failing. 

However, it fails for a different reason. 

If you watch closely, you see it fails because we have a duplicate key issue. 

And that of course stems from our setup code here where I create a new user that
now for the second test run already exists and the result is a different issue. 

This process doesn't quit as it did before. 

We manually have to do this with control. 

See, now let's fix all these things in the next lectures. 

---