## 474. Setting up a Testing Database

<strong><em>no description</em></strong>

Now obviously we can test way more about our controllers, but that is basically
now all about stuff that I already explained to you. 

You can write different expectations. 

You can set up different request objects. 

You pass in with different email addresses and passwords, and that allows you to
play around and expect different things. 

But I also mentioned that there is more than one way of dealing with code that
accesses a database. 

The way we deal with it thus far is that we simply stop it away. 

We create a stub for the find one method and then define what this should do for
this test case. 

And then I restore it. 

And that is absolutely fine. 

It prevents the real database access from happening here. 

And that, of course, might be what we want because it allows us to run our test
faster and of course, important. 

It also doesn't impact the database because your tests could still write data to
the database and you definitely don't want this to happen in your production
database at least. 

It is, however, a valid setup to use a dedicated testing database because whilst
of course the downside is that your test will run a bit longer, the upside is
that you have a very realistic testing environment. 

If you really hit a database and you really write data to that database and you
read it from there, you have a bit of more. 

You don't just have a unit test. 

You have kind of a integration test because you have a full flow of controller
gets executed, model does its job, reaches out to the database, returns data. 

You have more than just a unit test, but you also have a test under very
realistic circumstances. 

And in some cases this might be what you want and it might be easier than
stopping everything and writing a lot of stubbing code. 

And therefore, let me show you how you could set up a testing environment for
MongoDB, where you use a dedicated testing database because that's important. 

You definitely don't want to use your production database for testing. 

You don't want to mess with your user data for testing and accidentally delete
it or anything like that. 

So let's actually create a new test here still related to the off controller
before we finish up this module with the feed controller later. 

So still related to the off controller and we had a look at log in. 

Obviously, there is more we could test, but let's now move on to the get user
status method. 

You're actually to to get user status controller action there. 

We're finding a user by ID and therefore will need to make sure that our testing
database has such a user. 

And we then just want to make sure that let's say we could of course also test
that we don't find a user for ID and test for an ID that does not exist. 

But let's also say we want to test for an ID that does exist. 

Then we just want to make sure that we actually don't return an error, but that
we instead return a response where our user status is set. 

That could be a test we want to write. 

So back in the off controller, I'll add a new test case and give it a
description of it. 

Should send a response with a valid user status for an existing user, something
like that. 

Now this again will require that done keyword because we'll again run async code
in that test case. 

And now inside of that test case, I want to connect to my testing database. 

I want to make sure that there is a user in that database, of course, because
otherwise I can't retrieve the user. 

Then I want to retrieve it and I want to make sure that I do actually then that
my controller action does correctly retrieve the user status and add it to a
response with the status code of 200, let's say. 

Now for that, first of all, we need to connect to the database and this requires
us to import mongoose. 

So let's require Mongoose here and set up a connection down there in this test
case. 

And I'll show you a different way of doing this on a per test case basis soon. 

But for now, let's do it here by calling. 

Whoops. 

Not disconnect, but connect. 

And now you need your connection string. 

And for that you can generally use the same connection string used before an app
args. 

So this connection string here, you can use that and actually of course you
could. 

Copy this entire code here, even into your off controller. 

Add it like this. 

Now just need to adjust some things. 

I changed that password for that user in the meantime, so I'll paste that in. 

And now important the database to which you're connecting there should be a
testing database, so I'll name it test messages here and that's super important.


Don't use the production database. 

Now of course we don't call app listen when we are successful, but instead here
we now can continue setting up our test. 

And again, I will show you a more elegant way of doing this, all in this nested
manner later. 

So here I now want to define my my testing logic. 

And my testing logic here, of course, is that, first of all, I need a dummy
user. 

So I'll create a user with new user. 

User is already imported. 

And that user which gets created here, of course, has to be created as we do it
in our user model or as we define it here with the email, a password, a name
status does not need to be set because there is a default of I am new for which
we then should check later and post array. 

So email, password, name and post is what should be set here. 

Email could be test at test dot com. 

Password can be tester and of course no hashed password. 

But this is all just a testing setup. 

The name could be test and the post array can be empty here and status again
doesn't have to be set because there is a default defined. 

Then we call save and I return this because this will all return a promise so we
can now add another then block. 

In this function here we now have the dummy user set up and saved to the
database. 

---