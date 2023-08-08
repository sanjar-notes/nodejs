## 226. Clearing the Cart After Storing an Order

<strong><em>no description</em></strong>

So let's clear the cart after storing an order and for that, here once I'm done
with saving the order, I want to clear the cart and one way to do that would be
to go to the user model and add a new method there. 

We can go to the user schema, to the methods key and then add a clear cart
method, so simply a function we can call to clear the entire cart and how would
we do that? 

Well we would simply set this cart equal to an object where we have an empty
array of items and then we just return this, whoops, return this save and that
should be it. 

That updates the carts to have no items in it anymore and we then save this and
therefore we update this. 

With this, let's go back to the shop controller and here once we know that the
order was placed, let's simply call request user clear cart, this method we just
added and then I will return that and move my redirection into a new then block
after the previous one which will only execute once the cart was cleared. 

So now with that, let's save that, let's now also go to products and maybe add
another product to our cart. 

Let's order that cart now, let's click on cart again, no products in cart, this
is looking great. 

Let's quickly check our orders in compass and this new order should now have two
products, that is looking good, one with quantity two, that was our nice book
and one with quantity one, that was the second product and in the users, the
cart is empty. 

So now we got an elegant way of managing orders and the cart through mongoose. 

However let's of course also add the functionality to get the cart in the next
lecture. 

---