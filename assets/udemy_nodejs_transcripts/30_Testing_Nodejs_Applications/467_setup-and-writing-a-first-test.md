## 467. Setup and Writing a First Test

<strong><em>no description</em></strong>

Now to demonstrate testing, I picked a snapshot from our course where we just
finished the rest API with async await because that is particularly nice to test
and to dive into testing. 

Now obviously testing different kinds of node applications like GraphQL API all
have their own specialties and special complexities. 

And this is only an introductory module here. 

If you want to learn all about that, you find dedicated tutorials for all these
different scenarios that would be enough content for its own course, and
therefore I rather did not squeeze it all into this one to not bloat it. 

But what you'll learn here, the core ideas, the core concepts, the way of
thinking about testing and the general setup that will always be the same no
matter which node application you're building. 

And therefore this is super important start into testing that you need to then
really master testing. 

So here I have this snapshot and you find that code attached to this lecture, of
course. 

And to add tests here with first of all have to set up our testing environment
with MoCCA and Chai. 

Now you can simply Google for MOCA GS to find MOCA dot org where you can find
the official docs and find out how to install it, how to write tests and so on. 

And the same. 

Of course it's true for Chai. 

You can Google for chai jazz and you can learn more about Chai here and find out
how that works. 

But of course, I'm going to walk you through all these fundamentals here. 

So let's install these things here now with NPM installed safe dash depth here
in our project and there it's just mocha and chai. 

These are the two tools we need to get started. 

So let's install them here and let's wait for that to finish. 

And with the installation process finished, let's start writing our first tests
now for that. 

First of all, let's go to the package store. 

Jason fall in there to the script section and there you should have a test
script already if you don't simply add it now by default. 

This does not have a useful command in there. 

So let's get rid of that. 

And here you can now just run MOCA, just like this, just type markup, this
dependency you just installed without any other configuration. 

Now what you can do now is you can run NPM test here in your terminal, navigate
it into the project folder, and this will now run all your tests you defined in
this project. 

But of course here it's going to complain that it didn't find any test files. 

The reason for that is that mock up by default looks for a folder named test. 

So let's add one and it has to be named test, not tests, not anything else, just
test. 

And in there you can now define files that hold your testing code. 

Now let's start very simple and I'll name it starts as you can name it. 

Whatever you want doesn't have to be named. 

Start can be any phylum you want. 

Should be a JavaScript file though. 

Now in here we write our testing code and writing testing code can be strange
when you see the for the first time, but it quickly becomes very
straightforward. 

You simply write a test by writing it. 

Just it. 

And it is a function provided by MOCA. 

Now it might look like a strange function name, but the idea here is that you
give your tests name and they read like plain English sentences because indeed
it takes two arguments and the first one is a string which simply describes your
test. 

And this is something which you'll later see as an output for your test, which
will help you identify which tests failed and which tests succeeded. 

So obviously this should be a title that kind of describes what's happening in
the test. 

So here we could, for example, test that two numbers are added correctly. 

Now, of course, this is kind of a stupid test here. 

It will become more useful later, but this is just to introduce you to testing. 

So here it should add numbers correctly, could be a description. 

And you see this now reads like an English sentence. 

It should add numbers correctly. 

Theoretically, you can of course put any title you want and here. 

But it's a convention to write sentences like this. 

The more important part, of course, is the second argument, and this should be a
function of function that now defines your actual test code. 

Now later, we'll dare reach out to our own models, our own controllers, and test
these, because that, of course, is the idea that we test our controller
functions and so on. 

But for now we will write a very simple test here. 

We'll add a num one, which maybe is two and a num two, which could be free. 

And now we want to test if these two added together are five. 

And yes, this is an absolutely stupid test. 

Of course they are. 

Just to show you how to run your tests, it'll become more helpful later. 

So we get number one, we get numb to you and now we want to check if they are
added up to five. 

And of course, later you might have dynamic values that the user enters and that
you transform in your code and you want to test if your code transformation
works correctly. 

And then this makes a lot more sense than if you have strongly typed values like
you have here. 

So how can we now check if our test succeeded? 

How can we now define a success condition? 

Well, that happens with the help of Chime. 

Mocha is responsible for running our tests and for giving us this IT function
that defines where we define our test code. 

Chai is responsible for defining our success conditions and for this we just
need to import something from chai. 

Here we import a function that is named expect you do this by requiring chai and
there the expected function. 

Now there also is a different way of defining our conditions with a should
keyword, but we will use the expected way you can learn about the should way
here in the official docs. 

In the end, they do exactly the same. 

They allow you to define success conditions. 

It just differs regarding how you write your test conditions and I like that
expect style more, but you can definitely dive into both. 

So how does this now work? 

Well, you write expect and then inside of this function call. 

So as an argument you pass your code that you want to test or your result that
you want to test like here num one plus num two. 

So we expect this addition here. 

Now, how can we define what this should be? 

Well, again, this is. 

Close to defining or to writing normal English sentences. 

Chai gives you a couple of properties on this object. 

Expect returns. 

So expect returns an object. 

And there you have properties like two. 

And then on two you have another object which gives you things like two equal. 

And then equal is a function where you can define the value you expect us to
equal. 

So this really is something you have to get used to. 

But in the end you again write an English sentence with the help of all these
helper properties and methods. 

And of course in the official chai docs you will learn about this too. 

And there you also learn about all properties you have available. 

So if you dive into the guide here or into the API docs, well then of course you
can learn all about expecting and you can see what you can change so that you
can say to equal to B or whatever you want. 

So here we expect num one plus num one plus one, num two to equal five. 

Now with this defined in the start JS file in the test folder, if you run NPM
test again, it will automatically look for the test folder and execute all tests
in all files defined in that test folder and therefore here in the output we
see. 

A checkmark next to should add numbers correctly, which of course is this test
which is now executed correctly, as you can see. 

And that is what you want to see when writing tests. 

You want to see that all your tests pass. 

Because now, of course, we could define more than one test. 

For example, it should not give a result of six or whatever you want to name it.


And now here we could say we expect number one plus number two. 

Not to equal six, for example. 

So now we're basically checking whether this is not only five, but it's also not
six. 

So now we have a second test defined. 

And now if we rerun NPM test here, well then we get two passing tests. 

And now, of course, it's easy to make a test fail if, for example. 

Change num one here to free and I now run this again. 

Now you see I have a failing test and you see I get an error, I get that it
expected six to not equal six because three plus three now is six. 

But we are not expecting this to be six and this is therefore hinting us at the
test that failed, giving us a reason of why it failed. 

And therefore, when we're not testing dummy code like this, where we have the
reason for to fail written in the test, but where it might be in our other code
which we eventually will test, then this will allow us to fix our other code. 

---