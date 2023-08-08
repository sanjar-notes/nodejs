## 173. Resetting the Cart & Fetching and Outputting Orders

<strong><em>no description</em></strong>

Now that we can add orders, one thing is missing and that is that we clear the
cart, I want to do this right after we edit the orders. 

So down there I need to work with the cart and therefore first of all, I'll
store it in a new variable, fetch cart, initially it's empty and here once I got
the cart, I'll store the cart in the fetch cart variable so that I can also use
it down there. 

Now that cart should essentially drop all its cart items. 

Now I can use my fetch cart here to call another method, set products for this
cart and set the products to null. 

Now let's return this and then add a new then block with the result of this
operation where I simply want to redirect. 

Let's give it a try, let's save this and reload the cart page here, click order
now, we're on the orders page, go back to the cart and we got no products in the
cart because if we go into the workbench, we see that the cart items indeed are
empty because we dropped all the items in the cart by setting them to null, this
is how easy we can clean up the cart here. 

So with that, we got all that logic done, the last step I want to do here is
that I actually show my orders and we can get rid of the checkout page here for
now because we have no such step at the moment. 

So now let's make sure we also retrieve the orders correctly and can display
them on our orders page. 

For this here, I'll first of all get my user and now I'm interested in the
orders of this user which I can get with get orders, a magic method added by
sequelize, thanks to our associations. 

Here we again get a promise, let's log any potential errors we get and in the
then block, I know that I have my orders. 

This is where I want to render my orders page therefore and I will pass a new
variable into that page, the orders variable which simply stores all the
retrieved orders. 

So with that I got my orders for this user, now let's go to the respective view
in the views folder, here's the orders.ejs file which always shows nothing
there. 

Now obviously that's not what I always want to show, instead I only want to show
nothing there or no orders placed yet, whatever you like if we got no orders, so
I'll first of all add a normal ejs statement where I check if orders length is
smaller or equal than zero, then we probably have no orders, so in this case I
want to display nothing there. 

Now else and that is of course an important part, let's also close that
statement of course with the closing curly brace, else I want to output my
orders and for now I'll do this in a very ugly way with an unordered list of
list items which I repeat for every order, so again ejs time to loop through all
orders with forEach for example. 

Now forEach as you know takes an anonymous function which gives us access to
every order then we repeat this code here for every order and then here, we
close the curly brace and the bracket of our forEach method, we can add a
semi-colon if you want and now this is executed for every order we got. 

Now every order we got has a couple of products that belong to the order, so for
every order I have here, I will output a h1 tag with the ID, order.Id, output
like this and below that another nested unordered list with more list items
where I loop through the products belonging to the order, so here I'll have
order and then it's order item, that is our connected model so to say, forEach
because that will be a list of all the related items and here I get my item. 

Let's close this here and let's also close the forEach syntax then down there
and now this list item is repeated for every item in this order and there I
simply want to output the title, so output item title. 

Keep in mind this is a product so it will have a title and then maybe in normal
parentheses, I'll output item quantity and this will not work, I can already
tell you that. 

If I save that, I get another error actually and that is simply coming from the
fact that I deleted one route, the checkout route, we need to delete it here too
so I deleted the action, we need to delete the route too but still if I reload
the orders page now, this will just crash here because I have an ejs syntax
error though, let's quickly fix that. 

Ok here for item quantity, you need to close that but even after this change,
this will not work now because order is not defined because that should be
orders forEach but now because we can't loop through order item here, this does
not work. 

And to understand this, let's have a look at our shop.js controller file and
let's output orders here and let's see what exactly we get. 

For this let's now reload the page, it will still break of course but now we can
have a look at the output there, we want to scroll up. 

There is what we log with this line, console log orders and there we can see
that we do have an array of orders but an order does not have an order item key,
this is not provided by sequelize. 

If we also want to fetch the related products to an order, we have to pass an
object here where we set include to an array with the field products or the
element products as a string. 

Now why products? 

Because in app.js, we associate an order to many product, products of course and
if we have a look at our model, the product model has the name product. 

Sequelize pluralizes this and then we can use a concept called eager loading
where we basically instruct sequelize hey if you are fetching all the orders,
please also fetch all related products already and give me back one array of
orders that also includes the products per order. 

Now this only works of course because we do have a relation between orders and
products as set up in app.js here and now we can load both together. 

This will still not make our template work immediately but now we got orders
with more data in them. 

Each order will now have a products array and with that in mind, we can go back
to our view here, to the orders view and tweak that. 

We can loop through the orders and every order will have an ID, that's fine. 

Now our order will still not have a order item but it will have a products list
and now we can loop through all the products and each item which is now simply a
product and therefore we can name it as such to make this clear, each product of
course has a title which we can output and it does not have a quantity but the
product will now have an order item key which then stores the quantity for that
product in that order. 

And now if we reload this page, we do see our orders with the nested products in
there, not the most beautiful presentation you have for sure but this is how it
actually works. 

We also see there is one dummy order that was created accidentally in between
with no products and we can always verify this by looking into the database, we
get four order items related to orders with the ID 9 and 11 in the orders, we
got 9, 10 and 11 so indeed there is the order with the ID 10 which has no items.


We can simply clear it by right clicking on it here, delete row, apply apply and
close and now if we reload the orders page, it's gone and we only see these two
orders. 

So this is now working and now we get the full flow, we got a user who is
related to created products, we can edit the products, we can delete the
products, we can add products to the cart. 

We can then also create an order based on the data in our cart, we can view
product details and so on. 

So this is all working fine as it should and with that, we get the set up we
need for now. 

This gave you an introduction to sequelize and definitely dive into the official
docs to play around with that and learn more about it and how it works. 

---