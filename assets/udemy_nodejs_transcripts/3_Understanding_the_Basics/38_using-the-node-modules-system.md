## 38. Using the Node Modules System

<strong><em>no description</em></strong>

So let's wrap this module up and right before we finish, let's actually start
wrapping it up by improving our code a little bit. 

We've got all this code in this file and actually typically you write multiples
or work with multiple files and why don't we create a new file that actually
contains our routing logic, so the logic where we check the url and do different
things. 

So I'll create a new file here, routes.js, the name is up to you and I get this
special icon by my IDE, it is a normal javascript file, don't be confused. 

And in that file, I basically want to have my if statements here and my default
response code, so I'll cut all of that out of here so that this is a pretty lean
file and move it into routes.js. 

Now this wouldn't work like that, let me say that, we'll have to tweak that but
this is now the code moved over. 

I don't need the file system in app.js anymore so we can remove that import, we
do need http because we still use that there and we don't need the url and
method here so let's remove that, go over routes.js, add this fs imported on top
and now start working with that. 

Now what do we need to do in this file? 

We somehow need to be able to connect app.js to routes.js, right because we need
to be able to send our incoming request to that file so to say. 

And for that, let's create a new function, I'll name it request handler and we
can either create a function like this, it should receive request and response
as arguments, just as this function does because we'll effectively replace that
function or we use an ES6 function, storing it in a constant, request handler
which looks like this. 

Bit of a strange syntax if you've never seen it before but we're essentially
creating an anonymous arrow function which we store in a constant and this
therefore is the function name. 

Now here we again receive request and response and in that function, we now move
all that code because that code obviously uses the request and response object,
so we need to have them available as local variables and we do now because these
arguments are now named this way. 

We also use url and method, so we need to re-add these constants by getting that
data out from the request, request url and request method and now we just need
to export this handler. 

We're importing with this require syntax but how are we exporting in nodejs? 

There are two ways of exporting, the first one is to go at the bottom and add
module.exports, this is another keyword or object which is exposed globally to
you by nodejs which has an exports property and we can assign a value to this,
like our request handler, so this constant which holds this function, it's now
stored in module exports. 

And since this is a global object exposed by node, node is actually able to work
with this and we can now import from that routes.js file by requiring it and
node will look for module exports and see if something was registered for this
file here and we do register something in module exports, the request handler
and you can register anything here. 

You can add a new javascript object with multiple key value pairs, whatever you
need, here I'll just register my function. 

So now I can go back to app.js and import my routes, the name of that constant
is up to you, by requiring it and since this is now not a global module, we
don't just type routes, instead we want to add a local path to it with ./ and
you can omit .js because nodejs will automatically attach this at the end. 

You can add it though but I'll just type ./routes separated from the core
modules to make it really clear that this is a custom file and now node will go
ahead and look for a routes.js file in the same folder as app.js which it will
find and in that file, it will look for module exports and see what's registered
in there and now we export that request handler method and now we can use that,
it will be stored in that routes because we assign whatever is exported from
that file in that routes constant, so this routes constant will ultimately hold
this function and now we can use that here as a handler, routes. 

Don't execute it, so no parentheses, just pass the name telling node hey please
execute the function that's stored in routes for incoming requests. 

And now if we save that and we restart the server and we reload this page, this
is looking good and this is also looking good, we should have tests stored in
message.text and we do. 

So now we simply split our code over two files, having one file which is very
lean that just spins up the server but and that's important, that also creates a
connection to another file through that import and through that export where we
export our request handler function here. 

This is how that works, now one important note about nodes module system, the
file content here is actually cached by node and we can't edit it externally, so
if we somehow would define routes as an object and we tried to add a new
property on the fly here, this would not manipulate the original file, so this
is basically logged, not accessible from outside, we can only export stuff that
we can now read from outside. 

Though you could have functions which you export that start changing stuff
inside of that file but let's not make that too complicated for now, we'll see
all of that throughout the course obviously. 

For now we have that connection, there's one other syntax you could use, instead
of module exports, sometimes you export many things and you could do that by
having an object which has like the handler key and that is my request handler
function and then also it has some text key which is some hardcoded text in this
case, now we would export two things and that is how you can group that or
separate these two things and still have one export being managed here which is
the most you can have and now in app.js, routes would be that object and not
that function. 

So here we would have to access the handler property, so this property which
holds the function reference we want to use and we could also simply output
console log routes some text here. 

So this is how we can have multiple exports in one file, now you see some
hardcoded text here from this console log and we still have the same
functionality as before. 

Now there also is a different way of exporting multiple things, besides this
code which you can of course use, you can also have module.exports.handler
request handler and then also module.exports. 

some text, some hardcoded text. 

Now it might look different but we still only have one export, we still have
module exports which bundles all the exports but we explicitly assigned the
different properties like this, so this is basically equivalent to this code. 

If I now save this and restart my server, we see some hardcoded text and if I
submit this, it also still works. 

Last but not least, there is a shortcut for this syntax, you can now omit module
and just write exports, this is simply a shortcut supported by nodejs, not some
general javascript magic, it's just an explicit shortcut supported by nodejs
where now we also have multiple exports being merged together into one export,
so therefore again when I execute this, we see some hardcoded text and some last
value being submitted here still works and still ends up in message.text. 

So this is how we can connect multiple files by exporting either one element,
one function as we had it initially with module.exports equals request handler,
right this is what we had initially, let me comment this out with two slashes in
front of it or module exports pointing at an object to combine multiple things
or using module.exports.handler equals request handler and module.exports. 

some text equal some text or again, this shortcut which is the same as this,
just with this shortcut offered by nodejs. 

So this is how imports and exports work, how the module system works and we'll
work with a lot of files throughout the course so this is important to
understand. 

With that out of the way, let's now finally wrap this module up. 

---