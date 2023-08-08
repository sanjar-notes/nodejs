## 162. Adding a One-To-Many Relationship

<strong><em>no description</em></strong>

What do I mean by association? 

You could also say relation. 

let's say in our project and that is basically our project, we have products,
users, carts and at some point also orders. 

Now if we want to connect all these things on and define how they work together,
then a product would probably belong to many carts because our users will have
carts therefore we have multiple users, multiple carts and therefore a product
can belong to many carts because of course different users can add the same
product to their carts. 

Each user only has one cart though, so this is how we could relate that, a
product also can be part of multiple orders and a user can have multiple orders
because you typically order more than one thing. 

A user can also own multiple products in a sense of this user created this
product, so not own it in the sense of I bought it but in the sense of hey I
offer this product, I created it in the shop. 

This is a rough outline of how we can communicate or relate different models and
this is what we can also reflect in sequelize. 

There I'll go to my app.js file here, let's close the views, I'll go to my
app.js file and before I sync all my data to the database, I want to define my
models. 

So for this I will add more imports and I will import my product model by
requiring this from the models file and there the product file, add a models
folder in the product file and I'll import my user model from the user file in
the models folder. 

With the two models imported, we can relate them and I will relate them here in
the same place where I sync sequelize but before I sync it. 

Here I can basically say that a product belongs to a user. 

Now you can learn way more about these relations in the sequelize documentation.


There, there is a whole article about associations, which kind of associations
exist and how you define them in sequelize and which effect this has. 

I will show you some important implications in this model of course. 

So back to our code, we are now setting up that for sequelize, a product belongs
to a user and this is now talking about a user created this product, we're not
talking about purchases at this point. 

We can also configure this by passing a second argument which is optional, here
we can define how this relationship be managed and very important, we can define
so-called constraints, set them to true and for example say that on delete, so
if a user is deleted, what should happen to any connected products? 

And here we can say cascade which simply means well the deletion would then also
be executed for the product, so if we delete a user, any price related to the
user would also be gone. 

This is totally optional and you definitely need to learn a bit more about SQL
to fully understand your options here, this is beyond the scope of this course
but this can all be done with sequelize and now we got this relation set up. 

You can also define the inverse and say that one user has many products because
one user can of course add more than one product to the shop. 

Now this is optional, you don't need that, you can basically replace belongs to
with a has many call but here I also like to define both directions to really
make it clear how this relation works. 

Now with this being set up, sequelize sync will not just create tables for our
models but also define the relations in our database as we define them here. 

The one problem we have right now is that we already created the products table
and therefore will not override it with the new information and we can ensure
that it will by setting force to true. 

Of course a setting you wouldn't really use in production because you don't
always want to overwrite your tables all the time but here during development, I
want to reflect my new changes so I'll set this to true and therefore after
restarting, we indeed see a couple of statements were executed. 

First of all it dropped any existing tables and then it created a new table,
users with all the set up and then it also creates a new products table and
besides adding all the fields there, it also defined that there is a new field,
the user id field which is an integer and which is a foreign key that references
the ID field in the users table and that on delete, it should cascade and on
update cascade is the default. 

So this is some meta setup in the database which sequelize now also added to
connect our tables there too. 

And if we go to workbench and we right click on our database and set call
refresh all, we see there are two tables now and indeed if we inspect products,
we see that our product is gone because it recreated the table but now besides
created at and updated at that were added by sequelize, there is a user ID field
which was also added by sequelize and this will automatically be populated by
sequelize too once we create products that are related to a user. 

So let's make sure that we have a user because right now that table is empty and
that we then can connect users and products in our app. 

---