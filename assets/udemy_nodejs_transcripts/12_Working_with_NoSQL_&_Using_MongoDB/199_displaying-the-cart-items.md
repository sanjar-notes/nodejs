## 199. Displaying the Cart Items

<strong><em>no description</em></strong>

Now whilst we're able to add product to the cart now with this code, let's make
sure we can also display them when fetching them, when going to the cart's page
here, to this page because right now we don't support this page because we still
have that route commented out and we've got no logic to fetch all cart items
anyways. 

So time to go into the controllers folder into the shop.js file where we do have
the get cart route. 

Now this request user get cart thing will not work anymore, so let's make it
work. 

Let's go back to the user model and in there we have add to cart, let's now also
call or add a get cart method, you could name it however you want of course. 

The idea here is that we do indeed return the cart items, so that in the
controller we have the cart items there and we can start outputting them, in the
end what we need as you can tell is just the products, right, so we want to have
a list of the products with the respective quantities. 

Now get cart exists on the user who already has this cart property, this is the
mongodb way of thinking about relations, we don't need to reach out to a cart
collection because there is no such collection, instead here we can simply
return this cart and that's it, this gives us access to the user cart. 

Obviously we could have directly accessed the cart property on the user if we
wanted to. 

You could add more logic to transform it or anything like that but in the
shop.js controller, I can now already call get cart and have the cart therefore.


Now on that cart I can't call get products though but I don't need to because
the products are also already included in the cart or at least their references,
right because what I'm storing in the user model with add to cart is the ID of
every product, this is what we store. 

Now and that is exactly something we can change in get cart, instead of just
returning this cart, it would be interesting to return a fully populated cart,
so a cart with all the product details which we also require. 

And to do this, we of course have to reach out to the database again, so let's
get access to our database client and let's return the result of a database
operation where I do reach out to the products collection now because I have all
the user data, I have all the cart data, now I need to fill it with some live
from the products database and there I want to find all products that are in my
cart. 

Now how can I do that? 

Well for this, we can use a special query syntax mongodb supports. 

In find I can tell, I can say I want to find all products where _id is equal to
and now I don't pass an ID here because I'm not looking for a single ID instead
I pass an object because this allows me to use some special mongodb query
operators of which there are many covered in detail in my mongodb course or in
the official docs of course but we are looking for the $in operator. 

And this operator takes an array of IDs and therefore every ID which is in the
array will be accepted and will get back a cursor which holds references to all
products with one of the IDs mentioned in this array. 

So all we need to do is construct such an array, so product IDs can be
constructed by using this cart items and remember, this is an array of objects
that look like this, so objects that have a product ID and the quantity. 

Now we're only interested in the product ID here, so I'll simply map this, this
is a default javascript function, I'll map this to transform every item in there
and I simply want to return the product ID. 

So what I'm doing is I'm mapping an array of items where every item is a
javascript object into an array of just strings, of just the product IDs and
this is then stored in this new product IDs constant. 

This is then my array which I want to use here to tell mongodb give me all
elements where the ID is one of the IDs mentioned in this array here. 

So this gives me a cursor with all the matching products, now I'll again use
toArray to quickly get that converted to a javascript array and then I'll add a
then method. 

So in this then method, I'll have all my product data for the products that were
in my cart. 

Now of course we want to add the quantity back to every product because that is
something that is important to us, now how can we get that information back into
there? 

Well in this then block, I'll again return a mapped version of my data, so a
mapped version of my products array where every product will be converted a
little bit. 

I'll return a new object for every product which is fine because every product
is an object and I'll distribute all the existing properties, so I want to keep
all the data I retrieved but then I'll add a new quantity property and that
quantity property of course needs to be populated with data I know or I have on
that product. 

Now we of course have the products stored in the cart of this user, so what I
can do is I can use this cart and make sure you use arrow functions here to
ensure that this inside of this function still refers to the overall class, with
normal functions it would not, so use this cart in here, access my items and
simply find the item with that ID at hand here. 

So here I'll have my cart item again and I'll return true if that item has a
product ID toString, that is equal to the product _id to string of the product
we just fetched from the database. 

So this can look confusing but in the end I have an array of products here fresh
from the database, then I want to transform this which I'm doing with map, map
takes a function that executes on every element and products which describes how
to transform this element, here I'm basically returning the new value which is
an object where I still have all the old product properties but I add a new
quantity property and to get the right quantity for that given product, I reach
out to my cart items which exist on that user and I again use a built in
javascript method, find to look at all elements in cart items with this function
here and then identify the one product where the product ID I'm storing in my
cart items matches the ID of the product I have fetched from the database and
since with map I'm going through all these products, this will also vary for
every run. 

Now the last thing is this whole thing here, the whole find method in the end
just gives me the product object, I want to get the quantity though. 

So now from the cart items I have, I extract a quantity for the given product. 

And now with that code, get cart should return products which are enriched with
all the data that is stored in a product's collection because in users in the
cart we'll only store the reference and this is what we need to do in mongodb if
we then have a connection between two collections with a reference, we need to
merge them manually as we are doing it here and with that merging being done
manually here, we can now use that data. 

So get cart should now return a cart with all the information we need, so on the
user we can call get cart and then we know we get back some products here, so we
can delete that here as well as this and then render our view with the products
we fetched. 

Now on that view, so the shop cart view here, we just need to make sure we
output our products correctly because we cycle through them but now due to the
way how we merge this, every product will itself already have the quantity here
and whenever we use .id, we should have _id as you learned. 

Let's see if that works by going to our routes folder and there the shop.js file
and let's add that get cart route again. 

So I'll reload this cart page here and this is looking pretty good, now let me
add a new product, third with some image and some description. 

Now this exists, not in the cart though unless I add it to the cart. 

Once I do that and I go to the cart, we see it there too. 

Now the one thing that is still not working is that if I do add a cart item,
we're stuck, let's fix this in the next lecture. 

---