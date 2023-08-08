## 222. Loading the Cart

<strong><em>no description</em></strong>

So in the last lecture, you saw how you can extend mongoose with your own
functionality and that is really powerful. 

Now obviously, also check the official docs, there under schema you can learn
way more about that, this is the technique we just used, we added an instance
method, you can add more about that and all the nice features you can add to
your own schemas and models, so definitely check that out for all the details
that could be interesting to you. 

Now here I want to work on the route that allows us to load the cart and this is
a nice practice for you again, feel free to pause the video at this point and go
ahead and try to implement this on your own before we then do it together. 

Were you successful? 

Well let's go to the shop.js file in the controllers folder and we're looking
for the get cart method here. 

Now there we have request user get cart and get cart is a method we defined in
the past which does not exist by default, mongoose does not give us this method.


So we again have to revisit our user model and in there, let's have a look at
get cart, how we defined it in the past. 

In the past we simply reached out to our cart items, we got all the product IDs
and then we had a look at the products collection to find all the products in
there, convert this to array and return the products, so essentially get cart
gave us an array of all the products in the cart. 

Now with mongoose, this is a bit easier, we already have our nested cart items
array and if we have a look at compass, we see the items are objects where we
have the product ID and now we simply need to populate the product ID with all
the data we are interested in. 

So in shop.js in get cart, I will not call get cart on my user instead we can
call populate on the user to fetch data even though we already fetch the user,
we can also call populate on that and tell mongoose to fetch data for, now which
path is it? 

Well for cart.items.productid, let me console log my products here to see if
that works. 

Now we also need to add that route again, so in the shop.js file in the routes
folder, let's add that get cart route again and with that changed, let me load
the cart page and I get an error and the reason for that is populate does exist
but actually it does not return a promise, so calling then on it would not work,
we have to chain exec populate after that and then we'll get a promise, so then
we should be able to call then. 

So now with that, let's log products, save that and reload that page, now I get
no products in cart but if I go back, well we see actually what we have here is
the full user object which makes sense because we're not just fetching products,
we still work with the full user, so that is a tiny change so let's actually use
or log the user cart items here to see if that was still populated with all the
item data and I'll temporarily create an empty products array so the rest of the
code does not fail and now let's save that and reload the cart page one more
time. 

If I now go back, you see indeed here what I log, user cart items now is an
array of items where the product ID is populated with the product data. 

So now it works a bit different than before but it still gives us the data we
need, so here products now actually is user cart items and that is what I pass
to my view but I will need to look into my view now because the structure
changed a bit compared to before. 

The cart.ejs file is what we need to edit and in there, we loop through all
products which is fine but remember that our product data will then be nested in
a product ID field and you could also rename this to just product in your schema
therefore which makes a bit more sense I guess but I still have product ID here,
so the title is not available on the top level object which would be this object
but on the nested product ID object. 

So here we have to say p.productid.title. 

The quantity is on the top level object so this is fine, the product ID again
can be found on the product ID nested or embedded document though. 

So with that, let's save that and let's now reload the cart page and indeed we
see our cart item here now. 

So this is looking better, now we're able to populate our cart with data. 

---