## 536. Connecting Deno to MongoDB

<strong><em>no description</em></strong>

<v Instructor>Now to a real database,</v> I'll use MongoDB and I do already
cover MongoDB throughout this course. 

I have whole sections dedicated to it, so check out these sections if anything
is unclear about MongoDB. 

It's a no SQL database and we can install it locally. 

On mongodb.com you will find instructions on how to do that, but you can also
try it for free and get started with MongoDB atlas, which is basically a cloud
service, a cloud hosting service for a MongoDB database and you can get started
with it for free. 

Just fill out this form here, create an account and once you did that, you will
be walked through a wizard to create a new MongoDB cluster. 

If you do walk through the creation wizard for the first time, just make sure
that you use the free tier option in all the places where you have a choice. 

Again, I do cover this in the MongoDB course module already. 

Now, once you did create a cluster and you logged in, you'll be greeted with
something like this. 

Now first of all, you should make sure that under database access, you have at
least one user and you'll then need to set a password here, which you memorize
because we'll need that to connect on our fronted application. 

In addition under network access, make sure that you add your current IP address
here to make sure that your local application is able to send requests to your
cluster. 

And once you did all that, we can connect our Deno app. 

To do that, we'll use another third party module because there turns out to be a
MongoDB module. 

Here it is, the Mongo module. 

The Mongo module makes connecting and working to and with a Mongo database very,
very easy. 

You get some basic documentation here but in the end, this is just a wrapper for
the native Rust MongoDB library and Rust is simply a programming language, which
is being used by Deno under the hood. 

So, Deno is built with Rust and you typically don't need to care about this but
here it matters because that means that the MongoDB library for Rust also works
with Deno. 

All you need is a wrapper and this package here, this module here, deno_mongo,
is such a wrapper. 

So, you will just be able to use it in types with code without worrying about
anything else. 

Now, when it comes to using it, we can copy this import here, here you also see
a version being locked in, in the URL, which is always a good idea. 

It ensures that this code will also work in month or two from now. 

So, I will copy this URL here and now with that copied, we wanna use it in the
place where we want to connect to the database. 

Now it's up to you where you wanna do that. 

I'll add a new folder, Helpers and in there add a db.ts file. 

And I'll put my database management logic in there. 

This is an optional pattern but one I'd like to use here. 

So, now I import Mongo client from this Mongo library here in the db.ts file and
you'll now see how we can connect with these lines here. 

And with this line, we then also establish a connection to a database and then
even to a specific collection. 

As you learned in the Mongo course section, MongoDB works with collections and
documents. 

I'll copy these three lines here, over into db.ts and with that we first of all
instantiate the imported Mongo client, then we use this client object to connect
with a URL and now here we need to provide the URL to our MongoDB cluster. 

So, back on the cluster, if you click on connect and then connect your
application, we get that URL. 

So, we can just copy this full URL and then insert it here. 

Now, we need to insert our data for the username and for the password and you
don't need to copy my password, it will be changed when you're watching this. 

So, insert your username and your password here, then you can remove this db
name thing here and just have mongodb.net? 

and then those query parameters and with that the client will go ahead and
connect to this URL. 

Thereafter, we can switch to a specific database by calling database on the
client and that's something I'll do here. 

And I'll connect to the todos database, however, the name is up to you, maybe
name it todo-app, really up to you. 

And I'll also rename this file to, db_client. 

As a side note, the official Deno style guide recommends that your file names
should be, well named like this. 

If you multiple words that you wanna combine together, you should use a
underscore, not a dash. 

In Node, you would typically use a dash, in Deno, they want you to use a
underscore. 

Technically, it makes no difference but of course here, I wanna follow the Deno
style guide, so I'll use db_client. 

Back to the database though, with that we're setting up our database here and
now we want to make sure that we can use this database from outside this file. 

To ensure that this is possible, I'll create a new function here, getDb and I'll
return my database here. 

Now, why am I using this approach? 

I'm using this approach because I'll also wrap the other functionality here into
a connect function. 

The reason for that is, that now I wanna export both connect and getDB and we
can then call connect from inside app.ts for example and getDB from inside todos
to get access to the DB. 

For this pattern to work, I'll just make sure that I set up my DB as a variable
and set the type to database, which is a type you can also import from the
mod.ts file from the Mongo library. 

And then I assign a value here to DB in line 11, instead of the connect function
and we always return the latest DB object here in getDb. 

I use this pattern to make sure that whenever we reach out to the database, we
really are guaranteed to get connected database. 

Now, we can export this connect function and export getDb and now in app.ts, I
wanna call connect. 

So therefore here, I'll go to app.ts and import connect in curly braces from
./helpers/db_client.ts and then simple call connect, maybe here before we set up
the application, wherever you want. 

We need the curly brace import here because connect is a named export and you'll
learn more about named exports in the modern JavaScript with Node section. 

In the end, this is a named export because we have the export keyword right in
front of the function declaration and we're exporting multiple things in this
file by name, because we have multiple export statements. 

So this is how we import connect, we then execute it and this should be it. 

And now in todo.ts, we can also import something from the Helpers folder,
db_client.ts and that something is the getDb function and now we can continue
with that and we can call this function whenever we wanna get access to the
database and then we can use the database to store data, get data and so on. 

So, let's do that next. 

---