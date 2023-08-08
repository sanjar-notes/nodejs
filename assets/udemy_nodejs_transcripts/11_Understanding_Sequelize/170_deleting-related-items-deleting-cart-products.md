## 170. Deleting Related Items & Deleting Cart Products

<strong><em>no description</em></strong>

Our program is taking shape, we can't delete products from the cart yet though
so we should definitely also do that. 

To do that, we still need the product ID we want to delete but now again, I will
first of all get my cart for the user by accessing request user get cart and
then adding then and catch calls as we did it multiple times already and in the
then block here, I know that I've got access to my cart and in that cart, I now
want to find the products for this user and to be precise, the products, not all
products but the product with that product ID. 

So here I will return cart get products and then simply here where ID is equal
to prod ID. 

In the next then block we add, I therefore have my products and I have to
extract that exact product I'm looking for as the first element in the products
array and now I want to destroy that product but not in the products table of
course but only in that in-between cart item table that connects my cart with
that product. 

To do that, I can simply call product cart item using that magic field sequelize
gives me to access the element in the in-between table and then destroy and that
will remove it from that in-between table. 

Now I will return this so that I can add another then block here with the result
of this operation if I would care and then there I'll simply redirect back to
the cart, where I should then not see that product anymore. 

Let's give it a try. 

If we reload the cart and I delete that one with quantity three, it's gone. 

Got no errors here and if we reload the cart items, we only have one element in
there with quantity two and the other one is gone indeed. 

So this is how simple we can delete connected items in this in-between table. 

Here are the example of the cart. 

---