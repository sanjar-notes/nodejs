## 476. Cleaning Up

<strong><em>no description</em></strong>

Now, first of all, why do I need to quit this process with control? 

See, the reason for this is that despite me calling done, Mocha detects that
there is still some open process in the event loop and indeed there is our
database connection which we open but never closed. 

So one thing we should do here is when we're done with our expectations, we
might want to call mongoose disconnect and only when this is done. 

So here in the then callback we call done. 

Now this is the first important step, but right now this wouldn't work because
we actually have an overall error in our test case. 

Therefore we don't even make it into this then block here. 

Instead, our setup right here already fails and frozen error because of that
duplicate key because we hard coding and ID here and we already have a user with
that ID in the database and the ID has to be unique and therefore MongoDB
complains when we create it again. 

The solution is to clean up once we're done. 

So besides disconnecting before we actually disconnect, I want to call user
delete many and pass on an empty object, which means all users are deleted and
that is generally not the worst idea. 

If you have a test where you set up dummy data, clean up everything after that
test so that you can be sure that you have a clean setup for the next test
thereafter and also for the next test run, which is the issue here. 

Here for our second test run, we have no clean setup because we already have
that user now with delete many. 

We cleaned it up there, we now have that then lock and there I then want to
disconnect and in the then block there I then want to use done. 

Of course we can clean this up a little bit by converting this to one promise
chain and we can even convert this to one promise chain. 

But anyways, the code isn't super pretty and we'll fix this soon. 

But for now the result should at least be that if we run this again. 

Well, it still fails because we still have that an issue initially. 

Let me actually go there and manually delete this user. 

And now if I run this again, obviously it will succeed. 

But now also for subsequent runs, it should work. 

So now. 

This, uh. 

Fails because I have one extra exclamation mark here. 

So let me now. 

Convert this back to the valid validation here. 

Let's now rerun this test here. 

And of course, clean. 

And of course, refresh here and clean up this user one more time. 

So that we have one clean run. 

Now if we run NPM test. 

Now they all pass and aspergillosis finishes. 

But of course this is not perfect. 

As you can tell, whenever a test fails, we don't make it into this cleanup phase
here because that will throw an error and therefore we would have to add a catch
phrase overall so we don't make it into this cleanup part here if an expectation
fails. 

And in general, this is pretty clunky and pretty hard to read code. 

And if we have a number test that requires a MongoDB database or our dummy set
up, well then we have to repeat all that code and therefore there is a cleaner
solution to all of that. 

---