## 4. Installing Node.js and Creating our First App

<strong><em><p>We know what NodeJS&nbsp;is about - let's now see it in action. For that, let's install Node.js and create our first little application in this lecture.</p></em></strong>

So we want to get started with Node.js and for that we first of all need to
install it. 

To do this, visit Node.js dot org and then there simply download this latest
version. 

In my case, that's 14.11. 

It will change over time. 

When you're watching this, you might see a higher version here. 

It is important to note that these versions will change frequently, but they
don't really bring many new changes. 

It's most of the time just behind the scenes optimizations and bug fixes. 

I will keep this course updated though, as I have in the past, but with that,
let's install this latest version for this. 

Simply download it onto your system and I'm doing this on a mac here on Windows.


It's exactly the same. 

You can download the installer here and then you simply walk through that
installer. 

And again here that is the Mac installer on Windows. 

You have a similar installer and you simply walk through all the steps you have
there, leaving all the default settings which are set up for you. 

You don't need to tweak anything there. 

Ultimately this will then install Node.js on your system. 

This JavaScript runtime, this course is all about and we need Node.js to be
installed in order to execute JavaScript code with Node.js, which of course is
our goal in this course. 

So once this is installed, we can use it. 

And the first and quickest way of getting started with it and of using it is
that you open up your default system, terminal or command prompt on windows. 

So again, here I am on Mac OS. 

So I'm using the built in terminal on windows. 

You would simply open up the command prompt or PowerShell and you can check
whether Node has been installed successfully by running Node Dash V to check the
version of Node JS that was installed. 

And there you should see the version you just downloaded and installed. 

And with that, if that succeeds, if you don't get an error, we know that it
worked. 

Now we can use Node and one way of using it is to enter an interactive mode. 

Node JS offers you the so called rappel TA, which I will come back later. 

You enter this interactive mode by simply executing Node as a command. 

Now this enters a new mode in your terminal or command prompt, and here you can
run certain node commands. 

You can use it as a basic calculator to do basic math there, and you could do
more than that. 

You could run some JavaScript code in there. 

Again, I will come back to this rappel later, but actually this interactive mode
might be nice to play around with Node. 

You're not going to use it to write real Node programs for that. 

Instead, you will use a code editor and store your code in files and then
execute these files with Node. 

So let's do that. 

Now for that, let's quit this interactive mode by pressing control C twice or
control D or typing exit as you see here. 

And once you closed that mode, let's actually create a new project, a new folder
in which we write our first code. 

And I did just that. 

I created a new folder somewhere on my system and I opened it with my favorite
code editor, Visual Studio code, which you can find if you simply Google for VZ
code or you visit code dot Visual Studio dot com. 

Visual Studio code is a free code editor, which is great for web development and
it's available for Mac OS, Windows and Linux so you can use it on any operating
system. 

Simply download it from code dot Visual Studio dot com and then walk through the
installer that gives you to install this editor on your system. 

As a side note, you can use any IDE and code editor of your choice. 

Of course, Visual Studio code is just what I will be using throughout this
course and what I recommend that you use. 

If you don't have another favorite editor. 

Of course, with it installed you can also open your project folder, which at the
moment should be empty with this tool simply by going to file and then open and
then pick the folder in which you want to write your code files. 

Now, if you want to make sure that you got the same look and feel as I do, you
can go to view appearance and there you can control whether or not you see the
sidebar, this activity bar on the left and so on. 

So that's how you can customize this. 

And in addition, under preferences color theme, I am using the dark plus theme
and you can switch to this as well if you want to have the same colors. 

Last but not least, under view extensions. 

You can search for the material icon theme, which is 100% optional, but which
will give you a specific icon look, which you will see for all the discourse in
my project. 

So that's why I will enable this icon theme here. 

For me, using it is optional though. 

And with all of that we got the code editor set up, which we are going to use
throughout this course or which I am going to use. 

And now we can write our first node code in a file for that. 

I'll add a new file in there, which I'll name first dash app JS, dot JS because
of course it will hold some JavaScript code in there. 

We can now write JavaScript code which can be executed by Node JS and a very
simple first code snippet we could write here is a simple console log statement
which logs something to the console where we say hello from Node JS for example.


This is code which would run in the browser. 

It will also run if we execute it with Node.js. 

Now to executed with Node.js, we need to execute this file here with Node.js. 

And for that, the easiest way of doing that in Visual Studio code is that we go
to terminal, new terminal. 

This opens your default system, terminal or command prompt here, integrated in
this IDE and already navigate it into this project folder. 

And then we can run this first app JS file by running node and then first the
DASH app. 

JS So simply add the file name after node and then you will not enter this
interactive mode, but instead execute this code file this JavaScript file with
node JS and therefore you should see hello from Node JS here. 

Now that was a nice first example, but we can do more with Node and to right and
at least a little bit more realistic or more fancy application. 

We can also try writing some output to a file instead of the console. 

And for this we'll leverage one of the built in functionalities Node.js offers,
and that would be the file system functionality which enables us to work with
the file system for this. 

We first of all have to import it into that file to let Node know that we want
to use this functionality. 

And the syntax for that is that we call require a function made available by
Node JS and we want to require the FS module, which is one of node's core
modules shipping together with Node JS. 

And I will come back to this import syntax and to the node core modules in
greater detail later. 

For now, we just call this and we store the imported file system functionality
in a simple constant here. 

And then we can use this file system to call right file sync, which is a method
made available by this file system object which we're importing. 

And this method here will write a file to our harddrive. 

And the argument it wants is the path to the file, including the file name. 

And here we could name this hello dot text. 

And then the second argument is the content of that file. 

And here we could store hello from node js again. 

So now this is our code here. 

I am writing to a file by leveraging the file system module offered by Node.js. 

And if we now save this file and then run node first edges again, we should find
a hello text file next to our script file which contains this content, and that
is how we can use Node.js. 

Now, obviously, we're just scratching the surface at the moment. 

We just learned about a brand new syntax, which you don't know from the browser,
and therefore we are going to dive way deeper into all of that over the next
lectures and throughout this entire course. 

---