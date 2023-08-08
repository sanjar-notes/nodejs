## 169. Adding Existing Products & Retrieving Cart Items

<strong><em>no description</em></strong>

So let's ensure we can see items on the cart page and the problem is that right
now, this does not work because here on cart.ejs . 

we're still accessing product data for every product we loaded but the products
we have here are now just the products from our database. 

So we don't need to access any nested product data instead here, we'll just have
p title, we'll have a look at the quantity in a second and pId down there, so it
directly access the fields of our products on well, the product we're looping
through. 

Now the quantity is not part of that but of the related cart item you could say
and conveniently, sequelize also gives us a cart item key for this which stores
information about this in-between table and the entry that is related to this
product there. 

So with this if we save this and we now reload this page, it still doesn't work
because that should be cart item with a capital I, this is how I named my model.


So now you can see this works and now we're displaying our cart item here and
that of course is not quantity but quantity, so the key name we defined in our
in-between table and now we see the quantity too. 

So now we can see the cart items again, now we can go back to making sure that
we also handle the case that we add an existing item to the cart. 

So let's make sure we also handle this case, that we add a product to the cart
which is already part of the cart and that should of course simply increment the
quantity then. 

Therefore here if we make it into this if block, I essentially want to get my
old quantity first of all which I can get from my product by accessing cart item
as we just did it in the view in the last lecture, this is this extra field that
gets added by sequelize to give us access to this in-between table and there to
the quantity and sequelize does not just give us access to the in-between table
but to this exact product in the in-between table, so therefore we get the
quantity for this product as it's stored in the cart. 

So now we have our old quantity and new quantity, the variable we initialize
with one here is now simply old quantity plus one. 

With that we just have to add it to the cart, so here I will return fetched cart
to get access to the cart and then add product as I do it down there too, add
product and then simply my product here and my through call where I set my
quantity to, whoops new quantity just as I do it down there. 

If we now wanted to avoid nested then blocks here, what we could do is we could
add a new then block here where we get some data to which I'll come back, where
we do handle this fetch cart thing which is the same for both cases essentially,
we add a product with new quantity, so we can certainly remove that but now the
difference is that data here actually should hold both the product that needs to
be added and our quantity right because the quantity is calculated differently,
it either stays at one or here we set it to old quantity plus one. 

To make sure that we correctly get that data, we can of course pull new quantity
out of this anonymous function, make it a top level variable in this overall
function here and therefore new quantity is available in all then blocks and we
either leave it at one here or if we got a product, we also need to return that
product here because that will then be our product we receive in the then block,
it's automatically wrapped by a promise as I mentioned earlier and now we have a
setup that should work again and that ultimately should ensure that we redirect.


So now let's see this, let's click add to cart again and the quantity indeed is
two now and if I add a second product here, this one with the price 66 and I add
this to my cart, this is now add 1. 

And that is now pretty neat, we can now start adding all these products. 

Now let's make sure we can also delete them from the cart. 

---