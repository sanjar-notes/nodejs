## 227. Getting & Displaying the Orders

<strong><em>no description</em></strong>

Let's move towards the end of the module by making sure that we can also get the
orders and display them on our orders page here. 

So for that, we want to work in the shop controller with get orders and there I
had a get orders function on my user model we could call. 

If we have a quick look at this function, get orders simply reached out to the
orders collection and found me all orders for this user. 

Well that shouldn't be too hard right because what we can do of course is in our
controller here, we know the user ID because we got it here in a request object,
so in the end what I can do is I can use my order model which we're importing at
the top of the file and I can find all orders where and let's have a look at the
order model real quick, where the user, user ID so this nested object here, this
nested key is equal to the user id of the logged in user. 

So here we have user.userID, that should be equal to request user _id, that is
the check I want to make and this will give me all orders that belong to that
user. 

Well and then we can just use these orders here in the then method, so
essentially I can also just reuse my old then method where I already expected
the orders and I can render the orders page. 

If we now save that, we just need to make sure the route exists, so let's
quickly comment that in here and now if I click on orders, I get an error
because the structure of our data changed a little bit, so we need to work on
the view to adjust it to our data in my orders page here. 

How did it change? 

We loop through the orders and each order has an ID, that will still work but
then we have no order items anymore, we've got order products now, we can
confirm this with our schema or in compass of course, we got order products and
each product has quantity and then the product data in a product field. 

So inside of here, we have the product and there we have a nested product field,
so we could also name this just P to avoid confusion, this will be p and there
we have the product field with the title but directly on the top level p object,
so directly in the object that is stored in that products array, we have the
quantity so we can still access this directly on p which is the part directly in
order products but then the product data itself is nested in one additional
embedded document product. 

But with these changes to our view, if I now reload that view page, this looks
good, now I see all my orders here as we did before. 

Now something is wrong about the first two orders and the thing that is wrong is
that simply these orders were created at a time where we only store the object
ID and no special object data, so let me quickly delete these two orders here so
that we don't have them in our view and in our app anymore, so now we only have
valid orders in here. 

So this does now all work, feel free to play around with that, try adding totals
for the orders or anything like that. 

For now this is the state I want to work with, I want to continue with and this
is what I wanted to show you with mongoose and mongodb and you therefore now saw
a lot of different alternatives for working with databases and how to work with
the data then. 

---