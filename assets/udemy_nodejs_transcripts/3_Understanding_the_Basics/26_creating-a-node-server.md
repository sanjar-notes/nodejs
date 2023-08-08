## 26. Creating a Node Server

<strong><em>no description</em></strong>

I'm back in Visual Studio Code, the IDE I'll use throughout this course and this
is again a totally empty folder, I only got my gitignore file in there because I
will use version management here, git you don't need to use that at all, if it
doesn't tell you anything you can just ignore that,  you don't need that
gitignore file. 

So I have an empty folder and again I will now create a new file with command
and or by pressing this icon here and this file can have any name you want but
often you name it server.js or app.js because it is the root file that makes up
your nodejs application, so the nodejs code you will execute on a computer in
the cloud on a server in the end, so I'll name it app.js here. 

Now in this file, I want to create a server through nodejs and thus far in the
first module, we only saw how we can work with the file system, so how can we
now spin up such a server? 

We again need to import some functionality because the way javascript works both
for the browser and nodejs, there is a handful of functions and objects we can
use globally without importing anything into the file but generally, most
functionalities aren't available by default, to not pollute our global namespace
with all these reserved keywords and names basically and also to make it very
obvious in each file on which functionalities this file depends and thus far,
this file does not depend on anything. 

Now there are a couple of core modules nodejs ships with and as you will learn
throughout the course, you can also install third party modules which do not
ship with node but let's stick to the core modules for now. 

Here are a handful of them, now not all core modules, just some and as you can
see there is fs which we already used thus far, there also is path which helps
us with constructing paths, so paths to files on a file system that work on any
operating system because Windows and Mac and Linux use different path formats. 

There is the OS package which helps us with operating system, relevant
information and so on and there are the two topmost packages, http and https and
as you might be able to guess, these two sound very helpful when it comes to
creating a server and working with http requests and http responses. 

And indeed, http helps us with launching a server or also with other tasks like
sending requests because a node app could also send a request to another server,
you can have multiple servers communicate with each other. 

For example you could send a request to the Google Maps API to send some
coordinates and get back an address but that's just an example, let's keep it
simple here and let's focus on the launch a server aspect. 

Https would be helpful when we want to launch an ssl encoded server, so where
all that data which is transferred is encrypted and as I mentioned earlier, this
is something I'll come back to towards the end of the course. 

Now with that. 

let's use that http module and to use it, we need to import it. 

So we basically need to make sure that we can use features from that http module
which nodejs ships with but which still is not available globally by default, we
need to make sure that we can use these features in this file and for this, we
import that functionality. 

We do this by creating a new constant and you could create a var or use let too
but since we'll have some value here which we will never change, we can also
just use a const to make this really clear that we will never touch this again,
we'll use it but we'll not overwrite it and you can give this any name you want
but typically, you keep the name of the module you're importing. 

So I'll name this http but again you could rename this to whatever you want. 

Then you have an equal sign and now we need to assign a value and now there's a
special keyword, a special function nodejs does expose globally, so you can use
it by default in any file you run via nodejs and that is the require keyword. 

Now this is simply the way you import files in nodejs, require either takes a
path to another file, you can also import your own javascript files but we'll
not do this for now, we'll do this heavily throughout the course though or if
you don't have a path to one of your files, you can also import a core module,
like http. 

By the way, a path to one of your files always has to start with ./ or slash if
it's an absolute path, ./ would be a relative path, so this would lead to the
same folder and would now look for an http file. 

By the way it automatically adds .js at the end, you don't need to add that on
your own but you can. 

But this would now look for a local file named http, if you omit ./ or slash at
the beginning, it will not look for a local file, so even if you had a file
named http.js, it would not import this file, let's get rid of it but instead it
will always look for a global module named http and indeed, such a module exists
because nodejs ships with it. 

So now we got this imported and now we can start using functionalities from that
global module and you can see that if you type http., this is how you access
functions or so-called methods and properties on objects in Javascript and as
you can see, this http object which we import from the http module has a bunch
of fields and methods we can execute. 

Most importantly, it has the create server method. 

Now as the name suggests, this is a crucial method when it comes to, well
creating a server. 

And create server, actually if we hover over it we can see it, actually takes a
so-called request listener as an argument. 

A request listener simply is a function that will execute for every incoming
request so let's define such a function. 

