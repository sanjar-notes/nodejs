## 469. Organizing Multiple Tests

<strong><em>no description</em></strong>

Now that we wrote our first test, that actually makes sense. 

Let's continue and write the number one. 

Our code here only works correctly if we have a header and authorization header
which can be split into two pieces because that's what we're doing here. 

The reason for that, of course, is that we expect something like bearer and then
our token, right? 

That is how we send our tokens, that is how we send that authorization header
and therefore this is something we could test for. 

It should flow an error if. 

The authorization header is only one string. 

Now let's pass a function here again where we define our actual testing code. 

And in there now again I will create my own dummy request object where I get my
authorization header. 

Now it's not null anymore, but it's only one string, so only let's say x, y, z
as a token value. 

And that means that now we can again to find an expectation where we say when
the off middleware gets called, and just as before, we're not calling it
ourselves, we're preparing it to be called by using bind here. 

This says to this keyword, then our dummy request object, then an empty object
for response, and then well, an empty function for the next function. 

And I expect that to flow. 

Now you could check for an exact error message, but if you're not sure, or if
you only care about whether an error is thrown at all, you can also just check
for flow like this without passing any arguments to it. 

So now this should indeed fail. 

If I now rerun NPM test here, I mean it should succeed because it's because
indeed we get an error if we pass this in. 

Because if I check for this not to flow just to demonstrate this now, it will
actually throw as an error here because it expected it to not throw an error. 

But actually we got an error here, as you can see, because splitting our code
essentially failed. 

So we want to make sure that an error does get thrown here, and that is another
test. 

Now, of course, the more tests we add, the more difficult this output here
becomes to read. 

Right now, it's still easy. 

We know we're only testing the off middleware and there we got to tests. 

But what if we're testing more than just the of middleware? 

What if we later all to start testing our controllers, which we will? 

Well, then we might want to find out which of these statements here refer to the
of middleware and which statements refer to our controllers or to which
controller. 

And for that, Mark actually gives us more than just the IT function for defining
and organizing our tests. 

Besides it, there is a describe function, a describe function is there to group
your tests and you can test as many describe function calls as you want. 

So you can have multiple describe function calls inside of each other, describe
all the takes a title, and that now is not a sentence that reads like an English
sentence, but instead like a header for the group you're describing, like, for
example, of middleware. 

Now this gripe also takes a function as a second argument, and into this
function you pass all your test cases as these function calls are called. 

So now they're inside of this function of the scribe. 

And as I mentioned, if you need it, you can also have a describe in a describe. 

And then in the function of that describe, you could have your test cases. 

So now we have that organization and if I now run LPM test again, you see that
you have this header here now which makes it easier to find out to which file or
to which area of your code of your app these tests belong. 

And that of course can be very useful. 

And therefore from now on we'll use this describe grouping to make our code more
readable and easier to understand. 

---