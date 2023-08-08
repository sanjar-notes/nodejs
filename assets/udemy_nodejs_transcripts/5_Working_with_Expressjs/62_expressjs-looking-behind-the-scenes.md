## 62. Express.js - Looking Behind the Scenes

<strong><em>no description</em></strong>

So we now had some basic work with expressjs . 

now let's also dig into the internals of expressjs, at least a little bit. 

Here is the expressjs code repository on github, it's open source so you can
dive into the code and no worries, we'll not do a deep dive analysis but it's
interesting to see how some things work. 

So in there on that github repo, click on lib and then you'll find a response.js
file, now click on it, in that file you will find a lot of code. 

Now let's simply search for send and then an opening bracket and you will see
how the send function, so basically a function we are calling here, how this is
defined internally and this helps us understand it and this by the way is always
a great technique if you want to see what something does behind the scenes. 

and if you need to do something yourself, for example set some header or if that
is done for you and we had that default header of text html right, so let's see
what send does internally. 

It does a bunch of checks to see if we're using outdated versions of that
function which we didn't in this course so let's ignore that and then down
there, it basically analyzes what kind of data you are sending and you see that
if it's a string data, so some text as we are doing it here, that in this case
it sets the content type to html but only if we haven't set it yet. 

So it checks if the content type header is not present yet in which case it sets
it, otherwise it would leave our default. 

If we have other values like a number, a boolean and so on, it would actually
set it to binary or json data. 

So this is just some of the internal things it does and you don't need to go
through the entire code here, it's a bit much and you're using express so that
you don't have to do everything on your own but diving into this can help
sometimes. 

Now one other interesting thing to see is that we can actually also shorten this
code here where we set up the server. 

We can pass app to that create server method but instead we can also just use
app and call listen and this will do both these things for us, something we can
see in the official code if you go into the application.js file. 

In there what we can see is that if we search for listen here, the listen
function in the end just does the two things we did before, it calls http create
server and passes itself, so the app object which we previously also passed to
that passes it to create server and then this in  the end just make sure that
listen gets called on that server object. 

So it internally does the same we did here and this of course save some code and
now we can also remove that http import up there. 

So now our code looks like this and we'll still work fine, it restarts here and
if I reload this page, this is looking good to me. 

So now we're using expressjs and you hopefully get a basic understanding of what
it's doing and why this helps you write cleaner code because now you have a
clearly fine structure, use this middleware funnel and you save code. 

The question of course is how can we now handle different routes as we
previously did where we had slash message and slash nothing and so on and of
course it would be nice if we now could also read incoming requests in an easier
way. 

Well we'll do both and see both over the next lectures. 

---