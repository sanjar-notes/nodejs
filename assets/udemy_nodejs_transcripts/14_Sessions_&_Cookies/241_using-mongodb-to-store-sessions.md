## 241. Using MongoDB to Store Sessions

<strong><em>no description</em></strong>

Now I showed you how to use a session, the problem here is this session is
stored in memory and memory is not an infinite resource. 

So for development, this is fine but for a production server, this would be
horrible because if you have thousands or one hundred thousands of users, your
memory will quickly overflow if you store all that information in memory. 

You don't want to do that, from a security perspective, it's also not ideal. 

So we want to store sessions differently and on the express session
documentation, so on the docs, on the github page of that package we're using,
if you scroll down to the end, you will find a list of session stores you can
use and basically all kinds of databases are supported. 

You could store it in files though that might not give you the best performance
and we will use mongodb because we are already using that right and for that,
we'll use the connect mongodb session package here, so we'll install this
package now and register this as a store with which we can work. 

So back here in our project, let me quit the server with control c and let's
first of all install that package with npm install --save connect
-mongodb-session and this will download this package which we can use to let our
express session package store data in the database. 

So now it is installed, we can restart our server and now let's go to app.js
where we do initialize our session, here we do configure the session and this is
also where we need to configure our store. 

Now to set up that store, first of all I'll import mongodb store, you can name
this however you want and I will require connect mongodb session. 

Now this actually gives you a function which should execute to which you pass
your session, so this session object you're importing from express session is
passed to a function which is yielded by required connect mongodb session and
the result of that function call is stored in mongodb store. 

Now with that, you can initialize a new store, store it in a constant named
store maybe, that name is up to you and you execute mongodb store as a
constructor because this function happens to yield a constructor function which
we store in mongodb store. 

To that constructor, you pass some options and now which options could that
database store require? 

Well it will require a connection string because it needs to know in which
database, on which database server to store your data. 

Now we have a connection string down there, so I'll copy that entire url and cut
it actually and I will store it in a constant up here, I'll name it mongodb URI,
all capital case to signal that this is basically a constant value which I'll
reuse and then here, I will use my mongodb URI and I will also use it down
there. 

Please note that the session now will also be stored in a shop database, you
could use a different database but then you need to use two different urls, I'm
fine with using the same database. 

I will define the collection though and you need to to define the collection
where your sessions will be stored and I will name it sessions but the name is
up to you, you could name this however you want. 

Now you could also add more information, like for example when this should
expire and then it can be cleaned up automatically by mongodb but I will set it
up like this and now I have my store added here and when I saved, I get an error
actually. 

This can be fixed by removing that retry writes here at the end of the URL,  if
you do that, it should work. 

So now we get the store set up here and now we can use that store as a session
store and to use it, we go to the place where we initialize our session down
there and we add another option, the store option and we set it equal to our
store constant or whatever you named the constant where you store that
initialized mongodb store and with that, your session data will be stored in
there. 

So if I now go back to my page and I do click that login button again, I got a
new session, a new session cookie and that session will now be stored in mongodb
and we can of course validate that by starting mongodb compass to look into our
database. 

There if you look into your shop database, you will find a sessions collection
and in the sessions collection, you'll find a session with an ID and in that
session, you'll find that information like is logged in and some information
about the cookie which belongs to that session, also you find the expiry date
that was set by default. 

So this is how sessions are now stored and this is how you should store them for
production, use a real session store, don't use the memory store which is less
secure and which also is less unlimited or which will reach limits when more
users use your app. 

But with that sessions are a powerful tool for storing data across requests
while still scoping them to a single user and not sharing the data across users
because now as you saw, different users have different sessions but this is now
a great way mostly for managing authentication but you could also store
something like the shopping cart in a session. 

We are storing it in a database which is also a decent solution but you could
store it in a session and therefore indirectly in the database I guess, in the
session database collection but you could use a session for something like this.


So in general, use a session for any data that belongs to a user that you don't
want to lose after every response you send and that should not be visible to
other users. 

---