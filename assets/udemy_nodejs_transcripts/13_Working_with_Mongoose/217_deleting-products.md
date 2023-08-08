## 217. Deleting Products

<strong><em>no description</em></strong>

Last but not least let's make sure we can also delete data so that you see that
last part of the crud operations with mongoose as well. 

For that, we got our post delete product action and I'm calling delete by ID
here on my product model. 

Now if I have a look at delete, you'll see this is not something offered by
mongoose, however we do have find by id and remove and that is exactly what we
want here right, so if we call that then we've got everything we need, this is a
built in method provided by mongoose that should remove a document And now we
can go to the admin routes again, comment in that last admin route again, save
that and with that being saved, if I now click delete, no products are found and
we can of course also confirm this in compass if I refresh, there are no
documents in the products collection. 

So this is how we can work with mongoose and do basic crud operations with it. 

Now let's again add a user and see how we can relate different entities with
mongoose, so how we can manage relations and let's then add that cart and orders
thing again. 

---