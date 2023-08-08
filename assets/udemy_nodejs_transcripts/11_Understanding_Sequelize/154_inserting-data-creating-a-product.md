## 154. Inserting Data & Creating a Product

<strong><em>no description</em></strong>

So time to use sequelize outside of the table creation. 

For this, let's go into our controller files and there let's start with creating
a new product because that will be helpful for later also retrieving them. 

In admin.js, we right now import our product model from the models file and that
is fine because we do still export it there at the bottom, so we should still
import it in admin.js but here in post add product, we will now work with that
product a bit differently. 

What it will do here is I will get rid of that old code we used for creating a
product and instead, I will now create a new product here by calling one of the
methods provided by sequelize and by just typing the dot, my IDE suggests me a 
lot of methods I can call and these methods are all coming from sequelize which
shows its great power and there we got create for example. 

Create creates a new element based on that model and immediately saves it to the
database. 

There also is build which also creates a new object based on the model but only
in javascript and then we need to save it manually, so create basically does it
in one go, with build we get the object in javascript first before we then have
to save it manually. 

I would go for create to immediately store it and now create here simply takes
some arguments that we need to pass per our model definition. 

So I can pass in a javascript object and now here, I even get the
auto-completion by my IDE to assign field values. 

Now I don't need to assign an ID, that will be managed automatically but for
example I need to assign a title by storing the title here, so on the right side
of the colon, I'm referring to my constant, left side refers to one of the
attributes I defined in the model. 

I also have a price which I assign to price, I also have an image url which I
assign to image url, whoops, image url and I also get a description which I
assign the description value I fetched and as I said, this will immediately save
it to database. 

Now just as MySQL did in the last course module, sequelize works with promises. 

So here we can chain then and we can chain catch, we can catch any error we
might get to see what's going wrong and we can now also have a look at the
result we get in case it does not go wrong. 

Now with that if we save this, let's go to our application and it won't work by
default because fetch all is not working because we have no function place to
fetch products. 

So for now, we have to immediately go to /admin/add product to load this page,
the other pages won't work and here I'll store my first book. 

I fetch an image url, make sure it's not a base64 url but a real url pointing at
some jpg or png file. 

I'll assign a price here and I will store a description, this is the first book
I add through sequelize. 

If I click add product here and we go back to nodejs, this seems to have
succeeded here because we get no errors, here we see the SQL statement it
executed, insert into. 

I got an error before that though, that was when I tried to reach the well the
page listing all the products where we failed to call fetch all because that is
not provided by sequelize but thereafter once I was in the right page, inserting
this was executed. 

You see it also executed the syntax where it escapes the values automatically as
we did in the last module and in the return value, this is looking good, it
looks like it did create this book and we can prove that by going to our
products table and refresh this and we should see our book being added there, so
this indeed succeeded. 

So this is how we can add a value through sequelize and this is a huge step
forward of course and I'll comment out my result log here and simply log created
product to not pollute my console as much. 

So now we created a product, let's in the next step have a look at how we can
use sequelize to retrieve data. 

---