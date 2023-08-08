## 132. Fixing a Delete Product Bug

<strong><em>no description</em></strong>

Now I'm generally pretty happy with the state of this application but there is a
minor issue in it. 

If we have no products in a cart or at least not the product which we're trying
to delete, let's say the one on the right here, we actually get an error and we
do get an error because we try to access the quantity of a product which we just
don't have. 

And the reason for that is that we simply use in our products.js file in the
models folder, we use the cart model to delete the product from there, right. 

The problem just is obviously not every product is in the cart, so in the cart
here where we have delete product, we first of all need to check if a given
product is part of the cart. 

So here when I parse the overall cart, here when I find the product in the cart,
I should check if we really have that product because if we don't have it, so if
I add an exclamation mark in front of this, so if this check here is true, that
means we don't have a product then I simply need to return here, I don't want to
continue, I don't want to try to edit it because it's not part of the cart. 

So therefore now if I reload my app and I quickly add a new product here,
whoops, with a price and a description like this and I then click on admin
products and delete this, now this works. 

---