For this I'll create a new function with the function keyword, we can name it
however you want, rqListener or whatever you want, the name is totally up to you
and this function has to receive two arguments,  you can see that here if you
hover over that. 

The request listener receives a request which is of type incoming message and a
response object, so in short nodejs automatically gives us some object that
represents the incoming request and allows us to read data from that request and
it gives us an object response which we can use to return a response to whoever
sent that request. 

So now we have to accept these two arguments here and you can again name the
arguments however you want, you just have to keep in mind that the first one
will contain data about the request and the second one will help you send a
response, so I'll name it req and res  and these are typical shortcuts you often
see. 

Now this is a function, rqListener and now we can pass this function reference
so we don't execute it, don't set these curly braces, just pass the name to that
function because this will simply tell create server hey please look for this
function with this name and execute it for every incoming request, so this is
now what we'll set up. 

This function will now run for every request that reaches our server which will
be started by calling create server or almost, one piece is missing, I'll come
back to that. 

Now this is one way of doing it. 

Now you don't have to explicitly create such a function though, you can also use
a so-called anonymous function. 

So here, you can also type function req res, like this, this is now a function
without a name, that is why it's called anonymous and it still achieves the
same. 

We pass that function to create server and therefore, node will execute this
function whenever a request reaches our server. 

This is an event driven architecture nodejs uses heavily. 

You work a lot with such setups or such code snippets where you tell node if X
happens, do Y, so in this case if a request comes, please execute this function.


Now you can also use next-gen javascript syntax and use an arrow function where
you omit the function keyword and just have the two arguments followed by an
equal sign and a greater sign hence an arrow and then the function body. 

This is basically the equivalent to the function keyword approach. 

Ok, so this is our create server callback function as it's called, it's called
by nodejs whenever a request reaches our server, for now let's simply console
log the request object to see what's inside. 

Now if we execute this file, we can do this in the built-in terminal which is
already navigated into this project folder, make sure you go into that project
folder if you are using the terminal outside of that IDE. 

So once you are in a terminal, navigate it in that folder, you can run node and
then app.js, this will execute the app.js file and let's see what it does. 

Hmm, nothing right? 

We don't see console log and that makes sense because we didn't send a request
to the server but we don't even know where the server is, how do we reach that
server, which address does it have? 

Well one important thing is missing, this create server method actually returns
a server. 

So we have to store that in a new variable or constant and I'll use a constant
because I'll never overwrite it, I only create a server once. 

So now the created server is stored here and now we can use that server and do
something with it. 

As you can see we get a bunch of methods we can call and one method is listen. 

Listen now actually starts a process where nodejs will not immediately exit our
script but where nodejs will instead keep this running to listen, that's why the
method is named like this for incoming requests. 

Now listen as you can see takes a couple of arguments, optional arguments, the
first one is the port on which you want to listen. 

Now in production you typically would not fill this out and it would take the
default of port 80 but here on local development, we want to use a different
port and you can also define a hostname. 

Now by default, this will be the name of the machine this is running on, so for
our local machine, this is localhost by default. 

So let's just pass a port, 3000 is a port you often use but you're relatively
free to use any port you want, the thousands port are typically pretty safe. 

And now with that, if we re-execute this, you'll see one important thing. 

The cursor here in the terminal doesn't go back in a new line because this
process here is now still running, it didn't finish, this file execution didn't
finish because we now get an ongoing looping process where this will keep on
listening for requests and this is obviously what you want, right? 

You want to have a web server that keeps on listening for requests. 

Now we can see that in action by opening a new browser window where we simply
enter localhost 3000 and once you did that, nothing happens because we haven't
configured it to return any html page but if you go back to your terminal,
you'll see a lot of output there and that is this line, this is your request
being logged to the console. 

Now let's analyze what happened here in detail and what's inside this request
over the next lectures but these few lines here already give you a fully
functional or almost fully functional web server and this is how you create
servers in nodejs and I know that this can be hard to wrap your head around
because it was for me when I started out with nodejs years ago, it was difficult
to understand that coming from a PHP background you suddenly write your own
server, that sounded like something super complex. 

Well actually it's just these few lines and from now on we'll just have to focus
on doing something meaningful with the request and important, sending back a
response. 

So time for detailed analysis in the next lectures. 

---