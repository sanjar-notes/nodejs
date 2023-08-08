## 171. Adding an Order Model

<strong><em>no description</em></strong>

So our cart is looking pretty fine and actually we have the old functionality
again, now without storing anything in files but now working with a database as
we should. 

Now one thing is missing and that are the orders. 

Now I'll not add a real checkout flow here but I want to have a checkout button
in my cart which will basically for now immediately move all the elements in
this cart out of this cart, so clear the cart and instead create a new order, an
order that is related to a couple of products and a user. 

Now if you're feeling fancy, you can certainly try this on your own otherwise
we'll of course do it together here and we'll get there step by step adding a
simple checkout functionality. 

Let's start with the model and for this, I'll create a new order.js file and
copy my cart item.js file, move it in there, import sequelize, rename it here to
order, also here and now how should an order look like? 

Well an order is in the end just an in-between table between a user to which the
order belongs and then multiple products that are part of the order and these
products again do have a quantity attached to them. 

So just as we had cart items for the cart, I'll have order items for my order. 

So I can copy cart items again, move that into order item and rename cart item
here to order item, starting with a lowercase o here in the string name
definition and then it will have the same structure as an order, as in cart item
here in order item and the order itself will not have anything but the ID
because the order essentially is like the cart here for me. 

You could of course say an order has more information like an address and you
could add this here, you just have to make sure you add this for every order you
create but that is essentially it. 

Now regarding the relations, there is one important difference to the cart
though. 

If we go to the app.js file where we do set up all the relations, I'll import my
order here from the order, whoops, from the order file and I'll import my order
item from the order item file but now if we connect the models here at the
bottom, we can say that an order belongs to a user and it doesn't belong to many
users because a single order is always belonging to one user who placed the
order and the user may of course have many orders, like this. 

So this is not a many-to-many relationship, it's a one to many relationship, one
user can have many orders. 

Now an order however can belong to many products and it does so with an
in-between table which we specify with through which is our order item table,
like this and we can also define the inverse here if we want and that would be
basically that a product belongs to many orders but we can also leave it out
here. 

Now we get this set up. 

now let me make sure we can sync again so let's turn on forcing this. 

If we now refresh our database, we should have new orders and order items, in
orders we see a connection to a user and in order items, we see a connection to
an order and to our product ID then. 

So this is now the set up we need to use and I'll disable forcing this so that
we don't overwrite tables all the time now. 

So as a next step, let's make sure we have a checkout button and that this
button does actually then trigger something to create such a order. 

---