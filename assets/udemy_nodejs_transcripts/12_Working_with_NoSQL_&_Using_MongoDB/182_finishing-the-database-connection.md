## 182. Finishing the Database Connection

<strong><em>no description</em></strong>

So I still want to have a function which I can call to connect and therefore,
this function still is looking good to me in general. 

One thing I want to do is I'll add a throw error here so that I also throw the
error again when we fail here but besides that, I'm happy with having mongo
connect here but I'll change something, I'll not return the client in my
callback here instead I'll add a variable, _db, the underscore is only here to
signal that this will only be used internally in this file but you don't have to
name it like this, you could also have normally, just like db and initially this
will be undefined. 

Now here in the then block, I will store a value in there, I will store access
to the database here and if I leave it like this, what we will do is we will
connect to the test database by default because that is what we specify here in
our connection string. 

So I will connect to shop here and then this will give us access to the shop
database to which we automatically connect and you could also enter the database
name here to overwrite this and connect to a different database than you were
connected to initially but I'll not enter anything and just connect to that
database. 

As a side note, unlike in SQL we never need to create that database or the
tables, the collections in there ahead of time. 

It will be created on the fly when we first access it which is again fitting
that flexibility theme mongodb gives us. 

In SQL we had to prepare everything in advance, at least when not using
sequelize which also had to do that but it did it for us, here we don't need to
do anything, we're just telling mongodb hey connect me to the shop database and
if that database doesn't exist yet, mongodb will create it as soon as we start
writing data to it. 

So that's just a little side note, here I do store a connection to my database
in the db variable. 

And with that stored, now in my callback I don't need to return it but I will
add another function here, I'll name that get db and here I will simply check if
db is set, so if it's not undefined and in this case I'll return db, so I will
return access to my database otherwise I'll essentially not do anything here, so
I'll return undefined, we could also throw an error, no database found,
something like this. 

Now here, I also want to export that so I'll not just export Mongo connect but
instead, I'll just use a different syntax you learned about, exports mongo
connect equals Mongo connect and I'll also have exports get db which equals get
db, like this. 

So now I'm exporting two methods, one for connecting and then storing the
connection to the database and therefore, this will keep on running and I have
one method where I return access to that connected database if it exists and
mongodb behind the scenes will even manage this very elegantly with something
called connection pooling where mongodb will make sure it provides sufficient
connections for multiple simultaneous interactions with the database, so this is
really a good pattern we should follow. 

Now with that changed, we still can connect, one thing I need to adjust though
is in the app.js file where I do connect, I'll not get declined anymore because
we don't return it in the callback anymore, so now we just know we are connected
but there is nothing else we can do. 

But one thing I will be able to do is in product.js where I create my product
model, there I don't just can connect the connection now but I can import get db
and that of course is very useful because that means I do import this by
accessing get db here because this means that I now can call this function to
get access to my database and therefore I can use it to well interact with the
database. 

Now let's use that database connection starting in the next lecture. 

---