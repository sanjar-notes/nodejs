## 128. Adding the Product-Delete Functionality

<strong><em>no description</em></strong>

Now the application is taking shape, now there are two things I want to add in
this module still before we're done. 

The first one is I want to make sure that we can also delete products and I want
to make sure that we also can see our cart items on the cart view and also
remove them from the cart. 

Let's work on deleting products here first and definitely feel free to try this
on your own, you'll have to add a new method somewhere and basically make sure
that you can not just save products in the product model but also delete them
but of course we'll then also do it together after a short pause that you can
use to pause the vIDeo and go ahead on your own. 

Were you successful? 

Well let's see how I would solve this. 

We want to be able to delete our products right and if we go to the products.ejs
file, this view in the admin folder, we already have that delete button which is
wrapped in a form on purpose to send a post request to delete product, so we
need to handle that route, that is a good starting point. 

So in the admin.js file in the routes folder, we need a new route for this, post
route for delete product. 

Now since it's a post request, we also don't need to enclose or encode any
information in our path in the url, we can put it as part of our request body
instead. 

So back in the view, here I will add a hidden input again as we did it before in
post requests where I set the value to product ID using ejs templating syntax
and the name to product ID so that we can extract that information by that name.


So that's the first step, now we do have that route, obviously we also need to
work on the controller now. 

So let's go to the controller, the admin controller and let's add a new action
for deleting a product, exports post delete product. 

There I get my normal arguments in this function and now the question is what do
I want to do in there? 

Well obviously I can extract the product ID from the request body by accessing
product ID, that is why we just added it to our ejs template and now we can also
go back to the routes file and simply connect this route to our admin controller
post delete product action but the real magic now happens in our model, in the
product model. 

We have the save method, now I want to delete a product. 

So let's add a delete method in there and what I plan on doing here is I
actually want to turn this into a static method and maybe name this delete by
ID, pass in an ID and then have all the logic for deleting a product in here. 

To do this  I first of all need to find out which product to remove or update my
array of products so that I can then write it back to my file. 

So just as in find by ID, I will call it get products from file to get all the
products and in here, I then have the products array, there I now need to find
the index on the product I want to delete. 

So I will use products and then the find method to go through all my products
and find the product with the ID I'm trying to delete, this is a mechanism we
did before, whoops, it should be find index though. 

Now this means I can update my products array such that this element is removed
and actually there is even a shortcut we can use. 

I can create a new constant, updated products, take my existing products and not
use find index but use the filter method instead. 

Filter also takes an anonymous function and will return me all elements as part
of a new array that do match the criteria my function returns. 

So if this returns true, the element is kept. 

Now I want to keep all elements where the ID of the element is not equal to the
ID I'm trying to delete because all elements where the ID is not equal should be
kept around, should be part of the new array which will be the array I save 
back to my file. 

This means that in this function, I actually want to return the opposite here. 

So only if the ID is not equal to the ID I'm looking for, I want to keep the
item so this will then return true if the IDs are not equal therefore the item
is kept and only for that single product I'm looking for this will be false, so
the item is not kept in the new array. 

And that simply means that I can now go ahead and save my updated products which
are all products except for the one I want to delete back into the file. 

So I will use the file system to write a file on this path and simply add my
updated products in json format and then again I can use my or add my callback
function to see if this throws any error. 

Now if it does not throw an error, so if everything went fine then I also want
to remove that product from the cart of course because I can't have it in a cart
if the product doesn't exist anymore, right. 

So as a next step, we'll also work on the cart and make sure we can delete items
from there, a functionality we need anyways. 

---