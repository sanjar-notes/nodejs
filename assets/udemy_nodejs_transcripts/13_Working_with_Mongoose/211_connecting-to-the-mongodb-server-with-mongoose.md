## 211. Connecting to the MongoDB Server with Mongoose

<strong><em>no description</em></strong>

Now first of all let me show you the official docs, you can always visit
mongoosejs.com and there you can dive into the full docs to learn everything
about mongoose, all its details, all its advanced features which we'll not cover
in this course because this is not a mongoose course, I just want to give you an
introduction to mongoose here, so everything can be seen in great detail here
but that being said, I will walk you through all the core fundamentals in this
course and in this module of course and we'll also keep on using mongoose for
the rest of this course so we'll gradually use more features as we add more
features to our application like authentication and so on. 

So this is how you can learn more about mongoose, now to add it to our project,
I quit my npm start process and then I can simply run npm install --save
mongoose, like that, that is the name of the package. 

Now this will download and add it to our project and then we are already ready
to start using it and the first thing we want to do when we start using it is
that we want to connect to our database and for that, we could use our database
utility file here but actually mongoose does all of that utility management and
the management of that connection behind the scenes for us. 

What we can do is we can get rid of the database.js file and we can go to the
app.js file and in there, simply import mongoose. 

So here let's import mongoose by requiring mongoose, whoops, mongoose like this
and with mongoose imported, we can set up a connection. 

So down there where I used my own mongo connect, I can use mongoose like this
and then there, there is a connect method we can use. 

Now that connect method takes the same url we used for connecting before, so
make sure you grab that url from your backend again and enter that here, make
sure you're using the right user which you set up for that and of course enter
your password and this will now connect to mongoose. 

Then you get a promise here or you can call then at least and there you'll get
the result of this connection but most importantly, you know that at this point
of time you are connected, so here I then also want to bring up my node server
or to be precise, start listening for incoming requests. 

I can also add a catch block here and log any potential error I might be getting
when trying to get connected. 

So with this, we already have everything in place we need to connect and
mongoose as I mentioned will manage that one connection behind the scenes for us
 so that in other places where we start using mongoose from the mongoose
package, we use that same connection we set up here, really convenient of
course. 

And that already leads us to the next thing we have to do. 

We have to move our code over to mongoose now and not to use the mongodb driver
directly as we are currently doing it. 

So we'll again have to rewrite all our models but I hope you still see the
advantage of this, you first of all learn how to use the mongodb driver and you
could of course stick to that and continue using that if you wanted to but now I
will show you how you can move that over to mongoose to focus more on how your
data should look like and less on all the logic for interacting with the
database. 

Now to move over, again I do something I did before, I will comment out my
different routes here in the shop.js and in the admin.js file so that we can
gradually comment them back in as we make them work again. 

Now with all routes commented out if I run npm start, I get an error of course
that util database was not found, in app.js I certainly have to get rid of that
import here where I do import something from that database and the same is of
course true for my models where I do also import something from the database. 

Now the problem is if I comment that out, nothing will work here anymore and
therefore I will simply comment out everything in my models for the moment. 

Now with that, it looks like we are connected because we don't get any error
here, this warning can be ignored and therefore we now are connected to our same
mongodb server but now by using the mongoose package. 

And with that set up, let's start working on all our models and all our code to
make it work with mongoose in the next lecture. 

---