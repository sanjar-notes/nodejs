## 205. Removing Deleted Items From the Cart

<strong><em>no description</em></strong>

Now one problem I just noticed when I clicked around and deleted some products
here is of course that when I delete a product that wasn't a cart of a user as I
have it here, I added one product behind the scenes to a user product with this
ID and if we have a look at products and I don't want to update anything, if we
have to look at products, this product ID is not the product ID I have in my
cart here. 

So I deleted a product which was part of the carts of different users, now what
would you do about that? 

For one it's important to notice that our app works correctly because when we
try to load the cart, when we don't find the product data for an item in the
cart, we just go ahead and well ignore that basically which is what we want here
but how would you solve this? 

Well what you would do or what you could do, one approach that would makes sense
is that you add some kind of worker process which is something a bit more
advanced and not directly related to building web applications with node,
basically a script that runs on the server and checks for such cases in your
database once every 24 hours or something like this, where you basically scan
your users, your carts and look for products which you don't find in the product
collection anymore and then you clean up these carts, that would be one thing
you could do in an application to clean this up. 

Depending on your requirements, you could even have a cleanup script for the
entire cart which resets the entire cart every 24 hours or every seven days. 

An alternative approach that you could of course look into would be that when
you load the cart page as we are doing it here, so when you're calling get cart
on the user and you know that there are cart items on the user object and still
the products you get back is empty, then you know there's a mismatch between
what you have in your cart and what's in the database and in such a case, you
could then issue some behind the scenes request, so basically with exactly the
tools you learned about to update the cart of that user to match the product you
got back from the database. 

So if you got an empty product array and you have items in the cart, you want to
reset your cart. 

If you've got less items in the data you get back from the database then that's
in your cart, you want to find out what the difference is and then update your
cart accordingly. 

So this would be strategies you could employ here. 

For now, I will move on and not focus on that as this of course also depends
highly on your application needs but especially the second strategy is certainly
something you can implement with the knowledge you learned in this module, so
this would be a great challenge you can take to add the functionality to clean
up your cart on the user collection whenever you find out that in get cart,
there is a mismatch between the products you get back and the products you think
you have in your cart. 

---