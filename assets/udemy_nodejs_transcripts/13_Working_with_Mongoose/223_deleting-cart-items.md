## 223. Deleting Cart Items

<strong><em>no description</em></strong>

Now that we're able to load the cart data, let's of course make sure we can also
delete cart items and for that, we have the post cart delete product action in
our shop controller. 

Now in there, I use the delete item from cart method on the user object which we
wrote on our own in the last module and which of course is also not a default
mongoose method. 

So it's time to go back into the user model and have a look at the delete item
from cart method and see how we can recreate that functionality. 

There what I do is essentially I create an updated cart items array by filtering
out the items that should survive, so all the items except for the one I want to
remove and then I update my model. 

Well we can of course do that by copying, well basically just that code here and
adding another method just as we did it with Add to Cart, so I will use my user
schema and there, the methods key again and then I'll add a remove from cart
method which will be a function and in that function, I will add that code which
I copied from the bottom. 

This code relies on being aware of the product ID of the product we want to
delete, so Product ID is an argument I expect in this function here, in this
method and now we get the updated cart items and now all we need to do is we
need to set this cart items equal to the updated cart items and then we return
this save and now we got a method that we should be able to call to remove an
item from the cart, just like that. 

So let's move over to the shop.js file in the controller's folder and there in
the post cart delete product route, well I just renamed it a bit, I named it
remove from cart, you could have kept the original name of course. 

Now I have remove from cart, I pass the product ID and I redirect here to the
cart page once we're done. 

That should work but it will only work if we enable the fitting route again, so
let's go to the routes folder, the shop.js file and let's comment in the cart
delete item route again. 

And with that all changed, if we now go back and we click delete here, that
looks good, we loaded the cart page and all the data is gone. 

Let's also verify this in compass by reloading our users collection, there in
the cart items is an empty array. 

So we're now able to add items to the cart and remove items from the cart, let's
next work on the orders. 

---