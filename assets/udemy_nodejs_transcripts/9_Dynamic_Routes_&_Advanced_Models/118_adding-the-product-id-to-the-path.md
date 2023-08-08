## 118. Adding the Product ID to the Path

<strong><em>no description</em></strong>

Let's start in the use folder and let's start with our product list.ejs file. 

There we obviously also want to be able to view the details for a given product
when we click on it. 

Now this requires a couple of adjustments, first of all we got our entire
article here which holds our product information, so this product cart and we
now need a way to also load a detail page. 

For this I will go into my cart actions down there and add a new button there
which is actually an anchor tag, I'll just give it the class button to make it
look like one and there I'll add details or write details on it and this should
go to some details page, we'll continue working on this part in a second. 

Let's now reload that products page here and you should see that details button
there. 

Now details should of course not lead to just slash but to a page that does show
us some details for the given product and this is exactly one of the use cases
where we need to pass additional information as part of our path because let's
say we want to load /products and then /information for this specific product,
now for that, we need some unique identifier. 

So first of all, let's ensure that every product we create actually has a unique
ID and for that, I'll go into my model product.js and in there we don't assign
an ID yet, so when we create a new product here or when we save it to the
database so to say, so to a file, in one of these steps we should also add an ID
and I will do it in save. 

Right before we do save it to a file, I'll add a new property by writing this ID
and this adds a new property to the entire product object we're working on and
I'll set it equal to and now we need some unique ID. 

Well we can generate a real unique ID with some external packages or anything
like this, for now I will simply take math random which theoretically is not
guaranteed to be unique of course but here as a dummy value it'll do. 

So math random is now my unique ID, I'll convert it to a string to have a text
unique ID, you could use a number but I'll go with a string and therefore this
will now be saved for all new products too, so our products will now have an ID.


And now that we know that, back in product list.ejs, I want to pass that unique
ID to my path here. 

So I will now use ejs here to also output something as part of that link here,
as part of this path and that will be product.ID, we have that ID available now.


So this link will now lead to products and now let's say we had this random
value, this would be one possible path now. 

Now we just want to make sure that we of course then also are able to handle
that and extract that unique ID from the path in our routes file so that we or
in the controller, so that we can load the correct product and show the details
for it and that is the whole idea here. 

We send some information as part of the path so that we can extract all the data
we need for the product from the controller or inside of the controller because
we can't really send the entire product as part of the url but we can send this
key information. 

Now with that, let's go to the data folder and make sure to remove all products
you have in there and I'll just quickly save that link here so that I don't have
to search a new image but then make sure to remove that or even easier, add an
ID by adding ID between double quotation marks and give that some random number.


Theoretically you can use any string but I'll go for some random number. 

And now we have that ID added and therefore our code will now work, if we didn't
add this well we would not find an ID and therefore we could not create that
path that contains the ID. 

If you save that and reload, if you hover over details now or if we click on it,
you should see that in the url you now also have that ID in there and right now
we got a page not found because we're not handling this route yet but we have
products and then this ID and in a next step, we will now extract that ID and
then know which product to load. 

---