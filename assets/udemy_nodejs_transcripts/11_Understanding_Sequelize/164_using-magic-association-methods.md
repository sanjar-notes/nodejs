## 164. Using Magic Association Methods

<strong><em>no description</em></strong>

From now on all new products that are created should be associated to the
currently logged in user and for now, this will only be this one dummy user. 

That means that if I'm in the admin.js controller, here when we create a new
product in post add product, we'll not create the product like this anymore, we
need to pass in extra information regarding our user that is associated. 

One way of doing this is that we set this new user ID field we got, keep in mind
user ID was added as a database field because we now have a relation set up and
we set this to request user ID, keep in mind that request user is the sequelize
user object which holds both the database data there for that user as well as
the helper methods. 

So this should create new products with that user being associated to it, let's
test this. 

Let's go back to add product and simply enter some dummy values here for now,
seems to work, we get no error here and if we look into our products table by
clicking on this icon here, we indeed have the user ID stored here. 

Now we also have one tiny problem or thing we can improve at least. 

We manually fetch the user id and this is not a lot of work here but there is a
more elegant way of setting this so that we don't manually have to set the user
ID. 

We can use another cool feature of sequelize, we can use our user object as it's
stored in the request and always keep in mind, this is a sequelize object with
all the magic features and there we'll actually have a create product method. 

Now where is that coming from? 

Well it is something you can get from the official docs if you read through
associations. 

There you'll learn that if you set up associations, sequelize add special
methods depending on the association you added and for a belongs to has many
association as we did, sequelize adds methods that allow us for example to
create a new associated object. 

So since a user has many products or a product belongs to a user as we learned
or as we set it up in app.js, since we have that relation defined, sequelize
automatically adds a create product method to the user. 

Create product because our model is named product and create is then
automatically added at the beginning of the method name, that is some magic done
by sequelize. 

So create product is available and there we simply pass in the object with the
product data that can't be inferred by sequelize so basically anything but the
user ID and the timestamps and then we can chain our then and catch block here,
just as we did it before. 

The rest doesn't change but this now automatically creates a connected model. 

So if I now save this and I add a new product, this still works and if we have a
look at our database and we refresh the products table here, we see we also get
the user ID here even though we did not set it explicitly. 

Now this is done by sequelize with this magic way of connecting it and that is a
really cool way of using associations in sequelize and making sure that our
models know about each other. 

---