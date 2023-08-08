## 203. Adding Relational Order Data

<strong><em>no description</em></strong>

Now that we're able to store orders for the user, let's add a new method to the
user model to also get orders and this will be a method we need to make our
orders page work again. 

Now getting orders is pretty straightforward, we reach out to our orders
collection here and then we need to find all orders for the given user and oh,
how do we do that? 

Well there's one thing which we forgot right when adding orders, our orders
right now contain the content of the cart but no information about the user to
which they belong and that is something we need to change first of all. 

So let's pause getting orders for now and let's tweak our add order function
here. 

We insert one order and right now the orders only are a cart. 

Well this is not the entire truth, right, we also need information about the
user, so let's create a new constant order in here which is the object we
actually want to save and in there we certainly want to have the items, so we
want to have the cart items in there, that is for sure. 

But we also want to have some information about the user and for this I'll add
an embedded document where I add the id and here, I want to create a new
objectid based on this ID, so on the ID of the user we're working with but I
also want to store the name which we have as a property here and the email. 

So here I will duplicate data because this will then end up in the orders
collection and in the users collection but I don't care too much about this
because the data I have been here, the user data I have in here might change for
sure but it doesn't need to be updated on all the orders because if you had like
processed and open orders, for all processed orders, you wouldn't care too much
if the user email changed because you might not need to touch it there and of
course if you do care, you can always get rid of all the data. 

So now even if the user name would change, I could be fine with not changing it
here and only in the users collection. 

I also want to store more information about my products by the way because right
now, my items are really just the product IDs but the idea was that we have more
information about our products than just their IDs. 

To be precise when we have a look at our orders.ejs file, here I also output the
product title for example and you could argue you also want to show the price. 

So storing some extra information would be useful too, therefore we also need to
work on this cart items again and we need to fetch some data from our products
database, so we need to tweak that add order method a bit more. 

Now we learned how to fetch product information with get cart, there we actually
get a cart with enriched information about all products. 

So actually what we can do is in add order, I can first of all call this get
cart and then add then to work with the data get cart gives me, so with my
updated products. 

So inside then here, I get my cart products and these products will have all the
product information along with the quantity and I then create my order inside of
that then block, so once I know that I have that products data because outside
of that then block, the code would execute too early. 

And then my items here will be my products, so an array of products with the
product information and the quantity, so now the product information will also
be part of the order. 

And here I really don't care about that information changing because if it
should change, for orders we need a snapshot anyways, if the price of a product
changes, that doesn't affect the past order, so there we wouldn't want to update
the price even if it would change. 

So for orders, such a snapshot and therefore an embedded document is a great way
of relating the order and the product because the product data might be
duplicate but it doesn't need to change in the orders collection because there,
we want the snapshot. 

So now I have my products in there and some user data, not all but some and now
I'll take my insertion code here and move that into this then block after my
const order thing and move this then block up. 

So now the order is we get the cart which is essentially an array of products,
we create an order with that data, then we insert this order into our orders
collection, that's new, we need to insert that, we'd return the result of that
and then here, we know that we were successful with inserting this and we clean
up our existing cart. 

With that, let's test this. 

Let's go back to our application and add a couple of products to the cart, let's
say like this and now let's click order now and I get an error, yeah because I
need to return the result of this add order thing so that outside of add order,
to be precise in my controller, I can call then on that. 

So that needs to change, so let me go back to my cart here, it's actually
deleted because we did write it to the database, so if I do update orders, we
actually can see it there. 

This was our old order, we can delete that with the trash icon here, the second
document is the new order we just added and there you see items indeed does have
all the enriched product information, the snapshots of our products and the
quantity in there and we have some user data. 

So this works and now with that little change I just made, let's also see if
that works again. 

If I order now, yes now we get no error. 

So now we can work on that cart page and on getting our order information. 

---