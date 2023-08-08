## 39. Wrap Up

<strong><em>no description</em></strong>

So let's sum this module up now. 

First of all we had a brief refresher on how the web works and in general, it
looks like this, client so the browser sends a request to the server, the server
does some magic, reaches out to a database, works with files, sends back a
response, can be html, can be something different and sends it back to the
client, the browser which then can display that and that is the entire flow we
also saw in this module. 

Now nodejs is the part that runs on the server and regarding its lifecycle,
there is one important concept and that is that so-called event loop. 

Nodejs code runs in a non-blocking way which means we only register a bunch of
callbacks and events and nodejs will eventually trigger that code once a certain
task is done, so that the javascript threat is always free to handle new events,
new incoming requests and stuff like that. 

And node program can exit if there is no more work to do but on a server, this
well should at least never happen because create server registers an event
listener for an event which is never done, if a new event is triggered, so if a
new request is received, this does not mean that node unregisters the event
listener instead we keep on listening for more requests and that is of course
how a server should behave. 

So it's this cycle that's important to understand and that we have this loop
which always keeps on going, keeps on waiting for new events and which does
something when some event happens and then basically dispatches some actions to
the operating system you could say for example and then again frees up the
threat. 

Now this also involves a lot of asynchronous code which we saw with all the
callbacks. 

The javascript code should be non-blocking, so we have this callback and event
driven approach where we are able to register some code to be executed in the
future instead of running right away and blocking the main threat because this
has to be avoided under all circumstances and nodejs is built around that
concept of avoiding this issue. 

We also saw how to work with requests and responses the nodejs way. 

We saw that we have to parse the requests data which arrives in chunks and that
we can use this concept of streams and buffers which I explained and that we
should avoid sending double responses so that after res end, you must not send
another response and this can happen easily if you forget about that
asynchronous nature and that a line of code you write might not execute
immediately. 

So depending on where you write it, if it's in an event listener, it will not
execute immediately. 

That is what I mean and that is what is important to keep in mind here. 

We also learn that nodejs is all about using it's built in functionalities and
whilst there are some global variables or objects or functions we can use, this
also means that we should use its core modules. 

Core modules are things like the http, the fs or the path module, there are more
and you can learn all about them in the official nodejs docs of course, we'll
also use quite a lot of them throughout this course and these core modules give
us a couple of different functionalities that allow us to basically do whatever
we ever could want to do on a server like create a new server with the help of
the http module. 

They're imported via the require syntax and we can only use them in the file
into which we import them and if we want to use them in two different files, we
have to import them in both files separately. 

Now that leads us to the node module system and this basically works with the
help of this require keyword which pulls some functionality from one of our
files if we start with slash or ./ or from a core or third party module, we
haven't used any third party modules thus far but we'll also do that soon and it
basically pulls in whatever we export there and stores it in a new variable or
constant as we did it in this module. 

And export is an important keyword here, we do export with the help of
module.exports or for multiple exports with the export shortcut I showed you in
the last lectures. 

So this is what we learn in this module and I know that this was a lot of theory
or nitty gritty stuff about nodejs. 

Doesn't look too easy and beautiful but it'll get way more beautiful from now
on, it is super important to never forget what nodejs is and does it for you
though because many courses right away start with expressjs which we'll also use
starting soon and therefore you never really learn what's happening under the
hood which is sad because this is important and makes you a better node
developer. 

But with that, let's move on. 

---