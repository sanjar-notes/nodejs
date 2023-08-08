## 364. Creating our REST API Project & Implementing the Route Setup

<strong><em>no description</em></strong>

Now with all of the theory out of the way, let's build our first simple rest API
and for that, I'm in a brand new folder, I only did one thing in there, I ran
npm init and confirmed all the default settings, since I'm using version control
I also added a gitignore file so that I can ignore an upcoming node module's
folder and that is it. 

Now to build a rest API, how do we start? 

Well as I mentioned, all the things you learned are still important. 

We build a node express server just as we did before and also by the way, of
course you don't need to use express, you could build just a node server API but
you have to do a lot of request parsing and so on on your own as you learned it
before in this course and you can use other frameworks too. 

There even are specialized rest API frameworks but we will use express which is
a great all-rounder and therefore I will install as a production dependency with
--save express, we need expressjs to build an API conveniently. 

So this is the first dependency we'll install into this brand new project here. 

Now with that installed, I'll also install another package and that will be a
development dependency with --save dev nodemon because I still don't want to
restart my server manually after every change, so let's quickly install that
package now. 

With nodemon installed, let's go to the package.json file, let's add a start
script in the scripts section and let's execute nodemon app.js here to start
app.js with nodemon. 

App.js does not exist yet so let's add it and in there we'll set up our nodejs
server. 

So what do we do in here? 

Well first of all, I will import express by requiring express like this, then I
want to create my express app by executing express as a function and these are
of course the exact same steps we executed before in this course and last but
not least, we can listen to incoming requests, let's say on port 8080 this time,
not  3000, I'll need to add later for something else, let's use 8080 for now. 

This is a very simple server that we could now start and that will not do
anything of course, it has no routes to find but this is our simplest possible
node express server. 

Now to add some routes and to do something with them, I will also install the
body parser as a production dependency with --save so that I can parse well
incoming request bodies and now let's start adding some routes. 

We could add them in here with app use to handle any method or app get, app
post, app put and so on to handle specific http methods for specific paths but I
will use the express router again and I will also create a new routes folder
which you wouldn't have to do but this structure still make sense, separating
routes and controllers, you just won't have views anymore, the views folder will
not be recreated because we'll not render any views anymore, we'll just exchange
data. 

So in the routes folder here, let's say we're building a simple block or a
simple messaging social network block like application and we have some feed
routes, so like the news feed or something like that where we simply are able to
create new messages, show existing messages and so on. 

So I'll create a feed.js file in the routes folder and in there, we set up our
express router by again importing express into this file too because we need
something from that package in that file and then I create the router by calling
express router as a function and I will export the router at the bottom. 

In-between we can now define some routes and I want to start very simple with a
get route to let's say posts where I serve my posts later on, not right now but
later on. 

So here I have my posts and of course I now need my logic that should execute
when a request reaches this. 

Therefore I'll create a new folder, controllers and in there I'll add my feed.js
file as well, so feed.js in controllers now. 

In there let me export a new function, get posts which of course and that also
does not change gets a request, the response object and the next function it
could call to let the next middleware take over and in there, I want to send a
response and this will be the first part that gets interesting. 

Before we write that code, in my routes feed.js file, I will import my feed
controller by requiring it from the controllers folder and there from the feed
file and I will assign my feed controller get posts function here as the
function that should be executed for this route. 

Now to be able to reach that route, we need to register the route in app.js
which is our starting file. 

So in there, I will import my feed routes by requiring them from routes feed
like this and then all we have to do here is we have to use these routes, used
to forward any http method, we'll filter them out in the routes file then like
with this get function here. 

So we forward any incoming request to feed route let's say or let's say we only
forward requests that start with /feed, again this is logic you already learned
about. 

So now any incoming request that starts with /feed will make it into feed
routes, so into this file and there we handle one request right now, /posts. 

So in total, /feed/posts would be handled right now as long as it is a get
request, this kind of request would get handled by this controller. 

And now let's talk about the response and how we could send a request to that
route. 

---