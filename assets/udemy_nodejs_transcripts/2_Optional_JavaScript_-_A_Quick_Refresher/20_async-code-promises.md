## 20. Async Code & Promises

<strong><em>no description</em></strong>

Now I cleared the play case file again because to conclude this quick refresher
module, I'll dive into another core concept, and that is how to work with a
synchronous code. 

And for that, we first of all have to understand what asynchronous code is. 

Let's say I set a timer with set timeout, which is a function built into
Node.js. 

There we define a function that should execute after a certain timer expired. 

Here, I'll use an arrow function. 

You could use a named function, whatever you like. 

The second argument is the timer. 

Let's say 2 seconds. 

You express it in milliseconds. 

So 2 seconds are 2000 milliseconds in their. 

I'll simply log timer is done. 

If I now run this file for 2 seconds, nothing happens and then we see timer is
done. 

Now this is asynchronous code because it doesn't finish immediately and it would
even be a sin code if we had one milliseconds there. 

So if it's super fast, it does not happen immediately in our code snippets like
if we have console.log. 

Hello. 

And console.log. 

Hi. 

These two snippets are synchronous code because they are executed right after
each other. 

And yeah, technically of course it will take some time to execute them, but
there is no delay other than your hardware, so to say. 

And therefore this is synchronous code, this is async code, asynchronous,
because it does not execute or finish immediately. 

It takes a little time, even if that's super short. 

And indeed, if I execute this file like this, you see, hello and hi. 

Before you see timer is done, even though it's super fast because Node.js and
JavaScript in general does not block your code execution until that is done. 

Indeed, here it will recognize this so called callback function. 

So a function should execute in the future. 

It should call back later once it is done. 

So once this timer expired here, it will just recognize that and will then
immediately move on to the next line and will execute all the synchronous code
and then execute your async code once this is done. 

Which is why we see how low and high first, even though in our code time is
done, is printed first, and that is a crucial concept you have to understand in
JavaScript and especially Node and I will come back to that throughout the
course because it's so important. 

Now when working with that and I'll increase this to 2 seconds again to make it
even clearer, then you will see again our sync code runs and then after 2
seconds this code runs. 

When working with async code, we get multiple techniques of well handling it. 

The callback function is one, the oldest one, and you'll see it quite a bit,
especially in Node.js. 

There's nothing wrong with it, but you'll face a problem if you have a couple of
depending async operations. 

So here we set the timer and now let's say I create another function. 

Which I'll name fetch data. 

And in there I will also just set a timer because I don't want to set up some
data base or something like that. 

Where we fetch data from will do all that throughout the course. 

Of course, no worries. 

So here again, I have another timer in there which takes like one and a half
seconds. 

And now here in fetch data. 

I need some way of well, doing something when this inner timer is done. 

So here I will actually expect an argument which I'll name callback, because
this argument will be a function. 

I will eventually call in my inner function here. 

Once I'm done with the timer there, I can pass done as a value now in the place
where I use fetch data. 

Let's say that's inside of this set timeout call. 

I call fetch data like this. 

There. 

I now need to pass another callback. 

And here. 

I will get the text passed by the callback in my function when I execute it. 

So we'll get some text here and icon console.log that text. 

Now this might look confusing in the end here I'm creating my own function,
which gets a callback so that I can define a function which should execute once
this inner timer is done from some other place. 

So from this place here, this is the function which effectively is passed in as
a callback, and I'm executing that function here. 

Now, if I save that and I run that. 

It takes 2 seconds. 

Then it's trial time or it's done. 

And then after one and a half seconds, I see done. 

Now, if we have a couple of nested async calls, as we have here, we go deeper
and deeper from a callback perspective. 

And that is why we also have a feature called Promises, which we can use
Node.js. 

Now often we'll use third party packages that already use promises for us. 

So the syntax I'll show you now is one you really have to write on your own. 

That will be done by the packages behind the scenes. 

Still nice to know you create a promise. 

Inside of our fetch data function here, let's say. 

By storing it in a constant or variable, and then by using the new keyword which
you use in JavaScript to create a new object based on a constructor. 

If constructor functions are something that tells you nothing. 

Check out some basic introduction resource to JavaScript because constructor
functions are a core feature in JavaScript. 

And here you use the Promise constructor function which is built into JavaScript
and Node.js. 

And this actually also takes a callback which gets to arguments, resolve and
rechecked. 

You could name them however you want, but these are two functions and the first
one completes the promise successfully. 

It resolves it successfully, the second one rejects it, which is like throwing
an error. 

You then take your async code and move that into there and again, you really
have to write this on your own. 

Most packages already do that for you and give you the finished promise, which
does all the magic behind the scenes hidden away from you. 

Here we do it manually. 

So now in that callback we have our own function set. 

Timeout does not give us a promise API unfortunately. 

So here we also have to use a callback. 

But in there. 

We now know no longer use any callback function we get. 

I get no argument here in fetch data anymore. 

Instead here I resolve done let's say so I successfully return to resolve value
now in fetch data after defining the promise, we just have to return it. 

And please note this is synchronous code. 

So actually this will be returned immediately after the promise gets created,
before the code in the promise is run, which will happen sometime later when we
actually call that function and when this timer then completes. 

So we now return that promise here and in the place where we call fetch data. 

We now no longer pass a callback, but we can now use then which is callable on a
promise and we return a promise. 

And this simply allows us to now define the callback function here, which will
execute once the promise is resolved. 

Now. 

What is the advantage of that? 

If we had multiple such promises. 

So let's say I call fetch data again in there then I don't have to use then like
this. 

And therefore I would end up with nested. 

Callbacks again. 

But instead inside of a promise. 

And then block is part of a promise I can trust. 

Return a new promise and then add the next then block after the previous one. 

Like this. 

So now we have a chain of then blocks. 

This one gets called on the first promise, then in the then block, I return
another promise. 

And even if that would not give us a promise, instead of a then block returning,
it would convert it to a promise that instantly resolves. 

And then we add another then block, which is now referring to this promise here,
and this is more readable than having infinitely nested callbacks. 

So now if I run that, we see. 

Hello. 

Hi. 

The timer is done. 

We are done and we see done again because I'm calling fetch data twice. 

So this might be difficult to wrap your head around for the first time. 

We will reuse it throughout this course and then it will become clearer again. 

This code is mostly not written by you, but it is a crucial concept that makes
our async code more manageable. 

There always is another way of managing this async await to special keywords you
can use in modern JavaScript, and I'll have a separate section about this
towards the end of the course. 

I don't want to introduce it here because it can actually be more confusing than
this syntax here. 

And I want to stick to this one to not introduce too many new features at the
same time here. 

Async code is something you have to understand though, and if it's not totally
clear by now, that is fine though you will see it throughout the course a bunch
because we have a lot of asynchronous events in Node.js and I will explain this
multiple times. 

I'll also explain promises. 

Again, I just want to ensure that you have seen this by now and that you then
have a chance of understanding this, how it works and how we deal with it. 

---