## 492. Node Core Modules & Promises

<strong><em>no description</em></strong>

<v Instructor>I mentioned one other modern feature</v> which we can use a node
now, which I didn't use throughout this entire course. 

And that would be promises in core APIs. 

And that's important. 

I did use promises throughout the course, we have whole modules dedicated to
promises and async await. 

So you absolutely should know what promises are, how they work and why we use
them by now. 

We use them because a lot of third party libraries and also our own code can of
course utilize promises to handle potentially asynchronous operations. 

Now there is one part of the node apps we wrote thus far, which doesn't really
leverage promises and that would be the core APIs baked into node. 

I'm talking about things like read file from the file system module. 

There we use this callback based approach. 

And the reason for that is very simple, when Node.js was created, promises
simply weren't a thing, they didn't land in mainstream JavaScript yet, that's
why Node.js and its core APIs are callback based. 

Now, of course, here, we're using a different approach of sending the file back
anyways. 

But if we switch back to the previous approach, and if you had some operation
that needs to read a file or do anything else with a core node module, you might
wish to be able to use a promise instead of this callback approach which you're
forced to use unfortunately, while there are good news, a lot of core APIs baked
into node now also have promise support. 

Again, we can dive into the official docs, and there if you check out the file
system documentation we'll find one interesting thing. 

Data we find all the methods we can use on the file system, that's all nice, but
if we scroll down further, we see that there is a fs Promises API. 

And essentially, that's all the file system features here, now available in a
promise based version. 

So for example, we also have a write file method now, which actually embraces
promises so that we can use promises with these core APIs. 

And a lot of the built in core APIs have such a promise version. 

How do we use that? 

Well, we need to import the file system slightly differently. 

Instead of from fs, we import from fs/promises. 

And that's all, if you by the way use the old D require import syntax, it's the
same. 

So there you can also use promises even if you're not using the other import
syntax I showed you here. 

Actually, I have to step in here. 

This is not correct. 

You would import it like this, if you use the other import syntax. 

You access the promises proper key on the imported file system object. 

And this promises property exposes the file system object with all those file
system methods using promises. 

This is the proper way of importing it. 

Now, since we use the different import syntax, I unfortunately wrote this
incorrect syntax here. 

Keep in mind if you would use that upper import syntax, it's this year, this is
how you would get access to those promise based API's not this. 

Just a little addition here which I recognized after I recorded this. 

Sorry for the inconvenience here. 

In this module of course, we're using this syntax anyways though. 

Now with that, we got the file system object available. 

And we can call read file on that but this read file method now returns a
promise, which eventually will resolve to the data where to the err or data
we're getting back. 

So now we can grab this call back and remove it from here and remove that third
argument. 

And instead use then and catch or async await whatever you prefer, just as you
learned it throughout this course. 

And that's of course pretty nice because now we can use all the promise
advantages, like promise chaining to escape callback hell, on core APIs like
this one as well. 

One adjustment we need to make though, now since we're using promises, of course
in the ven method, we never get an error, here we just get the data. 

If we would want to handle errors, we would have to add a catch method and then
here we can handle any error we might get when we try to reach that file. 

So that is how we could transform this code to promises now, and they offer if
we now start this server here. 

We again see our file being served here, we see our page being loaded, but now
with the promise based version of this core node module. 

Now just as the new import syntax, it's 100% optional. 

It's not better than the average approach, you might simply prefer it because
you might prefer promises, especially if you chain multiple promises for
example. 

And therefore this is definitely all the feature which I didn't want to hide
from you and which I just wanted to show you here. 

---