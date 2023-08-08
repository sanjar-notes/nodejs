## 400. What is Async Await All About?

<strong><em>no description</em></strong>

So what is async await all about? 

Async and await are two keywords which are part of the core javascript language,
they're not an exclusive part of the nodejs runtime, they are also available in
modern browsers or in frontend projects, they're not part of nodejs but you can
use them in nodejs projects. 

The question of course is what do these two keywords do? 

Async and await allows you to write asynchronous requests, so requests where you
have some operation that takes a little while and comes back later in a
synchronous way and you see there is an asterisk after synchronous way because
async and await allows you to write asynchronous statements in a way that looks
synchronous but it still isn't a synchronous request. 

Now this is of course very abstract, so let's simply dive into our existing
nodejs code and let me show you which parts of it you could change to use async
and await and then it will become very clear what it does. 

I'm back in my nodejs backend application here and let me point out that as I
mentioned, you could also use async await in the react application but this is
no react course so I will leave this code untouched and I will go back to my
node application. 

Now how can we use async and await? 

Well if you go into your feed controller, you'll see that there we have an
asynchronous operation, post find. 

How can you see or how can you identify asynchronous operations? 

Well for example when you're using promises. 

Promises are a typical construct that help you deal with asynchronous code
because promises work like that. 

Post find gets executed and count documents also gets executed immediately but
then this actually, count documents returns a promise or a promise-like object
and you then use then to define a function that should be executed once this
operation here is done and since we access the database here, this typically
takes a bit longer. 

We're talking about milliseconds here but still it doesn't happen instantly. 

On the opposite, this line and this line get executed after each other
instantly, this operation does essentially not take any time at all, it's so
fast javascript can wait for it to complete and move onto the next step right
away. 

Here it will not wait for that to complete and that is why after this statement,
javascript would actually move on with the next statement inline, so if we had
another statement on the same level as post find, we would continue with that. 

Now in this case we got none but if we would have some code there, like a
console log or anything, this would execute right away, probably or very likely
before this or this code or this code was executed and the reason for that is
that with then, we define code snippets or we define functions that should run
in the future once this longer taking asynchronous operation is done and it's
called asynchronous because it doesn't happen instantly but it takes a little
while. 

Callbacks which we used earlier in the course are another way of working with
asynchronous code, so here too for count documents, you could actually and you
see that here in the documentation that pops up, you could define a callback
function. 

So here you could define a function that gets executed once it's done instead of
then and we don't use callbacks because in there, we would use that code and
then we would need a callback here in the find function and we would nest all
these callbacks leading to very unreadable code. 

That is why you often prefer promises even though you could do it with callbacks
because there, you have one then block after each other and it's very readable. 

Still it can get more readable with async and await and that is what I want to
show you in the next lecture. 

---