## 180. Installing the MongoDB Driver

<strong><em>no description</em></strong>

So with the mongodb server up and running, let's add the mongodb driver which
simply is a package we can use to connect to mongodb. 

For SQL or MySQL, we used MySQL too and also sequelize. 

Now in my case here or with mongodb, we'd run npm install --save and then it's
just mongodb and this installs the official mongodb driver which we can use to
connect to mongodb. 

Now with that installed, we can start using it and we can start using it in the
first file that gets executed when we bring up our server which would be the
app.js file of course. 

There we basically already do some database set up with sequelize and we can get
rid of all of that. 

We did create a default user here but we did this in the MySQL world, so we'll
start from scratch basically, we can get rid of all the associations and so on
we set up here so let's get rid of that. 

Therefore we don't need these imports anymore, let's get rid of all of them
including sequelize from the util database folder and with that all removed,
also here where I used my user model to find the user by ID, I'll at least
comment this out for now so that we really have a lean app.js file and now I'll
go to my util folder and there, the database folder and I still want to connect
to a database here but that will no longer be sequelize of course. 

So let me clear all of that here too and let's now set up some code that will
connect us to mongodb. 

Now for that, I'll first of all import mongodb here, so I'll set mongodb equal
to requiring mongodb, this gives us access to the mongodb package. 

In there, we can extract a Mongo Client constructor by simply accessing mongodb,
the thing we're importing and then Mongo Client, with a capital M and C, the
constant here can be named whatever you want of course. 

So now with that, we can use that client to connect to our mongodb database and
we do connect by running Mongodb Client and Mongo Client connect, like this, so
this is all we need to do to create a connection to mongodb. 

Now connect here simply takes a url to connect and that url is exactly that url
you're have in the connect modal here on the mongodb Atlas cluster page, so you
can copy that and paste it into here. 

Now one important thing, you need to make sure you are using the right user and
in my case that should be Maximillian, the user you created in your mongodb
cluster under security users and the fitting password for this user, so I'll
quickly insert my password here too. 

With that we got all set update that we need to establish such a connection. 

Now the connect method here actually returns a promise, which either fails or
throws an error if the connection fails and in such a case here, I of course
want to output my error here so that we can diagnose it or we have a successful
connection, so here I can say console log connected. 

And with that, we have a file which when we execute, it would connect to
mongodb. 

Now of course you want to execute this together with app.js, so here we are we
bring up our server or actually we're not doing this right now but where we will
soon do this again, here I also want to connect to my database. 

So to do that, how can we achieve this? 

Well what we can do here is we can wrap our connection code here into a method
and I'll simply create a method by using const here and I'll name it mongo
connect, this will be an arrow function and inside of that arrow function here,
I will then execute my mongo client connect code like this. 

I also expect to get a callback here and I will call that callback and pass
result into it here inside of my then block once we did connect here because the
result I can already tell you this will be the client, so basically a client
object which gives us access to the database. 

And then here all I need to do is I need to export mongo connect, this function
here. 

Now with that exported, we can go back to app.js and import that here, so here
I'll also name that mongo connect but that name is totally up to you and I'll
import from the util folder and there, the database file. 

There I will import my mongo connect constant which will be a function because
I'm exporting a function here. 

So in app.js at the bottom, I will execute mongo connect and remember here, we
have to pass a callback so a function that will get executed once we connect it
and here I will get access to the client object. 

So in here, I will run app listen and bring up my node server because I want to
do that once I know that I connect it to the database and I will also console
log my client here so that we can have a look into that. 

With all of that, let's run npm start and bring up our server and the problem I
now have is simply that when I bring up my server, we do actually register all
our routes here and in the routes files, we dive into our controllers and in our
controllers, we are using that sequelize object which simply does not exist
anymore because we're importing the models here and in our models, we require
sequelize and well that simply does all not work as before anymore. 

So in order to make this work, for now to simply see how we connect, I will
comment out my routes here and therefore also comment them out down there. 

So now we got no working routes for the moment but this means that we can now at
least connect and indeed with the automatic restart, this does not look like an
error instead we see connected here and then we see this Mongo Client object
which we got with some details about the connection and this is in the end the
object which we'll be able to interact with, to work with, to well create data
in our database for example. 

So now we are connected but of course our setup is broken now because it still
relies on sequelize which we're not using anymore, we're not even using SQL
anymore. 

So let's now implement mongodb in our app step by step and whilst we do this,
you will learn how to insert data, find data and so on. 

---