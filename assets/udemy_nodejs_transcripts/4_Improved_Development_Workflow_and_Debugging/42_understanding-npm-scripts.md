## 42. Understanding NPM Scripts

<strong><em>no description</em></strong>

For this module I'm back in the application or the project we worked on in the
last core section and you can find my state attached to this video so that you
can start right at the same point as I do. 

So it is just the code we wrote over the last lectures and one thing we
constantly had to do in the last section or throughout this course was that we
always had to run node app.js to start our well app or our node application with
that file. 

Now this is certainly ok and not too much work but it actually is possible to
define some scripts in a nodejs project that can help us with tasks like this,
we can also use them for other tasks but especially for this, they can be useful
right now and for that we have to use a feature we didn't use thus far. 

We have to use npm, npm stands for node package manager and it is installed
together with nodejs, so you don't need to do anything, you got this installed
already. 

Now we will also use npm to install some additional third party packages to our
project soon, so packages that are not included in nodes core, so not part of
nodes core modules but we can also use npm to initialize a so-called node
project or to add some extra features to it to be precise because we obviously
already got a node project here but now in this project, in a terminal navigated
into this project, you can run npm init. 

Now this will not delete your code or anything like that, no worries, simply hit
enter and you'll be prompted with a couple of questions here. 

It'll ask you first of all for a name of your package and for now you can simply
translate this with project name. 

Now you can pick any name you want, the part in the parentheses here always is
the suggestion, the default it will pick if you don't choose your own name, so
if I just hit enter here, it will take that default. 

So you can basically do that for all these questions, for the description, you
can leave that empty then it will have no default text either but you can also
enter some text like complete nodejs guide, this is what this course is and then
define an entry point with fs for example. 

You can leave the task command empty, leave that empty, keywords you can choose
some if you want, you can put your name into the offer field though this is also
not required and you can always choose a license but if you don't plan on
sharing this project publicly, this also doesn't really matter. 

So with this what you get is this package.json file and there you also see all
these settings or configurations you just set up and you can of course edit them
there too, so if you had a typo in your description, you can just edit it here. 

Now this is using the json format which is a special kind of data format which
basically looks a lot like javascript objects and it pretty much is based on
that, there is one important thing to understand though, the keys are always put
between double quotation marks and so are the values, except for numbers or
arrays or true or false which are not put between these but that's too much for
now, we can ignore that for now just so that you understand what you got there,
it's basically a configuration file for your project. 

Now what does this configuration file give you? 

Well let's clear the console here, with this configuration file, you'll see that
we got a scripts section there which has one default script that won't do
anything for now, you can add your own scripts here and I will tell you how to
execute them too of course. 

For that, let's add a comma after this test script and add a new script name
which has to be put between double quotation marks and there, let's name it
start. 

Now start is actually a special script name as you will see in a second, so make
sure to type this correctly and then between the quotation marks, you type a
command that should be executed. 

So this is a command which you could also type down there and there we always
have to type node app.js, so let's now put that between these double quotation
marks here node app.js, like this. 

With that save that file and then you can run npm start. 

Start is a reserved name and this will always look for such a start script here.


And if you do that, it will as you can see here just execute node app.js. 

So it does the same you had before but now you can always just well run this
command instead of running node app.js. 

Not that much of a saved characters but a few at least and it's also a good
practice because if you ever share this project, it's pretty common that people
just have to run npm start and that they don't have to guess which of your
javascript files is the entry file. 

So you can quit this with control c of course as always and I mentioned that
this would be a special script name. 

You can add more scripts, also without using a special name, you can indeed
choose any name you want, just make sure to always wrap the name in double
quotation marks and that it does not contain any blanks or whitespaces. 

So for example we could have start-server. 

Now this can also run node app.js, so it will do the exact same as this script
and therefore it's of course redundant but I want to show you something and now
if you try running npm start-server, you'll get an error. 

You basically get an error that is not a known command and indeed it isn't
because just typing the script name here will not work, start just was the
special case as I mentioned. 

Indeed for normal scripts with their own custom names, you have to run npm run
and then your script name, so npm run start-server will now also start the
server. 

Now as I mentioned, this is of course redundant, npm start is way shorter but I
want you to understand how you can add your own scripts. 

Now if you worked with something like angular or react or vue or any modern
frontend development workflow, you will have seen that you use such scripts a
lot to trigger build workflows for your projects for example and indeed you can
use that for all kinds of tasks to want to execute but for now we'll not dive
deeper into that and if you haven't worked with angular or react, it's also no
problem, you will see what I mean later in this course when I explore node's
functionality as a build tool a bit more. 

For now let's just use that npm start script to start our application
conveniently. 

---