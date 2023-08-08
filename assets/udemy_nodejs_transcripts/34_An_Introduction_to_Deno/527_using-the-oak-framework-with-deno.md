## 527. Using the Oak Framework with Deno

<strong><em>no description</em></strong>

<v Instructor>Now, throughout this course you learned</v> how you can process
requests with Node.js. 

And you saw that it isn't too much fun if you do this all on your own without
any extra framework. 

The code that you have to write could look something like this, for example. 

Now this is Node code. 

But in Deno, or Denos world, it would be pretty much the same. 

Out of the box, if you just used the core APIs, but also if you used the
standard library you would have to do all the requests, processing and the
response, body handling and so on. 

You would have to do all of that on your own. 

You would have to pass incoming request bodies. 

And whilst it's nice to see what happens under the hood, I will not repeat it
here because it's really not that different from what you learned about Node
there. 

Instead, the main takeaway, just as in Nodes case, is that we typically don't
want to do this on our own. 

Instead, we want to do this with help of some frameworks which take care of the
heavy lifting, which take care of the request body processing, and which allow
us as a developer to focus on our core business logic. 

And that, by the way, will be true no matter which kind of web application we
plan on building. 

We can, of course, build two main kinds of web apps, and that would be APIs and
server-side rendered views based web apps. 

So, for example, REST API or GraphQL API apps where you have those endpoints
where you then have a standalone frontend that communicates with the API. 

Or the other use case that you have server-side rendered views with templating
engines and you generate HTML on the server and send that back. 

And therefore you have one frontend, backend unit. 

This is what you learned about in this course. 

You had a look at teamplating engines in that course. 

We also learned about REST APIs. 

And you can use Deno for all kinds of apps. 

Just like you can use Node for all kinds of apps. 

You can also render server-side templates with Deno, and then you can also build
APIs with Deno. 

In this module I will focus on APIs. 

Simply that's a bit easier and allows me to focus more on Deno and not on
overhead-like templating engines. 

But in the end, you can build everything with Deno. 

That's really important. 

No matter what you're building though, as I mentioned, you don't wanna do all
that request passing and so on, on your own. 

So let's now see which frameworks we have with Deno and how they would work. 

In Node.js, we have the Express framework. 

We learned about Express in this course, and Express is a great and very popular
Node framework that takes care of the heavy lifting and allows us, as developer,
to focus on our core business logic. 

In Deno, or Denos case, we have the Oak framework. 

Just like Express, it's a middleware focused Deno framework. 

So learning Oak will be easy if you already know Express for building web
applications. 

Now, it's actually not directly inspired by Express, but by Koa, which is
another framework that exists for Node.js which I haven't covered in this course
though. 

Now if you search for Koa, you'll find koajs.com. 

And there you'll learn that it's a next generation web framework for Node.js. 

In the end you could say that Koa basically has the idea of being a better
Express. 

If you have a look at some code examples here, you'll see that it's also
middleware based. 

It's not too far away from express, but it does some things differently. 

You can check out Koa for Node.js if you wanna learn all about it. 

But in general, Express still is the most popular framework and Koa was inspired
by Express. 

Now, Oak, on the other hand is a Deno third party module. 

And you'll find it under third party modules on the Deno page. 

And here you find a lot of modules that can help you with a lot of things. 

But if you search for Oak, you'll find that Oak module. 

And that's, again, just this Koa, and therefore indirectly Express inspired
framework for Deno now. 

You also just make that clear if you search for Express, find certain frameworks
that are basically Express for Deno. 

Those frameworks might be powerful in the future, but at the moment a lot of
features are missing in those frameworks which is why I'm not covering them
here. 

That's why we will stick to Oak for now. 

Just as with Node and so on, there simply are different frameworks available,
different libraries available which you can look into to solve different
problems. 

The main problem which they tried to solve is always the same though. 

They want to make it easier for you to write your code and they want to take
annoying work, like passing request bodies away from you. 

So if we dive into that Oak module, we get some documentation there on how we
use it. 

And we can follow this basic code here, we can implement this basic code snippet
here to handle incoming requests, and send back responses with the Oak module. 

Now, the most important difference to note at this point here, is that we have
no package.json file and that we don't have a tool like NPM for managing
dependencies. 

With Express, we had core modules, which we had to import. 

But which were installed together with Node. 

And we had third party modules, like Express, which we had to install with NPM
Install. 

Right, that's what we did over and over throughout this course. 

We had to manage dependencies for our project. 

With Deno, this concept does not exist. 

Because there, with Deno, you have these URL imports. 

So you never install anything locally, you never manage local dependencies like
this with Deno. 

Instead with Deno you really just reach out to a web server, to a file on that
server, and you can install it from there. 

Now, you can still manage some versions by including them in the URL from which
you're importing, but you don't have a dedicated package management file as you
do have it in Node projects. 

And it's up to you whether you prefer this approach or whether you prefer the
Node approach. 

Either way, I'm going to copy this code here and replace my app.ts code with it.


I'm also going back to my extensions and I'll enable the Deno extension again to
ensure that I got good IDE support. 

And now what I'm doing here with this code snippet is I'm importing the
Application constructor function or clause, as it seems, from this URL. 

So from this third party module file. 

And then we create a new app by instantiating it. 

We register some middleware with the use method, that's quite similar to
Express. 

The middleware function looks a bit different though. 

Instead of getting request, response, and next here, we get a context, but also
a next function. 

I can already tell you that. 

But we get the context, and the context holds a reference to a request object,
but also to a response object. 

So request and response is basically summarized in one context object. 

We can use the response object to, for example, set the body of the response,
which then will be sent back automatically. 

And we need to listen, overall, to start up that server here with some top level
await, as you can see. 

With that, if we now run this file with Deno run, we again need to give it
network permissions with allow net. 

And now this will spin up a server. 

First of all, of course, it compiles the file and it will download this package
and all the dependencies. 

For me it doesn't do this again, because I did it before already, so the package
was already cached as I mentioned earlier. 

And now, with that, if I visit localhost 8000, I see Hello World. 

Localhost 8000 because that's the port being specified here. 

So, this is now a new Deno app, now using the Oak framework for handling
requests and sending back responses. 

And the idea, again, really just is that we can focus on our core work, on our
core business logic. 

Now, with that out of the way, let's build a very simple REST API with the Oak
framework. 

And let's then, of course, also... 

Just so that we always have the comparison, compare that to Node. 

And actually I'll start with the Node API. 

So if we build that simple API together, and will then port it to Denos, so that
we really have the best possible way of seeing the differences and of comparing
it. 

---