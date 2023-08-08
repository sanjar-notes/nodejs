## 59. Installing Express.js

<strong><em>no description</em></strong>

Now back in our project, let's add expressjs and you could also simply create a
new project, make sure to install nodemon though, I will keep using that but I
will get rid of the routes.js file because I will basically create a brand new
application you could say. 

So therefore of course in the app.js file, I have to get rid of that import and
that of course means I'm now missing my route handler or my request handler here
but we'll work on this later. 

So let's now install expressjs by running npm install --save, now why not --save
dev but --save? 

Because this will be a production dependency. 

We don't just use that as a tool during development, it will be an integral part
of the application we ship and therefore, it definitely also has to be installed
on any server or any computer where we run our application once we deploy it, it
is a major piece of our application. 

So let's install it as a production dependency with this command and the name of
the package just is express, so npm install --save express will install
expressjs into our project. 

Now once it is installed, you see an entry was added to the dependencies in our
package.json file here and now we can start using it and to use it, I'll go to
my app.js file. 

and here I will import express, you can name that constant however you want of
course but the package is just called express. 

Now you can also of course group that together with the core module import, I
like to separate my node specific modules and the third party packages and also
my own imports if I have them with empty lines so that you can clearly see
what's what but this is not required. 

So now express is imported and now let's also get rid of that console log
statement here, you can create an express application and store it in a constant
named app, though that name of course is always up to you by running express as
a function. 

So put in other words, the express package seems to export a function in the end
and actually you can see this if you hold command or control in Windows and you
click on the express here, you're taken to the source code and there, you can
actually see that in the end at the bottom of the file, it exports E and don't
worry about that syntax here, this is not javascript file, it's a definition
typescript file but still it exports E which is this function in the end. 

So it exports a function here and therefore we execute it as a function and this
will initialize a new object, you could say where expressjs, the framework will
store and manage a lot of things for us behind the scenes, so a lot of logic is
in this app constant here. 

Now the app here actually also happens to be a valid request handler, so you can
pass app here to create server and if you do that and you run npm start, you
will actually have a running server which of course will not handle any requests
though because we haven't defined any logic that should happen for incoming
requests, app will basically not do anything at this point. 

Well almost, it does one thing for you and that is it sets up a certain way of
handling incoming requests that defines or that is a key characteristic of
expressjs and we'll have a look at that in the next lecture. 

---