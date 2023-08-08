## 160. Deleting Products

<strong><em>no description</em></strong>

Updating was successful, now let's also make sure we can delete products. 

So in admin.js, I'm talking about the post delete product method here now. 

We get the product ID which is good, now delete by ID does not exist in a
sequelize world, instead on the product we can call destroy and destroy allows
us to destroy any product we find through our options here and these options
allow us to for example add a where condition to narrow down which product to
delete. 

We can also use a different approach, instead of calling destroy like this and
adding a condition which product to find which is of course fine, we can also
use find by ID again to find a product by that ID and then again have our well
known then and error, catch methods and in then, we know we got a product and on
that product, we can now also call destroy and now this will destroy the found
product. 

We can return this because this will also yield a promise and therefore add
another then block which will execute once the destruction succeeded and there
we can if we want console log destroyed product and we can now also redirect
thereafter. 

We should redirect here to make sure we only redirect once the deletion
succeeded. 

If we now go back to our application and I add a new dummy product without any
picture, just like this and we go to admin products, I got stuck on loading this
automatically, I'll look into this a second but if we go to admin products
manually, we see it here if I click delete, this works. 

Now one thing I noticed is that if I added a product here, we get stuck and we
don't redirect, so for adding a product host add product here, we don't do
anything in then block, there we should of course also redirect to
/admin/product, so basically to the same we redirect when deleting. 

So now if we go back and we add a new product again, this is working and now we
can also delete the products here. 

So this is now all working and now we can manage the products, we can view them
here, now one thing we haven't touched at all are relations though because we
don't just have products, we all have a cart and eventually, we'll also have
users. 

---