## 194. Creating New Users

<strong><em>no description</em></strong>

We get the basic crud operations with mongodb covered, how you can insert, find,
update and delete elements with mongodb and you also learned how to connect to
mongodb. 

Now let me show you how you can now work with relations and for that, let's work
with some users again. 

Now with sequelize, we didn't have an authentication flow and we will not have
one here either but now I want to create new users at the beginning here. 

And for that, I'll first of all work on my user model of course, I'll keep it
real simple but of course I'll again a normal javascript class again. 

So let me create a new class, user and add a constructor and in that
constructor, I'll get a user name and an email  let's say and then I'll just
store this in a name property and in an email property. 

And you could add more, you could work with this however you want. 

I'll then add a save method to be able to save that user to the database and of
course I'll also add a static method for finding a user by ID and here I'll get
the user ID as an argument. 

Now here's your challenge, try this on your own, pause the video here and try
implementing this on your own. 

Try using mongodb and that central mongodb connection we have to save a user
with the help of the save method and to find it by ID Good luck, after a short
break which gives you the chance to pause to video, we'll solve this together. 

Were you successful? 

Well let's start by first of all importing our mongo database client, so I'll
name this db again and I'll import it by requiring our database file in the util
folder and there I'll use or I'll access get db and I'll name this get db up
here too. 

Now let's start with the save method and there I'll create a new constant, db
and I'll call get db to store my database client in that constant. 

Now on that client, on this constant here, we can reach out to a collection and
obviously this will now not be the products collection but we could name it
users collection if we wanted to. 

Now in this collection, I want to insert one new element here and that new
element will be this, so this javascript object we're in, so an object with a
name and an email property, this is what I want to store as a user for now. 

Now with that, we can again use the then and catch if we want to or we just
return that and let whoever calls this listen to that if there is need for that.


Now we can also work on find by ID already and there I again will get access to
my database client and then I will return db collection users and here, I now
want to use find again to find a specific user. 

We can narrow the user down by comparing the _id and now the important thing
here is of course that you need to convert user ID which I expect to be a string
here to an object ID. 

So let me import mongodb by requiring mongodb like this and now here I'll follow
a slightly different approach which I also already showed before and I'll create
an objectid constant and simply store access to it by accessing it up here but
I'm not calling it, I'm not creating an object in here, I'm just storing the
reference to the objectid class in my objectid constant and then down there, I
can just write new object ID thanks to my constant up there and pass user ID to
it. 

And this should find me all fitting users and I therefore get back a cursor and
now I can call next to get the first and as we know only element that matters to
us, so now I'm returning this here. 

As a side note, you could also use find one if you are sure that you only find
one element and this will now not give you a cursor but immediately return that
one element, so then this would be an alternative and I will use that here but
of course this is something I haven't shown you before, so if you used find and
next, that's perfectly fine. 

So here I'll use find one and now I got two methods in place that should allow
me to create new users and to then find that user. 

Now with that user model added, let me go back to the app.js file and in there I
will import my model. 

So here I'll import user by requiring user from /models/user like that. 

With user imported, first of all we had some code here which I want to comment
back in where I want to find a user with this ID here and then store it in the
request, so I will still use that here, however I'll change the ID in a second. 

First of all when connecting, I also want to add some code to see if a user with
a certain ID exists and for that, I will actually create that user here in
compass. 

So I'll connect to the shop database and I'll create a new collection here,
users and of course this collection name here should be the collection name you
chose in your code. 

I'll create a new collection and then go into that collection and now if you
have a look at your user model, here I'm storing a name and an email for a new
user. 

So if we want to create one behind the scenes in compass, we can insert a new
document here and here is the automatically generated ID and I can enter a name
and you can use any name you want here and of course an email and insert that
document. 

And now it's this ID, this part here between the quotation marks that matters to
me, I'll take that and I'll use that in app.js. 

So here I could now create that user if it didn't exist but of course I now know
it exists because I created it behind the scenes, later we'll add a real
authentication flow where users can sign up by themselves, no worry. 

But here in my middleware where I find a user by ID, I can now search for that
ID and I convert that in the user model, remember that is why I can use a string
here. 

Ok so now I have that in place again, I get access to my user and now we're at
least prepared to set up a connection between our product and our user which we
can use later. 

So let me save that, that should work and in the next lecture let's use that
user object and store a reference to that user in our database. 

---