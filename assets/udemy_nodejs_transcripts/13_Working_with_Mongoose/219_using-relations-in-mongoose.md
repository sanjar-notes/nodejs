## 219. Using Relations in Mongoose

<strong><em>no description</em></strong>

With the user model set up, let's make sure we can use it together with the
product model. 

Now obviously every product should be assigned to a user, so first of all we
need to change our product schema a little bit. 

A product should also have a user ID field let's say, just as we had it before
in the last module. 

Now a user ID field is of type and now which type is this? 

Well it will be a reference to a user, so this will actually be of type schema
types objectID and now we can set something special here, we can add a special
ref configuration and ref takes a string where we tell mongoose hey which other
mongoose model is actually related to the data in that field. 

We know that we will store a user ID here but just because the type is objectid,
this is not obvious, this could be any object ID of any object. 

So I will add user here and you use the name of your model to which you want to
relate this, so since our model here is named user, I will name it user here, so
I refer to my user model here and with that I got a relation set up. 

This also means that in my user model where I do store the product ID, I can
also add a reference here and refer to product because I know that for every
user in the cart items, I will store products where I refer to some ID and that
ID happens to refer to a product stored or defined through the product model. 

So now we got relation set up with ref, of course you only need this when using
references, when using embedded documents as we do with the cart, you don't need
to do anything because well you use an embedded document, this already has kind
of an implicit relation that is managed inside of one document. 

So now with the references set up, let me also add a required to true here and
now I adjusted my schemas. 

Now with the schemas adjusted, we of course need to adjust our code like in the
admin controller when we create a new product. 

When creating a new product, we also want to make sure we store the user id and
that is super simple. 

We just add user ID here to the fields we pass in the object to the product
constructor and now remember that we did save the user in our request, so I can
just do request user_id like this and this should give me access to the user id
and assign it here. 

Now conveniently in mongoose, you can even just store the entire user object, so
this is really the entire user object not just the ID and mongoose will just
pick the ID from that object, so that's another convenience you got there. 

Let me save my code, let's go back and let's add a new product, a nice book. 

Let's use that image url we used before, let's give it some price, you should
not miss that and click add product. 

Now you see that looks good, it was added and now let's have a look at compass
and see if the user ID was added too. 

So if I refresh there, indeed we see the user id here and just the ID, not the
entire user, just the ID as we want it. 

So this is pretty awesome, this is how we can manage relations through mongoose.


Now let me show you something cool when it comes to fetching these relations. 

---