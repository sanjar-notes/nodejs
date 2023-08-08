## 161. Creating a User Model

<strong><em>no description</em></strong>

So it's now time to introduce more models and I will introduce a brand new model
before I start working on the cart again, that new model will be my user model
but for now we have no real authentication process, so we'll only work with one
dummy user who doesn't really have to log in, authentication will follow later
in the course but I still want to show you how you could have a user who did
create a product and who therefore is connected to that product and at the same
time, a user should own a cart and that cart will hold multiple products and
this is how we can then overall connect everything. 

So I'll add a user.js file in the models folder and in there first of all, let's
define a user model. 

And this is also something you can try on your own, try to define a sequelize
model with a user that has an ID, the ID should have the same function as it has
for the product model and let's say for now a user also has a name and an email.


Definitely try this on your own, pause the video at this point, we'll thereafter
define the user model together. 

Were you successful? 

Let's define the user model by first of all requiring the sequelize constructor
or class and then also with lowercase s, let's import our own sequelize object
which holds the connections on from the util folder and there, the database
file. 

We can then define a user and store the user in a user constant by calling
sequelize define, I'll name the model user like this and then as an object you
define the structure of the user. 

I want to have an ID for my user and the type here will be sequelize integer, it
should auto-incrementing, I don't allow null values and this will be my primary
key. 

Besides that ID, I'll also have a name and here I'll use a very short definition
where I say that the name will be a string and the email here will also be a
string. 

So this is my user, now we need to export this model with module exports user
like that and now with that being exported, we can start using it. 

And one thing I want to start using it for is that I want to create an
association. 

Now let's have a look at how we do that and what an association actually is in
the next lecture. 

---