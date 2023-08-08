## 172. Storing Cartitems as Orderitems

<strong><em>no description</em></strong>

Time to add the checkout button. 

For that I'll go into my cart view here and in the cart view, I'll add a button
below all my list items, so below the unordered list here but still in the first
if block, I'll add it inside a form and that button will get a class button
where it will have a caption of order now let's say, it will be of type submit
and the form will have an action that leads to let's say create order, the name
is up to you, whoops no comma here and a method of post. 

If I save this, we can go back to the cart page and reload it, now we got no
product in there because I recreated all table so let's quickly add a new
product and let's add it to the cart. 

Now it's not centered, let's do that by wrapping our form with a div which gets
the centered helper class I defined earlier, so it's already part of your css
files, save this and now we have the order now button here, let's also maybe add
a horizontal line to have some space. 

And with that set up here which is good for me now, I want to click that button
to move the cart items into order items so to say, so to create an order with
all the elements in there. 

And to see this, I'll add a second product here real quick so that we have one
more item, one and more items in the cart. 

So now order now should create a new order with these two items and clear the
cart. 

Let's go to shop.js and make sure we have an action for creating a new order, so
here I will go there and exports post order which has the normal middleware
function as we know it, I'll also create the new route for this to handle a post
request to this order route, so a post request to /create order. 

For that let's go to routes shop.js and let's register a new route here, router
post create order and there, I'll use my shop controller post order, this new
action I just added which doesn't do anything yet. 

So post order here should now take all the cart items and move them into an
order. 

For this, let's first of all get all the cart items by accessing the request
user and then calling get cart. 

This gives me access to the cart as we did it before, so here I'll console log
any errors I might have and then here, I simply have access to the cart. 

Now with access to the cart, we can get access to all the products in there with
cart get products and this will return all products by default, so now here I
can call then, products and I can simply console log my products here if I want.


If we now click this button, it won't do anything here but in the console, we
can see the products that were retrieved and we see that the products that were
retrieved are the products here which also have that cart item attribute which
in turn gives us information about the cart item in this in-between table. 

So this is looking good, we got access to the products, now the idea is that we
move the products into a newly created order. 

For this let's import the order model here first of all, so time to import order
here from the order file. 

By the way, we don't need the cart import here because we never directly use the
cart model, we always do so through the user model but we'll need the order
model here or do we? 

Well just as a cart is related to user, so is an order, so we don't even need
that import, we can clear both cart and order because we'll create a new order
as an order that is associated to a user. 

So in post order here, we can now call request user and just as we create a cart
for that user in app.js with create cart, we can now call create order for that
user. 

Now this gives us an order but we don't just need the order, we also need to
associate our products to that order, so here I'll return request user create
order. 

And with the order created, and here I'll again do this nested, you can always
restructure it to not use a nested promise here though if you want but here I
will get my created order and now I want to associate my products to that order
and that can be done easily by calling order add products and passing my
products here. 

Now important, we need to specify true and set the quantity here correctly too
but now which value would we assign there because we get different quantities
for all the products? 

The approach is a little different, we don't pass it like this, we just pass
products to add products but each product needs to have a special key, a special
field which is then understood by sequelize. 

Now to assign that special field I'm talking of, the products we pass in here
have to be modified and we can do this with the map method, a default javascript
method that runs on an array and returns a new array with slightly modified
elements. 

We add a function here that is executed for every element in the array and takes
the element as an input and returns the modified version. 

I'll return products here in the end but before I do so, I do edit it slightly,
a new property which sequelize will look for named order item. 

Now the name here is important to get this right. 

If in your order item model, you define this name, that is the name you have to
use, if you chose a different name, you have to use the different name. 

So here I have order item with a lower case o and a capital I and therefore
here, I have product order item written in the same way. 

This now stores a javascript object where I configure the value for this
in-between table, so here I simply define quantity which is the value I need to
store in between and I set this equal to product cart item, this is the related
table I have due to my cart, quantity. 

So I get the quantity from the cart and store that for the order item, this then
gets returned here,  so now in the end I have an array of products with all the
old product data but also this new information regarding the quantity for my
order and add products will pick this up and add the products to the order with
that quantity. 

This is what's happening here, now we can return order add products here and add
a new then block here where I get any result and in here, I will then redirect
to orders. 

With that set up, let's go back and reload our cart page, if we click order now,
I'm on the orders page where we never display anything but we should be able to
see some data if we load the orders table, there is one order and order items
also has the respective elements that belong to the order with the right
quantities. 

---