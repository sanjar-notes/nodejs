## 188. Making the "Edit" & "Delete" Buttons Work Again

<strong><em>no description</em></strong>

Let's complete the crud operations by ensuring that we cannot just find all
products and add them and find a single one but that we can also edit and delete
our products and that is of course something which would happen in the admin
area and therefore, we need to work on the admin side again. 

For that first of all make sure that our admin page here where we list all
products works again, feel free to pause the video here to try this on your own
before we will implement it together. 

Were you successful? 

Well let's do it together. 

First of all in the admin routes, I want to comment in my get route here again
so that we are again able to get all products onto our admin overview page. 

Now here we use admin control in get products to fetch and render all products,
so if we go to the admin controller here, I of course need to re-add that get
products function by simply commenting it in again. 

In there I use request user get products and this will not work anymore, so
instead let me here simply use my product model and then use fetch all and this
also returns a promise so we can still use then on it and we should still get
all products but now through our own modified model. 

So if I now reload this admin products page here, I see all the products and now
we can try editing and deleting them. 

Now for that, first of all we need to go back to our views and adjust them to
take account of the new ID format, so here in products.ejs in the admin folder
in the views folder, in there whenever we reference the product ID like we do
here, it's products._id, the same here, product. 

_id, that is really important. 

Now with that in place, if we reload that page, our edit and our delete button
should work again and should make sure that we edit or delete the right product.


So let's work on editing the product in the next lecture. 

---