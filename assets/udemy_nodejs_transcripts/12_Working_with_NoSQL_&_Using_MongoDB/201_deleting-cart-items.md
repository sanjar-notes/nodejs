## 201. Deleting Cart Items

<strong><em>no description</em></strong>

We're nearing the end, let's make sure we can also delete cart items now. 

For this I'll first of all get rid of that code I previously had for updating
the cart, we outsourced this into our cart model for now and now let's work on
the post cart delete product action here in the shop controller. 

I of course want to be able to delete items from the cart and to delete items
from the cart, the user model is again a great place to work on. 

There I'll add a new method, delete item from cart, the name is up to you and I
only need the product ID here to remove the entire product from the cart. 

With that ID passed, we can create a new constant, updated cart items and first
of all copy all existing cart items, again with this spread operator. 

However we can even take an easier route and just use this cart items and then
the built in filter method, this is again a method provided by vanilla
javascript. 

Filter allows us to define a criteria on how we want to filter the elements in
that array, so in this case the elements of the items array and then it will
return a new array with all the filtered items, so all the items that make it
through the filter. 

The filter is a function here which runs on every item and then we return true
if we want to keep the item in the new array or false if you want to get rid of
it. 

Now I want to keep all items except for the item which we're deleting, so I will
look into each item and these cart items are objects of the structure we define
up here, they are objects with a product ID and a quantity. 

So I'm looking for the product ID now, down there I'm looking for the product ID
and if that is equal to the product ID I'm getting here, then I know this is
element I want to remove, so I'll check for the opposite because remember, I
return true here if I want to keep the item, so I want to return false if I want
to get rid of it. 

So this should return false if I want to get rid of it and I want to get rid of
it for this condition. 

As before with toString, we can guarantee we're working with the right type of
data here and now we have the updated cart items which we just need to save back
to our cart and therefore to the database because these is already are the cart
items with the one item we wanted to get rid of removed. 

So I can simply copy my code from up there where I update the database, like
this and when I say updated cart here, well I simply mean I want to assign this
to an object with an items property because that is what our cart has, right, we
have items in there and items is equal to our updated cart items and that is it.


This now will update the cart to have all cart items except for the one we
deleted. 

So back in the shop.js controller, here I don't need to call get cart instead on
the user, I can call my new method, delete item from cart which you just added,
we can call that here and pass the product ID as an argument and that we can get
rid of all that code and simply redirect once we're done, so let's see if that
works. 

If we now save this, let's go to the routes and add this post route for deleting
cart items, reload this page here and let's delete the second item and this is
looking good. 

It's gone here, no errors here so this is looking good and if I update this in
compass, we see that for this user we indeed well obviously only have the other
items. 

So this worked and that is how we can delete cart items with these. 

---