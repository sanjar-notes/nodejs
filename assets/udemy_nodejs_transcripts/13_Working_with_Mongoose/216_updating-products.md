## 216. Updating Products

<strong><em>no description</em></strong>

Ok getting a single product was real easy, now let's complete the crud
functionalities back on the admin side by making sure we can also edit and
delete products and for that, let's start with editing. 

First of all get edit product should load a product and because as I explained
in the last lecture, because we would have find by ID by default, I can leave
that code as it is, I can leave that code as it is and I will get my product and
I shouldn't be loading that into my edit product page. 

So for that, I'll just need to go to the admin routes file and there I should
comment my get products routes back in, I'll work on this in a second too and
also my edit product, get edit product route, I should comment that back in as
well. 

Now let me quickly work on that route where I load all products, that is also
something we need of course, we can find that here, get products. 

I mentioned fetch all does not exist but find does and find also already gives
us the documents and not just a cursor so we can leave that code as it is and
with that if we save that, we won't be able to submit a change but we should be
able to see all products and to then click edit here and it is populated with
our data, so that is looking great. 

Now the next step is that we are able to click that update product button and
that this works of course. 

Now for that, let's work on the post edit product route in the admin controller,
we extract all the data we require which is of course great and then here we
need to change that code a little bit. 

Instead of creating a new product and calling save, I will fetch a product and
I'll fetch a product by ID with the prod ID, add a then block and in that then
block, I know I have access to my product right, to the product which was
fetched from the database. 

The cool thing is I can now move product save into my function here and call
save on the product that was fetched from the database because thanks to
mongoose, this will now not be a javascript object with the data but we will
have a full mongoose object here with all the mongoose methods like save and if
we call save on an existing object, it will not be saved as a new one but the
changes will be saved, so it will automatically do an update behind the scenes. 

The only thing I need to do is I need to set my fields, so I need to set product
title to the updated title, I need to set product price to the updated price, I
need to set product description, whoops, description to the updated description
and I need to set product image url to the updated image url and thereafter, I
can call product save and I can then return this and chain then here. 

So now I have a setup where I first of all find the product and I get back a
full mongoose object hence I can manipulate it and call save again, I return the
result of that and then call then on that to redirect once the saving was done. 

Let's see if that works, if I save my code and I adjust the price and let's say
I add an exclamation mark after the title, if I now would click update product,
I actually would fail because I need to comment in my route again, I just
remembered, here I need to comment in that post edit product route, so make sure
you comment that in and save your server side code. 

You don't need to reload that page, you can now just click update product and
this is looking good. 

I can already see my changes here so this seems to have worked and I can also
reload compass and of course I see my changes there too. 

So this is how we can update with mongoose, again very similar to how we did it
with sequelize all through logic and through manipulating our data. 

---