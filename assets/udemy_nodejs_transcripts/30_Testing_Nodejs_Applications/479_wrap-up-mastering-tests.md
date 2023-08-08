## 479. Wrap Up & Mastering Tests

<strong><em>no description</em></strong>

So this is an introduction to testing and you'll learn how to use Mocha and Chai
to write tests and expectations that you can test async code, that you can work
with, testing databases or with steps if you have external dependencies. 

And still this can be overwhelming. 

I know because how are you testing file access? 

How should you work with sessions or with cookies? 

There's so much to test. 

How do you know what to test? 

How do you come up with good test ideas? 

Does it make sense to test whether the status code was set correctly, for
example? 

Well, these are all tough questions to answer or not. 

Regarding the status code. 

For example, always ask yourself, are you testing something that you are
responsible for with your code? 

Regarding the status code, of course we don't need to test whether the status
code is set on the response, but if that exact status code you are looking for
is correct, that is something you could test. 

Is it status code 201 or 500? 

It's you and your code that defines that. 

So it is something you should test if you have functions that are very large and
you find yourself stopping a lot of stuff to test some tiny part of it, maybe
you can split a function apart. 

We could do this for our controllers here too. 

We could, for example, also outsource the part where we add a post to our user
posts into a new function that simply accepts a user ID and the created post as
an input, and then looks for that user ID and adds that post. 

So a function that essentially only does this part, we could outsource this into
a new function, which then all of a sudden becomes way easier to test because
you test functions and splitting your code into more granular functions can make
it easier to maintain and easier to test. 

So if you have problems testing large functions, try splitting them in smaller,
more testable functions. 

If you're wondering how to test sessions or cookies, well, google is your
friend. 

Sounds dumb, but it's the case. 

Search for Node.js. 

Express cookie testing. 

Session testing. 

You'll find instructions, ideas, thoughts by other people. 

Because testing is a lot about thinking and experience and trying stuff out. 

There rarely is one correct solution. 

It's also the case for writing your own test cases here. 

What do you pass in as a dummy configuration? 

Like for example, this time request object. 

How should it look like? 

Analyze, decode your testing and then think about how you need to configure your
inputs or your dependencies for your test scenario to become real. 

Of course, always keep an eye open if you're maybe just testing for stuff you're
introducing here. 

For example, when you're testing the user sign up and you pass in some dummy
request object with an email and password that might look like this, and you're
then expecting a user to be created with an email address of test two at Test
Dotcom. 

Well, then your test will fail and not because your code is bad, but because
your test is bad, because you define a bad input for your expectations. 

And therefore, testing really is about trying stuff out, gathering experience,
diving into discussions with other developers, diving into StackOverflow, and
that will make it easier over time. 

I hope it became clear that writing tests in general isn't too hard, though that
you write code that tests your code and the official docs of Chae and MOCA
should really help you. 

Defining tests, grouping tests, testing different things and you'll find plenty
of third party packages and plug in that can make it even easier. 

For example, testing things like sessions or testing promises. 

There are all the packages that make that easier to let you write even leaner
code than we are doing here. 

So with that, I hope this introduction was helpful and I hope you now are not
just able to write awesome note express applications, but you are also able to
test them both manually and automatically. 

---