## 58. What is Express.js?

<strong><em>no description</em></strong>

So what is express and why do we use it? 

Well I briefly mentioned it, writing all that server side logic is pretty
complex, just remember what we had to do to parse an incoming request. 

For extracting the body, we manually had to listen to the data event, to the end
event and then create a buffer which we in the end converted to a string and
this was just one type of data we could get. 

If we get other kinds of data, like for example we get a file or differently
structured data, then we would have to write new logic. 

Now expressjs helps us with that, it actually doesn't have a built-in way of
handling or parsing that data but it makes it easy to install another package
that can easily be hooked into our project that will then do the parsing for us
and you will see what I mean in a second. 

We in general don't want to care about all these nitty gritty details, we want
to focus on our code that defines our application, so the thing that really sets
our application apart from other applications, our unique selling point you
could say and we do use a framework for this, for all the heavy lifting. 

A framework is basically a set of helper functions but also a suite of tools and
rules with which we work, so basically we have a clearly defined way or at least
some outline on how we should structure our application, our code and how we
should work with that framework to write clean code and of course, I will teach
you all of that for expressjs in this module. 

So expressjs helps us with that and this is why we will dive into it here. 

Now of course expressjs is not the only package or framework you can use for
nodejs that will help you write better nodejs code and focus on your business
logic. 

Now from one you could of course stick to vanilla nodejs, we only use that thus
far and of course that works and depending on the complexity of your application
or the level of challenges you are seeking, you can absolutely stick to vanilla
nodejs, you can theoretically write everything on your own just with that. 

There also are other frameworks you could use, for example there is adonis.js. 

Now if you ever used laravel for php, this is basically a laravel inspired
framework for nodejs but not from the same creators. 

There also is koa or a sailsjs and there are many more, you can basically Google
for expressjs alternatives and you will find plenty of blogposts diving into the
different alternatives and what their strengths and weaknesses are. 

But expressjs is by far the most popular and most often used one which is why I
will also teach it here. 

The great thing about express is that it's highly flexible and actually doesn't
add too much functionalities out of the box but it gives you a certain way of
building your application or of working with the incoming requests that make it
highly extensible and therefore, there are dozens or hundreds and thousands of
third party packages built for express specifically that you can then easily add
to your node express application without having to configure a lot and this is
probably the real strength of express and of course it also does add some nice
features out of the box. 

So why don't we just install it and take a closer look ourselves. 

---