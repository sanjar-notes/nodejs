## 165. Fetching Related Products

<strong><em>no description</em></strong>

We learn about associations and that we get these cool magic methods here about
which you can learn more in the official docs of course, now which implications
does this have for our other admin.js actions? 

Well for get added product, there's no implication, we fetch a single product
here and we can do this as before, we don't really care about the user here, you
could argue that you only want to find products for the currently logged in user
though. 

Then what you actually want to do is you want to use request user get products
and there define where ID equals prods ID to also have that filter and then you
can chain your normal then call and so on. 

And with that if you click on edit, we see an empty form because it generally
did work and we see the SQL statement here where it simply looks for a product
with the user id one and that is not the condition we wrote, we're responsible
for this part where it then also narrows down the product ID but user ID one was
added by sequelize because we use get products on the user but keep in mind here
we get back an array even if it only holds one element, so we got products and
therefore we know that one product, the one we are interested in will always be
the first element, so we have to store that separately in a new constant and now
if we reload this, this works. 

So this is a more elegant way, though we could also still only use the ID if we
want to use the old approach. 

If we move on for post editing a product, there I'm fine with finding the
product like this because if we are at this point, I assume we already have a
product for this user only, so if I update it like this, it's fine. 

Now get product should change, instead of finding all products, I want to find
products for this user, so I'll call get products like that which will give me
all products for this user and then I can render them here. 

So if I now go to admin products, I see the products for this user here because
this select statement gets executed where we narrow down the user to the user
with the ID one and post delete product, here again we could only find a product
for this user with this ID, I'm fine with this setup though. 

So some tiny changes showing you more of that power sequelize gives you for
associated models. 

Let's next have a look at how we can reintroduce the cart to our application. 

---