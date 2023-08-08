## 197. Adding the "Add to Cart" Functionality

<strong><em>no description</em></strong>

So we're making progress on the add to cart functionality, at least a very basic
first version of it, let's now go to app.js to wire it up. 

When finding a user, I'm storing it in the request like this and this actually
should be all right, however it's important to understand that the user as I'm
storing it here will just be an object with the properties, so the data we have
in the database. 

All the methods of our user model will not be in there because the user I'm
getting here is data I'm getting out of the database and the methods aren't
stored there, they couldn't be stored there. 

So to have a real user object with which we can interact, I should actually
create a new user here and then simply pass user.name which is my username, how
it's a stored, user email, user cart and user_id, so I should create such a user
object and store that in the request because now this enables me to really work
with well all the user data or with the whole user model and this now allows me
to also call all these methods like add to cart on it. 

So with this changed to app.js, we can go to the shop.js file in the controllers
folder and then there, I want to work on the post cart method for now which
allows me to add an element to the cart. 

I do get my product id here which is nice and then we have all the logic here
for fetching what's inside the cart and for updating this, I will actually
comment this out because for now we don't need that. 

So instead what I want to do is here I want to fetch the product I want to add
here, so I will use my product constructor, my product model and I will use find
by ID to find a product by the product ID I'm extracting here and I'll just add
the then block here and in here, I should have the product that I want to add to
the cart. 

Therefore in here, I will now use request user which now is our full user model
and call add to cart and pass that product I fetched as an argument because in
the user model, add to cart does expect a product and then I return the result
of update one which will be a promise, so back in the shop.js controller, if I
return that promise instead of then here, I can simply chain another then block
where I get the result of in this case my update operation, so I'll just console
log that result. 

Now with that, let me go to the shop.js routes and let me add that cart post
route again. 

Let's now go back to products and let's give this add to cart button a try and I
get an error here. 

The problem here should be that if we have a look at our view, at our product
list.ejs file, that for add to cart, we have that add to cart ejs snippet that
include where I pass my product to but in add to cart ejs, I still access
product.id instead of _id, so I need to change this in order to pass on the ID
correctly. 

So now if I reload that products page and I click add to cart, now we get stuck
here but actually we were successful in a way. 

We did actually modify something as our result tells us here and if we quickly
go to compass and have a look at our users, you see there is an embedded
document, a cart document with items with an object which holds product data. 

Now that user ID here is a bit redundant because were already are in that user,
we could strip that out and only store what we want but it also that doesn't
matter too much. 

The important thing for us here simply is that we now store a whole product
which we do also store in a separate collection as part of an embedded document
in our user, so we clearly have duplicate data here, we have the same product
here as an embedded document and we have it in products. 

So this is maybe something which we should change because if we change the
product right now, if we change the title or the price, this will not be
reflected in the cart and in the cart we should have correct data because if the
price changes, we can show the wrong price in our cart, right. 

So actually we'll need to tweak this a little bit more. 

In our user model where I store product in add to cart, well I actually don't
want to store all product data in this object and then the quantity, I just want
to store the product ID by creating a new objectid here and passing product.ID, 
._id as an argument and the quantity, so now only the reference and the quantity
and not the rest of the data. 

If I now save this and I click add to cart again, it gets stuck again, it
doesn't matter too much right now. 

If I now update my users, I get an error here, that should be Product_id,
product_id, I forgot the t. 

So now again if I update this and I click add to cart again and I reload my
users document here or my collection, now you see I'm only storing the reference
and the quantity and this is exactly the information I want. 

If I now want to display information about the product, I have to fetch that
manually because I only have the ID, that on the other hand is all I need for
fetching information, so that is what it is. 

But on the other hand if I now do change my product, I don't have to change it
in the products collection and my users because that would be a lot of work for
data that might change quite a lot. 

---