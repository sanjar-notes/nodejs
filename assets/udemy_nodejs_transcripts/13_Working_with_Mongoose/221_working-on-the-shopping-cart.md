## 221. Working on the Shopping Cart

<strong><em>no description</em></strong>

Ok so now that we're able to relate data and store products that are related to
a user, let's work on that shopping cart and the orders again so that we can do
more to just look at the products. 

Now previously, in our user model in the part which is now commented out, I had
utility methods like add to cart to add products to the cart of that user and
actually it was really useful to have these because that allowed us to move
logic from our controller into the model which is typically where your data
related logic should live. 

So therefore I will re-add it and mongoose makes this really simple, you can
work on your schema so on my user schema here and then there you'll have a
methods key. 

The methods key is an object which allows you to add your own methods by simply
well adding them, Add to Cart and this should now be a function and the
important part is it has to be a function written like this so that the this
keyword in there still refers to the schema and not to something else and now in
this function you can add your own logic and that is exactly what I want to do. 

In this function, I want to add the logic I had in Add to Cart before and tweak
it a little bit. 

So let's grab all that code from Add to Cart, let's add it here and comment it
back in. 

Now the function here should also receive the product which I want to add, that
is something we required in the past as well, so we still will get a product to
that function, this is something we just need to assume because we are the one
writing the code in the end. 

And now in there, we should still be able to use these cart items because our
schema has a cart and then an items array, so this should still work and keep in
mind this will be called on a real instance based on that schema, so really on
an object which will have a populated cart with either an empty array of items
or an array of items with items in there. 

So this code should still work for getting the product index. 

I also still want to control my quantity as before and update my cart as before
by first of all copying it, then I will keep the logic of checking whether we
already do have the product in the cart in which case I'll calculate the new
quantity based on the old quantity and then I'll update my array or if I will
update my array by pushing a new object onto it. 

Now here the thing just is this will not work like that

 

02:41.680 --> 02:47.020

but I can just store the product ID like this and mongoose should automatically
wrap it in an object ID, the quantity can be stored like this however and this
should fit my schema of an item with product in the quantity, so make sure that
the names you used up there in your schema are the names you use down there for
creating new data. 

So with that, I got my updated cart, now I don't need to get access to the
database like this instead here, I will indeed return something but I will not
manually update this instead I will just call this save which should work,
before I do that I just need to set this cart equal to the updated cart. 

Now this should be a utility method that saves itself so where the object saves
itself by using the built-in save method where we update the cart, now let's see
if that works as it should. 

Let's go to the shop.js file and there we have all our post cart method. 

Now I find my product by ID which still should work because mongoose gives us
this function and then I do indeed call request user add to cart which should
now also work because we just added this method to the user object in our user
model, so this should work without any changes hopefully, let's go to the routes
therefore and comment that post cart route back in. 

If I now save everything, let's go to products and let's try add to cart, I do
get some output here and let's now have a look at compass and looking into the
users, there I have my cart, I got my items and I got an ID in there. 

Now that was added by mongoose automatically, it adds IDs for sub-documents as
well but most importantly I got my product ID and that product ID which ends
with 3C6 should be the ID of that product and it is. 

And now let's confirm if that really works by going back again and adding that
same product to the cart again, it still doesn't find the page it wants to load
but that is alright. 

Let's update our users collection now, look into the cart, we got one object
with quantity 2. 

So this is working  and this shows us the power of mongoose, we get a bunch of
nice built-in methods which we also leverage here in our own method which we can
add and which we then can call on our objects and are based on our schema. 

---