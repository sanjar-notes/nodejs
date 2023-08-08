## 477. Hooks

<strong><em>no description</em></strong>

That cleaner solution comes in the form of life cycle hooks provided by MOCA. 

We have describe and it and it are our test cases describe allows us to group
them instead of describe. 

We have certain extra functions we can call that actually will run before all
tests or before each test at the same for after and after each. 

And what do they mean with that? 

Well, let's say connecting to the database and creating one dummy user is
something we want to do when our tests run, not before every test. 

So we don't want to reconnect and recreate a user before every test, but
initially when our test runs starts. 

So essentially, I want to run this code here, you could say, and I will cut it
before every test. 

This can be achieved by adding before, here, before takes a function and if you
execute async code in there, you should add a done argument here as well. 

And then you paste in your async code. 

And once you're done here and of course, that could be synchronous code to here,
it just happens to be asynchronous because we interact with the database. 

Once you're done, you call done and then Maka knows you're done with your
initialization and it will start running your test cases. 

So it runs all your test cases after, before it and before only executes once,
not before every test case, but before all test cases. 

So now your test cases run and therefore here we don't need that extra then
nesting here. 

This is not required. 

And now here in this bottom most test case, we only define our testing logic. 

We don't have the initialization work. 

The same for the cleanup, of course. 

Clearing our users and disconnecting. 

It's not something I want to do here. 

Here. 

I just want to have my expectations on call done. 

So instead, inside of that described block where we had before, where we set up
that database connection and add our dummy user inside of that described block,
we can also add after and the position doesn't matter. 

You could define this up there too after we'll simply run after all your test
cases now just as before, it just gets a function which is also capable of
running async code with the done argument, and then you execute your synchronous
or async code. 

If it's async, you must not forget to call done once you're done. 

And here I do, then delete my users and then disconnect. 

And then I'm done. 

And now we have that cleanup and set setup work in a more centralized place and
therefore all our test cases can take advantage of that setup. 

Of course, if you have test cases that needs a different setup, you would need
to add them in a different described function. 

By the way, here, log in is no longer fitting since we're also testing the user
status, so I'll just have off controller. 

But you could have multiple described blocks if you need different hooks for
different test cases here. 

All test cases are fine with using the same setup and therefore they all have
the same hooks in their described block. 

And now with that, if I run NPM test again, we should have the same
functionality as before with our test passing. 

But now we have a cleaner setup where we also have our guaranteed setup and
clean up hooks and we don't need to mix this into our test cases. 

And that of course is a way better setup now besides before and after. 

There also are before each and after each. 

Now the difference is that for each is initialization work that it runs before
every test case, before runs, before all test case. 

So it's not repeated. 

It only runs once per test run before each is repeated and runs more often per
test run. 

It basically runs before every eight function call. 

This therefore is useful if you need to reset something before every test case
or if you want to have some initialization work that absolutely has to run
before every test case and there always is after each in case there is some
functionality which you need to run after every test case. 

So some cleanup work which needs to be done after every test case. 

So these also are very useful hooks for testing, of course. 

---