## 167. Creating & Fetching a Cart

<strong><em>no description</em></strong>

To work with our new cart let's go to the controllers folder here and there to
the shop.js file which is where we have our cart related actions. 

Get products get product, get index, that is all working, get cart however will
not work. 

In there, I want to use the cart associated with my existing user to get all the
products in it and render them to the screen. 

For this, let's get rid of that code but I'll comment it out so that I easily
can use my render function again and let's use request user, that's still the
user stored in our request. 

By the way one important adjustment, let's disable that force syncing again so
that we don't always override any data we stored. 

So let's go back to app.js, to shop.js excuse me and let's use the user we
retrieve for every new request and which we store in the request and there,
let's execute cart and let's look into this and see if this gives us anything
meaningful. 

If I now save this and I go to cart, it doesn't load the page and if I go back
we see undefined here, so we can't access the cart like this. 

But what we can do here is we can use our request user and get the cart which is
associated to it. 

Let's add then and catch, here we'll get the cart and let's log the cart here. 

If we save that and I reload this page, it still will not load but now I get
null here and not undefined. 

Now the reason why we don't find anything here for either of the two approaches
is that we got no carts yet, if we look into our database, carts is totally
empty. 

Just as we create a user right at startup, I'll create a cart for that user, so
here I create a user. 

Now in the next step where I get that user, I will also create a cart by adding
user create cart, like this  and I don't need to pass any data in there because
cart in the beginning will not hold any special data, it just needs to be there.


I'll then return this and only listen in the next step where I get my cart so to
say and with this now set up, you see an insert into carts call is done here. 

If we now have a look into our carts, we see now we get a cart associated to our
user with the ID 1 and now if I try to reload that carts page again, here we now
get some output and this output is stemming from our get cart call here, so from
this console log where I do log that cart, so now this is working. 

Now for completeness sake, let's also console log request user cart again, does
this also work? 

If I reload here, this still is the old log but if I scroll above it, we still
see undefined. 

So this does not work, we can't access cart as a property here but we can call
get cart to work with the cart. 

So now we've got the cart available, we loaded the cart from the database, we
know more about that cart here. 

With the cart available, we can use it to fetch the products that are inside of
it by returning carts get products. 

Remember a cart is associated to products in our app.js file through belongs to
many and sequelize will do the magic of looking into cart item and so on, so
into this in-between table. 

So we can get products, this was added by sequelize as a magic method and
therefore here in this then block, we'll have products available and here I'll
again just log any error I get. 

But in the then block here, we should have the products that are in this cart
and that of course means that we can now render these products. 

So here I will render my products here, store them in products and pass them to
the view. 

Now this will not work as expected though, if I now reload this page, we see no
products in cart. 

Now we got no products in a cart but we'll see that later once we do have them,
it'll also not work but I'll come back to that, for now let's just have a look
at our query statement. 

We can see that this is the statement executed by sequelize and if you didn't
see it before, here we can definitely see the advantage we have by using a
package like this. 

We don't have to write that SQL statement on our own, we use sequelize and let
it do that behind the scenes. 

So before I come back to what we will have to do regarding getting the cart
products, let's make sure we can add products to the cart. 

So for now I'll get rid of all that logic here and I will focus on adding
products to the cart in the next step. 

---