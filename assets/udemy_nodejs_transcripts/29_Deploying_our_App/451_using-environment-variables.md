## 451. Using Environment Variables

<strong><em>no description</em></strong>

Now after that theory, let's go back to our project and this is our shop, so
this is not the rest API, this is not the graphql API, this is the shop as we
built it and you can find this snapshot of it attached to this lecture. 

Now in there, let's first of all explore that environment variables thing I was
talking about and we can start in the app.js file, what would we control in an
environment variable and what is an environment variable? 

Now environment variables are a concept supported by nodejs where we can pass
certain configurations, certain values into our node application from outside,
so we don't hardcode certain values into our node code, instead the values will
be injected when our node server starts and that allows us to use different
values in development and production and also to conveniently change the values
in production without having to redeploy our entire code. 

And a great example can already be seen here, that connection string here. 

This connection string allows us to connect to our mongoose cluster and
obviously we have some hardcoded values here, the username and the password for
this user and then also the default database. 

If we want to change anything there, well then we have to change it in the code
and redeploy it. 

Additionally if we ever share this code with someone, like I do with you, you
know these credentials. 

Now they won't matter much to you because I change my password after I quit
recording this course but of course in a real application, you can't change your
passwords every time you share the code with some coworker or anything like that
and therefore you want to use node environment variables here. 

Another place where we would want to use one is at the bottom of this file, here
where we set the port where this should start. 

In development, we use 3000 and we can basically use any number that is above
the thousand range but in production, we want to let our server or our hosting
provider set this port because that is in the end the thing, the service that
does open our app to the web and that does configure all the network settings,
so there we don't control the port number but the hosting provider does. 

Another example for something we want to control in an environment variable can
be found in the shop controller. 

There at the top, I have this stripe key, not only is this the development key
which we have to exchange for the production key but it's also not a good idea
to hardcode it in here for the same reasons as it was with our mongoose data. 

So let's use some environment variables and using them is straightforward. 

Now first of all, I'll turn this connection url into a template literal by
replacing the single quotation marks with back ticks. 

Now it's still a normal string but now we can inject values by using dollar sign
curly braces and now here, we can access environments variables on the process
object, this is an object not defined by us but this is globally available in
the node app, it's part of the node core runtime. 

Now on this process object, we have the very helpful env property and that is
now an object with all the environment variables this node process knows. 

There are a bunch of default environment variables but we can also set our own
ones and here let's say I want to use the mongo user environment variable and
I'll replace this text with it. 

Now I also want to replace the password, so here I'll use mongo password and
I'll remove the password here and I will show you how to set these environment
variables in a second of course. 

The database here, we can also replace that with mongo default database,
alternatively you could of course make that whole connection string an
environment variable depending on whether that string changes regularly or just
the values inside of it. 

Regarding the port, I'll also go down and here instead of setting 3000, I'll set
process env port or if that should be undefined, 3000. 

Now most hosting providers or all hosting providers that manage that for us will
automatically inject the port environment variable, so most of the time we can
rely on that being set and for local development, we'll still fallback to 3000
because there, it will not be set. 

Now for stripe, if I move to the shop controller, I also want to use an
environment variable here and I will use process env stripe key here. 

With that I replaced a couple of things with environment variables where it
makes sense. 

Now if you scroll through all the code, you might find other occasions where you
would say ok I want to set that from outside, I don't want to hardcode that but
these things which I now exchanged are definitely important ones. 

Now we do try to read these environment variables in our node code, how can we
now pass them into node? 

Well we do that when we run our node application, with nodemon, we can provide a
configuration file. 

You can simply add a nodemon.json file in your project root folder and there,
provide a json document, opening and closing curly braces. 

In there, add an env object and there you can now set your environment variables
like mongo user, there the value should be Maximillian mongo password, so all
these variables I tried to read in my code and that should be the password you
just well removed from your app.js file and also mongo database and there I will
now use shop like this. 

So now I added the environment variables for my mongodb connection string here
and that should be named mongo default database I see so let's rename it here
too and besides these mongo things here, we could set the port but there we have
a default value, after the two pipe symbols we always fallback to 3000. 

Now for stripe, we also want to inject something and there we should sign into
our dashboard and in that dashboard, go to developers API keys. 

Now here for the server, you will need that secret key and you want to move that
into your nodemon package, so there I named the environment variable stripe key
and that is how I should name it here too, so that would be the value. 

And now that if you run npm start, it should still start and it should still
connect, I get an error that mongo default database is not defined because of
course here in the connection string, it should should be process env mongo
default database just as it is in all the other places. 

Thereafter everything starts just fine and now we have a running application
using these environment variables. 

Now these are still the development values but nonetheless we have that set up. 

Now of course we're not always using nodemon and especially when deploying this
app, we'll not be using it because there we don't want to restart the server on
every change because we will not change the code anyways. 

So what I'll do is I'll add a new start script to my package.json file, I'll
name it start:dev, you can name it however you want, you could just name it dev,
whatever you want and there I will use nodemon and in my main start strip, I
just want to use node. 

This however will now not use the nodemon.json file. 

So if you want to pass an environment variables here, you also got different
solutions and typically when using a hosting provider, you can set up the
environment variables in the dashboard of your hosting provider, that is
something we'll see later but if you're not using that, well then you can as a
simple solution simply take the key value pairs you want to set up and add them
in your package.json file in front of the start script. 

So there you would use mongo user equals Maximillian, like this and you would do
that for all the values you want to pass in. 

So now we can do the same for the password, mongo password, you simply separate
it with a whitespace, mongo password equals this mongo default database equals
shop and the stripe key equals and now I need to get that stripe key here, copy
that, move it here and now we are obviously a very long startup string. 

Again typically we'll not pass it like this but now if I would run npm start it
should still start and connect without issues to the mongodb database because
now we are running this with our environment variables here. 

I also want to highlight one special environment variable which you can set
manually and that is a special one which I just want to log here, on process env
there is the node env variable and now if I quit my server and restart it, you
see undefined here. 

Now again this will be set automatically by hosting providers, you can of course
also set it on your own and hosting providers will set this to production. 

Now if I restart, we see production being logged here and this is a special
environment variable even though it's not set by default because expressjs will
actually use that by default to determine the environment mode and if you set
that to production, expressjs will change certain things and for example, it
will reduce the details for errors it throws and in general, optimize some
things for deployment. 

So you want to set those when running your app in production and again hosting
providers typically do that for you. 

You can always check out the official docs of your favorite hosting provider to
find out if that is the case. 

---