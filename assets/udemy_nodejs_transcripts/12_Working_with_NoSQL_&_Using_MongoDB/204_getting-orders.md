## 204. Getting Orders

<strong><em>no description</em></strong>

So now that we added some relational information to our orders, we can go back
to getting all the orders in our user.js file in the models folder. 

There I have get orders and now I want to reach out to my orders and simply find
them all or at least find all for that user. 

Now how do I find all orders for that user? 

Well remember, each order has a user object and in that user object, we have the
ID of that user, so we need to compare that ID to the current user ID. 

Now to do this, we add a filter and now in mongodb, you can also check nested
properties by defining the path to them, the only important thing to know here
is that you need to use quotation marks around the path and then you can say
check user and then the ID for the user. 

You do that by specifying user._id and this will look for _id in the user
property which holds an embedded document and then here I can compare it is to a
new objectid for this ID and this should give me all orders for that user and
this will now be more than one, so again we can use the toArray shortcut and
return that data to return an array of orders for that user and our user here
for example has two orders because we got two orders for that user ID. 

So now we want to output that order information, so let's go to the shop
controller, get orders, now I named my function get orders here too, so calling
that here should work. 

We don't need that anymore, that include thing was related to sequelize. 

I then get back my orders and I passed them to the orders view, so let's now
just inspect that orders view here and there I loop through all my orders and
for every order, I have an _id, that's important and then in the orders, I don't
have products, we could name it as such but I named it items here. 

So I'll loop through all the items now, there will be product information in
there though, for example the title and the quantity which is now a top level
field in product so we access it like this. 

And with that out of the way, let's save that and let's go to the routes folder
and there the shop.js file and comment in that one orders route you removed
earlier. 

And let's now click on orders up there, get db is not defined, that should be a
typo in get orders in the user model, yeah this should be get db with a lower
case b. 

So let's reload that page and this looks much better, now we got our orders with
the ID and with the items we ordered. 

So this is now working, now we got that basic shop functionality working again
which we had work earlier with sequelize, now we're doing it with mongodb. 

Now obviously just as we used sequelize for SQL to make certain things easier,
we can do the same with mongodb and there also, we can find an alternative that
makes our life a bit easier. 

---