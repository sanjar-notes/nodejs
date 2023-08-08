## 202. Adding an Order

<strong><em>no description</em></strong>

We're coming closer to the end of this module, only the order part is missing
and I want to include that too because this will show you another way of
creating relation. 

With the cart, we had like the middle way, the cart is an embedded document but
the items on the cart then are a combination of references and extra metadata. 

Now for the orders, this will change. 

So let's work on the orders now and for that I'll go to my shop.js file where we
post the order. 

Again I want to store orders on users, so in the user model, we can add an add
order method and this doesn't take any arguments because the cart which will be
passed as an order or as the data for the order is already registered on this
user, so all I need to do here is I need to add the orders to my user or the
other way around. 

You could also argue that you want to store the orders in a new collection
because you might have thousands of orders and you don't want to embed them all
into user objects because these objects will then get pretty quick, carts don't
get that big but an order history, well often that can get very long so I will
actually work with a new collection here. 

I'll still create order here as a method on my user though, so I'll reach out to
my database client and then reach out to a new collection, orders. 

There I want to insert one new order now and I'll return the entire thing and
that one new order will be well the cart I currently have,  right, that is
essentially what I did before too when I added an order, I added my products in
the order model, we had no special fields for that, we just had our products and
then the quantity of every product and that is still the same I want to add
here. 

So you could say I'll insert one and I'll insert my cart, so this cart which
refers to the users cart. 

I insert this as an order and then when this succeeds, I set this cart equal to
an object where items is an empty array, so I basically empty my cart at this
point. 

Of course I don't just want to empty it here, I also want to clear it in the
database, so we'll also copy that code for updating my user in the database and
I will return that here in this then block and there, I will simply search for
that user and set the cart equal to an object where items is an empty array. 

So now I cleared both in the user object as well as in the database but I also
insert the cart into the orders collection before I clear it and that of course
is the important part. 

With that, we already are adding the order. 

Now in shop.js, in post order where the order gets placed, I can therefore
remove all the code up here and simply say add order, simply execute this method
and then redirect once this is done and in add order, I will store my cart as a
new order and you could of course also add some new fields like the total of
value for example if you wanted to and that is it for now, so thereafter I
redirect. 

Now let's see if that works by going to the shop.js file and re-adding that
create order route and let's click order now here. 

Now I have page not found because orders, the orders page the route wasn't added
again but let's refresh the entire page here and my items in the cart certainly
are gone but I don't see new orders in the shop database, I don't see that
collection here but here it is after updating this once with the update arrow in
the top left corner and in orders, I have one order with indeed the items I had
in my cart previously and the cart is now empty. 

So let's now make sure in the next lecture that we can see our orders page
again. 

---