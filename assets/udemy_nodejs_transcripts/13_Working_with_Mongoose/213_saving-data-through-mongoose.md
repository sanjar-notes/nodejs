## 213. Saving Data Through Mongoose

<strong><em>no description</em></strong>

So we got a data definition defined, we got a blueprint, we got a schema for our
product. 

Mongoose now also works with so-called models and the model is also what we'll
export here, so I can already say model exports and now what I want to export is
mongoose model. 

Now model is a function I call and a model basically is important for mongoose
behind the scenes to connect a schema, a blueprint with a name basically, so
here you give that model a name and that name here would be product. 

Typically you name it here like this with a capital starting character and then
simply just well the name of the entity this reflects in your project or in your
application. 

The second argument then is the schema so in my case that product schema we
defined and this model is what I export because this model is what we'll work
with in our code. 

So with that model defined here, we can now move over to the admin controller
where we have post add product where we do save a new product and there indeed I
want to create a new product and then I want to be able to save that. 

Now for that, we can basically keep the code we have here. 

We still import product from our models folder from the product file because I
do export a model here and we can basically use that just in the way I used it
here. 

One adjustment is required though, to the product constructor we don't pass
multiple arguments like this, instead we pass one argument only and that one
argument is a javascript object where we map the different values we defined in
our schema. 

So here I would map the title to the title and you basically now have to go
through all the fields you defined in the schema, the order does not matter
though since it's in a javascript object, so you then map let's say price to
price, you map description to description and you map the image url to image url
and just in case you're wondering, the part on the right side of the colon, so
title, price, description, image url refers to the data you receive in your
controller action and the part on the left side of the colon refers to the keys
you defined in your schema, so to these things. 

And now with this, this creates a new product based on our model and therefore a
product managed by mongoose you could say and indeed such a product happens to
have or such a model happens to have a save method now provided by mongoose,
that's really important, this is not defined by us. 

In the product model, we define no save method, we did before but this is
commented out. 

So we're not defining a save method, this save method here is coming from
mongoose and then we can indeed call then on that, technically we don't get a
promise but mongoose still gives us a then method, it also still gives us a
catch method we can call and therefore this code should actually continue to
work. 

Let's see if that is the case and let's head over to our application and click
on add product. 

Now I do get an error from app.js because there I of course still use my user
model, let me comment that out and let me comment it out here, let me comment
out that entire middleware, for now we have no user and otherwise all requests
will break for now so let's remove all that user related stuff in the app.js
file, this middleware and the user model import and with that removed, let's try
reloading that add product page and obviously we need to import the route again,
so we should do that. 

Not only the get route but also the post route, so make sure you re-add both
admin add product routes, this was the wrong one, this one is required. 

So make sure you have the get and the post and the product route added again
because we manipulated these two admin controller actions and now with that,
finally if I click on add product, this works and now let's test this, let's
test a test product with some price, some image, does this work? 

Click add product, we get a page not found because we can't load any other
pages, that is ok. 

In the code, I can't see an error but I got created product which looks good. 

And in compass let's refresh by clicking that icon on the top left and I
connected to the wrong url, I'll fix that, therefore I'm connected to the test
database instead of the shop database but theoretically it worked, theoretically
we get a products collection with the product added. 

Now where is the products collection coming from you might be wondering by the
way because we never defined that name? 

Well mongoose takes your model name, so product, turns it to all lowercase and
takes the plural form of that and that will then be used as a collection name,
so this is why our product here has a great impact because it was used for
naming this collection and here we see the data we entered. 

So this is working, that's all great, I will still drop this collection here and
quickly fix my connection settings in app.js at the bottom of the file. 

Here I do connect to the test database, I don't want to do that, I'll connect to
the shop database instead just as we did it before. 

And with this tiny change, if I now go back to my application and I try adding
this again, a book, now let's use that book url I used before, must read and
click add product, now this still works in the same way it did before but now if
I refresh here, my data is saved in the shop database and there in the products
collection. 

So this is looking really good, we're now able to save data through mongoose. 

---