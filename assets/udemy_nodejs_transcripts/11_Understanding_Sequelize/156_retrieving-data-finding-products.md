## 156. Retrieving Data & Finding Products

<strong><em>no description</em></strong>

With the product created, time to also retrieve a product when we for example
visit our index route. 

So in shop controller here in get index, it would be nice if we could get our
products. 

This current approach with fetch all will not work because product is now a
sequelize model as we're importing it from our model file and the sequelize
model simply have no fetch all method but sequelize models have plenty of
methods for getting data and instead of fetch all, they for example have find
all to get all the records for this model. 

Now find all as you can imagine also gives us back a promise where we can use
the result. 

Now find all by the way also can be configured with some options. 

We can pass our options here and we could define a where condition to also
restrict the kind of data we retrieve and you can read more about the possible
options you have there and how to write this in the official docs but we'll also
see a way of limiting the data we retrieve when we later fetch a single product.


For now let's get all without any restrictions and then here in the then block,
we should have our products. 

So here, let's assume we get a products list array to our function that get
executed here, that gets executed here. 

Here I will log any potential errors we might have and now in the then block, I
essentially want to render my page of course once we got the products and simply
pass the products into the prods key of my render function here. 

Let's remove the fetch all call down there and with that, time to save this,
let's go back to just localhost and indeed this is looking good. 

You see it retrieves the data, the data still has the same field names as before
and therefore rendering this automatically works. 

Now we need the same logic on the products page and therefore I will just copy
that and go to get products added here and of course replace the render function
here, make sure to pass products to prods though. 

And of course as I mentioned earlier in this course, you could refactor that for
the index and the products page to reuse this code instead of copying it, I just
like the more explicit approach here which makes it really clear what's
happening. 

So now we got get products working too hopefully, yeah this is looking good,
both work and we see even a difference because here I have a blank between the
dollar sign and the text and here I don't have it. 

So this is working and this is a huge step forward, now as a next step let me
show you how to retrieve a single product if we click on details here. 

---