## 525. Using the Standard Library

<strong><em>no description</em></strong>

<v Instructor>So let's get started</v> with some Standard Libraries. 

And for that, I'm actually going to work with the HTTP library. 

That library will help us with spinning up a web server, and actually here in
the docs of the library, we have some dummy code for doing that. 

So in the end, we're just going to replicate that code, but I'm going to explain
what's happening here. 

Now we see one important difference to note right away and that's the import
syntax. 

Now, I don't just mean the import from syntax, which differs from the const
require import syntax we used throughout this course, but I also mean, from
where we are importing. 

That's a URL. 

As you learned, Node does support the import from syntax. 

I do cover that in the modern JavaScript with Node core section. 

But what Node doesn't support, are URL imports. 

Where we don't import from a local file or a module, but where we instead point
at a file on another server to import that file. 

And that's something Deno does. 

Deno wants you to use such imports. 

The idea with Deno is not that you download everything you're going to use in
your project and store it locally, but then instead, you can import from any
JavaScript or TypeScript file on any server and start using those exported
features in your files. 

This is a core philosophy of Deno and that's, of course quite different to Node.


So therefore, here, if we want to use this standard library, the HTTP library,
and from that library, the serve function exported from the server.ts file, then
we have to go into our app.ts file and add this code in here. 

And this will then do just that. 

It will import a function from this remote file, and of course you can only
import what's exported if we dive into the server.ts file though, we see that if
we search for serve, If we search long enough, at least we have the exported
serve function here, because it's exported here, we can import it with this
code. 

So, this is how we import and we don't need to download or NPM install this,
it's also not built into Deno so it's also not like the file system module,
which comes with Node. 

Instead, it simply sits on another server and this is how we import it. 

Now serve is then a function that allows us to spin up a HTTP server. 

And we spin up that server by calling serve, and then through serve, we pass an
object to configure it and in this object, we can, for example, specify the port
on which we wanna listen. 

And here for development, we could do this on port 3000. 

We do this with the port property in this object. 

Now server then returns a server, which we can store in a constant. 

And now this server, of course could have incoming requests. 

In Node.js, we would now specify a callback function that executes for every
incoming request. 

Deno instead embraces modern JavaScript features for all its core capabilities,
and the server is no exception. 

In this example, snippet, we see how we listen to incoming requests in Deno with
this strange construct here. 

Now for await of, is a JavaScript feature, it's not Deno exclusive. 

Instead, it's a JavaScript feature called async iterable Server, is this so
called asynchronous iterable, which simply means it's like an array full of
promises and it's an infinite array basically. 

So this server generates new promises which we can await like this, and the new
promise, which then resolves, is generated for every incoming request. 

That's what server does under the hood, the Deno server. 

And you could build this entirely with vanilla JavaScript async iterables are
vanilla JavaScript. 

Attached, you'll find a link to the MDN documentation for async iterables, in
case you're interested in learning a bit more about them. 

So, if I copy this code here, into my app.ts file, we'll execute this code for
every incoming request. 

And this is just a Deno's way of sending back a response on the request object
which is generated for every incoming request. 

We got a respond method, which wants an object, where we can specify a body for
the response, which will be sent back by Deno. 

So this is how we listen to requests, then do whatever we wanna do, and then
respond back. 

And one noteworthy thing here, is that we have await here, on the top level like
this. 

This is not wrapped in any asynchronous function as you often needed in Avro
code, instead Deno out of the box supports top level await. 

So that you can use the await keyword outside of asynchronous functions. 

In modern versions of Node.js, this is also supported though, so that's not
really a key difference. 

Well, with that, if we save this, if I now run this file with Deno run app.ts,
it compiles and it will ultimately crash, but before it crashes, you see it
downloads a bunch of things. 

And that happens because of this import. 

Whenever you import from a URL like this, when you execute the code, Deno goes
ahead and reaches out to that server and downloads that file and of course, also
dependencies of that file. 

So, all other files which are imported by that file and it downloads those files
to your local machine, and caches them locally. 

so that when you run the script thereafter, it doesn't have to re-download them
simply to speed up execution time, and to make sure it doesn't exhaust all your
bandwidth. 

With this approach, you can also develop on a plane, assuming that you did
pre-download all the files you'll eventually need. 

Now, after it did all that, it crashes however, and it again crashes because of
a permission error that network access was denied. 

And this makes sense because I mentioned that as part of Deno's permission model
some things, like writing or reading to files, but also network requests are
blocked by default. 

And of course here, we wanna open up a server that has something to do with the
network, and therefore it's blocked. 

So, to make sure that this code works, I now have to run app.ts, with an extra
permission flag but here it's now, not allow write, because I'm not trying to
write to any file instead, it's allow net and that's the permission flag for
granting network permissions. 

And if I now hit enter, this executes the file with those proper permissions,
and therefor now, we can open up localhost 3000 in the browser, and we see
"Hello world there" which is the response we're sending back. 

And this is now also a process that keeps on running just like a Node server
does, until we quit it with Ctrl + C, because of course it keeps on listening
for requests. 

We don't want this process to finish, it should keep on listening, and that's
just what it does. 

Now, just as before, to have that side by side comparison, let's see how we
would spin up a similar server, with Node. 

For that I'm going to quit it here, and now again, going to write some Node
code. 

Feel free to do this on your own first, we'll do it together thereafter. 

---