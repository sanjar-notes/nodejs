## 460. A Deployment Example with Heroku

<strong><em>no description</em></strong>

Now that we created our account here and we learned that we'll use git, the next
step is on heroku to use its cli, its command line interface and that of course
now is heroku specific. 

On other hosting providers, you might simply be able to drag and drop your code,
let's say as a zip file into some part of the dashboard user interface of your
hosting provider to deploy it. 

heroku just doesn't use such a drag and drop alternative, instead heroku uses
that command line interface which allows you to run your code or to deploy your
code through the command line by typing on commands. 

So let's download heroku cli here, make sure to follow the instructions on the
page that opens in case you're facing any problems, here you also get informed
that you require git so definitely make sure to check that out as well if you
have problems. 

Now I'll go with my MacOS version there and then I will quickly walk through the
installer there and install heroku on my system. 

Once you did install it, the next step is to run this command and you run this
in your normal terminal or command prompt, I'm here in my code, in my node
project but you can run it from anywhere and there I will type heroku login,
this should now work and you can now login with your account data, so with the
same data you used to login on the website. 

Now once you did login the next step is to turn your codebase, so your project
you have been working on into a git repository so that you can add heroku as a
remote git repository and deploy to it, you can do that with these commands
here. 

Now I already have a git repository here so I will omit the git init command and
I will just use heroku git remote -a and then the name of my project and this
will essentially add it as a remote project and also set my remote project url
as a remote repository on this local codebase because this then allows me to run
these commands to create a new commit, a new so-called snapshot which you need
and then this push command to push my code to heroku. 

Now I set heroku as a remote branch, next in your package.json file of your
project, you want to add a new entry, the engines entry anywhere maybe above the
scripts and there add node and now set the version of nodejs you are using. 

You can detect that by running node -v in your project folder or anywhere on
your computer actually and you see for me it's 10.9.0, you might be using a
different version, simply enter it here and this will now use that version when
it installs that on that remote server we are going to deploy it to. 

Now additionally in app.js, for heroku you may want to make sure you are using
compression because heroku does not offer you to set up compression on the fly,
other hosting providers do that, this one does not do it so do it on your own. 

Also make sure that you are not trying to read in our certificate and private
key here for SSL, so comment that out because these files will not be deployed
because we'll not use SSL here, you should not be spinning up your own https
server because we will do that through heroku's managed server or you would do
it through heroku's managed server, so spinup a normal http server instead. 

Now with that changed, make sure that you also add a new file and that is heroku
specific,

 

03:44.310 --> 03:50.810

the procfile without a file extension and there, you simply add web:node app.js
and this will instruct heroku to execute your app.js file when it tries to run
your application. 

Now for different hosting providers, this might differ of course and there you
simply have to check their documentation to find out how you'll let them know
which script or which command they should execute to run your app. 

With all that set up, make sure you add a .gitignore file because this will tell
git which folders it should not actually include in its snapshots and there, the
node modules folder is important, all your third party packages are stored there
and we won't deploy that because that will just increase the size of data we
have to transmit over the wire, instead this will automatically be recreated on
heroku because heroku and that is the case for all hosting providers pretty much
do install your dependencies on the server after you deploy your code because
keep in mind that in the package.json, we of course have a list of all the third
party packages we're using and the versions we need. 

So this will be taken by the hosting provider and it will install all these
packages on the server then  ad that is why we always used npm install --save
because that added such entries to the package.json file which now can be used
during deployment. 

With all that added, create a new snapshot by typing git add . 

and then git commit -m and there any message you want between double quotation
marks and I will simply type prepare it for deployment, close that and hit enter
and now you simply run git push heroku master and you hit enter and this will
now upload all your code to heroku and there also as you see, install all your
dependencies, that is what it's doing now and it should automatically detect
that it's a node application because you have a package.json file, so you should
not be getting any errors here and it will now step by step spin up your server
and install the dependencies and so on. 

Now with that, you can go back to your dashboard and click on overview there and
you should see that succeeded build and you can now click on open app. 

This will open your app in a new tab and most likely, this will not really
succeed and the reason for that is that we deployed our application but now if
you type heroku logs in your terminal, you will see what went wrong and to be
precise in the error message, you will see that it failed to connect to the
database and that makes sense because all our node environment variables which
we rely on, for example to connect to the database are now not set anymore
because in the procfile, we instruct heroku to just execute the app.js file and
this will not pass the environment variables, only one environment variable is
passed by default by heroku and that is actually node env, this will be set to
production, that is something they do for you but all the other environment
variables are not set. 

Now we have to do that on our own by simply grabbing these names and going back
to our dashboard and there on the dashboard, so you want to go to settings for
your app and then go to config vars and there you can now add your own config
vars which are essentially the environment variables that are passed into your
application. 

You simply add them here step by step as key value pairs, so all the data we
previously passed in as part of our start script, we now pass it here as
environment variables, mongo user, mongo password, also of course the default
database, let's add it here, that was shop and also the stripe key where you
should use your production ready stripe key of course as you learned, not the
testing key necessarily, now if you click add, this is added too and now we have
all these environment variables added here. 

Now this alone won't do the trick though, we also need to change something on
our mongodb set up in our case here because we are using that hosted mongodb
atlas solution if you remember and that of course now depends on the database
you are using and there, you have to remember that under security, you had to
whitelist IPs which are allowed to connect, now you need to whitelist the IP of
your running application. 

And the thing about heroku and its basic version here is that we don't have a
static IP assigned to our project, instead it's a dynamic range. 

Now attached you find some resources that help you, for example assign a static
IP. 

If you have such a range, we only can do one thing on add IP address, we can
allow access from anywhere, keep in mind we are still secure by username and
password but still for a better set up, I would recommend that you also ensure
that you assign a static IP. 

As I mentioned, you'll find some helpful resources on that attached to this
lecture or depending on your hosting provider,  you might be using a hosting
provider that gives you a single ID anyways. 

Running mongodb on the same server as your web project is not really an
alternative because a database server is also not very trivial to set up
especially if it should be able to scale and so on. 

Now with that changed, go back to your overview dashboard of your app and
restart your server there by going to more restart all dynos, a dyno is
essentially that virtual server and thereafter let's try reloading our
application here and now there, you should see a running app. 

You should of course also be able to login and all that fun stuff, so
essentially you should be able to interact with it just as you were able to do
with it locally but now it's running remotely and as you can see, it's
automatically served via https. 

Now on heroku in case you want to stick to that hosting provider, you can also
change things, you can use your own domain, your own SSL certificate and all
that fun stuff but this is it for now, this is the essential setup I want to
show you here. 

---