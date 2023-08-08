## 473. Testing Asynchronous Code

<strong><em>no description</em></strong>

So we want to check whether that promise we have in there eventually returns an
error. 

For this test we're writing here. 

Right, because we're testing for an error code of 500. 

Now for that, let's make a tiny adjustment here. 

In our off controller file. 

Let's add a return statement here at the end. 

This will implicitly return the promise we have hidden behind async await in
here. 

We can now. 

Change this code. 

Reach out to the off controller, log in and called it. 

And of course, there, just as before, this is a middleware function and express
and it needs a request object, response object and a next key or next function. 

Here, the request object should have a body field which has an email and a body
field which has a password and well then we should fail anyway. 

So we don't really need to care about what else we're doing in the rest of this
code here. 

So let's create our dummy request object here. 

And that request object. 

Well, now I have a body field and that in turn will have an email test, a test
on call maybe, and it will have a password tester, whatever you want. 

And I passed it into my login method here. 

I also pass in an empty object forward to response and I also pass an empty
function here for the next method. 

Now I can add then here because we return a promise in the login method
implicitly. 

And then. 

Should now be executed once it is finished. 

And there. 

We now want to check for our error status code. 

So I get my result here. 

And I'll, first of all, simply console lock the results so that we can have a
look into this. 

And now let me run NPM test. 

Now what we see is, first of all, all pass, which is strange, but if we scroll
up a bit, we see all the undefined here. 

The reason for that is we go back to the off controller. 

I do return here, but indeed I return undefined. 

Right. 

And that is what I overall return as a value of that promise that gets returned
here. 

So what I actually want to return here is my error object or a bit earlier here.


There, maybe it's undefined. 

So in the success case I return nothing in that promise, which in the end gets
returned. 

Here, I return the error. 

So now if I rerun NPM test. 

Now we see that our object being locked up there. 

Does not look better. 

There's not allows us to change our record a little bit and actually expect
result to be NW. 

And now here you can actually pass an error. 

China is able to detect a couple of types of data and error is one of them. 

Of course, the official docs are the place to go to learn all about that. 

Our possible values would be string object, null promise, and so on. 

So here I expect it to be an error and I expect result. 

Q half a. 

Property. 

So to have property, I expect it to have property. 

Off status code, right? 

Because my error object should have that status code. 

So I expect a property status code which should be 500. 

Now ever run npm test on first look it looks good. 

Everything passes but actually this is a false pass here. 

It passes because Mark doesn't wait for this test case to finish because we
actually have async code in there and by default it does not wait for that async
code to resolve. 

It executes this code synchronously step by step and does not wait for this
promise to resolve no matter how fast is this? 

Now of course we can tell MoCCA to wait. 

We do this by adding an extra argument in this function we pass to it, and
that's the done argument. 

Now this is optional and it is indeed a function which you can call. 

So Mark, it gives you a function here which you can call once this test case is
done by default, it's done once it executed the code top to bottom. 

But if you accept this argument, it will actually wait for you to call it and
then you can call it in an asynchronous code snippet. 

So here now inside of this, then block here, I call done and I signal that I
want marker to wait for this code to execute because before it treats this test
case as done. 

And now if I run NPM test again, now it passes again. 

But now this is actually a valid test and we can confirm this by changing this
expected status code to 401. 

Because now. 

Does actually fails, as you can tell. 

It should throw an arrow cut of 500. 

And if you scroll up a little bit here, you see you got an error code of 401 of
500, but expected one of 401. 

That's what we wrote here. 

And indeed it now failed without done. 

And you must alter remove it as an argument because if you have it as an
argument, marker will actually by default check whether you have code that
executes asynchronously. 

So without that argument, without calling it, therefore now if you run this
again, all tests pass. 

So it's really important to pass done and then call it once you are done to make
sure that your tests were correctly. 

So now if I change this back to 500, which is the realistic expectation, now
they all pass and now it is really is correct. 

---