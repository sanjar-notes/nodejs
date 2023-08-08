## 127. Editing the Product Data

<strong><em>no description</em></strong>

Time to work on our product model again. 

In there we get a save method and right now we used that to create a new
product. 

Now why don't we also use that for updating an existing product if we already
have it? 

To do this what we'll have to do is in save we just have to check if we already
have an ID and therefore when creating a new product, we should accept an ID too
and then set this ID equal to ID but we'll simply pass null here for a brand new
product, so that we can still create products that don't have an ID yet then the
ID will be assigned here but if I we're editing one, we do have the ID already
so we can simply assign it here. 

And then in save, we can simply check if this ID is already existing, if it is
null, this will fail and will automatically make it to the next line which we
want but if we do have an ID, save should not create a new ID and new product,
instead it should simply update the existing one. 

We'll still have to get all the products though, so indeed this should be moved
into our callback because we need all the products anyways and the new ID
creation can also move in there but after this if statement. 

Now in this if statement, I now want to update the existing product and for
that, I need to find it first. 

So I'll find my existing product index again by searching for or going through
all my products with the find index method, products will be an array as we know
and there, I will get access to all my products stored in the temporary prod
argument here or in the prod argument of this anonymous function I should say
and I can simply check if the ID of the product I'm looking at in this array is
equal to this ID, put in other words if I'm now looking at the product I plan on
editing. 

If that's the case then I found the index of the product I want to edit and now
I simply have to replace that in that products array. 

So I'll create an updated products array where I use that spread operator again
to pull out all the existing product elements, store them in a new array and
then on that array updated products, I'll replace my existing product index with
this because this inside of this class here is of course the updated product
because you have to imagine that I create a new product instance, I will
populate it with information about my existing product and then I just call save
and I will find out that I already have this product and therefore I just
replace it in the array which is stored in the file with the newly created
product I'm in. 

So with that being saved, I just have to write that information to the file, so
fs write file is what I need to execute, so this code will stay the same, just
that I need to call it on updated products here and I will now also wrap the
other part here in the else block so that not both snippets execute but only one
of them. 

So now we're storing the updated products and write file will always replace all
the old content, so we won't add it or anything like that, it will replace it
and therefore we should now have a save function that we can use both for adding
new products or editing existing products. 

Now this has one important implication, we now need to go to the controller and
when adding a new product here in post add product, we now also need to set null
as an ID, as a first argument here on our product constructor because we just
added this as an additional argument here in the constructor and if it is null,
then this check will fail and we will therefore make it into the new product
created mode which is what we want. 

We now can also work on the post add, edit product method, there I need to do
two things. 

First of all I need to fetch information for the product, then I need to create
a new product instance and populate it with that information and then I need to
call save. 

Let's first of all extract the product ID, prod ID by accessing the request and
there since it's a post request, I expect to get that information in the request
body. 

However at the moment this will not happen, so let's go to the view first to the
edit product.ejs file and there I need to add a new hidden input which stores
the existing product ID. 

However that is only an option if I'm editing a product, not if I'm adding one, 
so first of all I'll use ejs to again check if I am editing and also close that
here, here we also need to open a curly brace therefore and if I am editing and
only in this case, I'll render a new input here which is hidden, so which the
user can't see where the value is now my product ID, so I'm using ejs to output
the product ID there. 

And this will now therefore be included in the form, now I just need to give it
a name, product ID maybe and now I can extract it by that name in the incoming
request in my controller, so request body product ID because I used product ID
as a name here in the view on the hidden input. 

Now with that ID fetched, I could fetch my product through the product model but
actually this is the edit route right, so I get the new values I want to store
as part of my post request body because the user enters them here in the form. 

Here all this is sent to me, so I will now simply store all that in values or in
constants like my updated title will be request body title, I'll have my updated
price which is request body price, I'll have my updated image url and you can
name these constants however you want. 

Now important of course is what you access here on the request body, these keys
have to match the names you have on your inputs in your well added product view.


Last but not least, we got the updated description here which is request body
description. 

And now with all that data, I can create an updated product, this name is also
up to you, instantiate a new product therefore and here, I do pass my existing
prod ID as the first argument and this will ensure that in the product model, in
this check here we do find a valid ID and therefore we go into this updating
mode instead of the add mode. 

So I'll pass that ID and I'll pass my updated title then, I'll then also pass my
updated image url, I'll pass my updated description and my updated price. 

So this is what I pass and now thanks to our changes to the product model, I can
call updated product, save and it should hopefully just save that and override
the existing one. 

Now let's try this out and for that, let's go to our admin.js routes first of
all and register this newly added post added product action on the added product
post route and now let's reload our page here and add a couple of exclamation
marks and hit update product and the problem is I never send a response so this
failed but if we have a look at our products.json file, the first product didn't
change but the second one indeed has all the exclamation marks, so this does
work. 

So the missing thing just is that we send the response in our controller, so
here after calling save, I will actually call res redirect and go back to just
/admin or let's have a quick look at the admin.js routes, I want to go to
/products, so /admin/products I mean, this is what I want to redirect to. 

So let's save this, go back and reload, here we see the estimation marks too,
let's change the price to 30.95 and also change the description, it's really
great. 

Update the product, we are redirected and we can already see the changes here
and we can edit it again of course, for example remove the estimation marks. 

So this is working, we're now able to edit the product. 

---