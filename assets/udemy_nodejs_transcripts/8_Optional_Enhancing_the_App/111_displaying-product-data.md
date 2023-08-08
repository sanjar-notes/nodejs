## 111. Displaying Product Data

<strong><em>no description</em></strong>

We're now storing a product with all the data we need, now we should also
display all that real data and don't show any dummy data anymore. 

So for that, let's go to our product-list.ejs file which is one of the views
where we do display all products and there, we already output the real product
title but that's it. 

The image source for example is something we should now also replace and we can
simply add our ejs expression in there and output image url and this will be a
string that should be a valid url, so this should be displayable. 

Now for the alternative text, we can also use the title again, so I simply
copied the ejs expression up there, for the price let's say it's always dollars,
so I'll keep that dollar sign here as hardcoded text and then output product
price and for the description here, I will of course also replace the dummy text
with my description as it is saved in the product. 

Now all old products will not fulfill this new structure, so in the data folder
in products.json, I will actually remove them all from that array here so that
it's an empty array again. 

With that back in product list, this is looking good, now in index.ejs, we have
the same logic so we can simply copy that and back in index.ejs simply replace
it. 

Now if I reload my app on shop and product, we got no products but if I add a
new one, this is a test product or simply a book. 

Let's search an image, I picked a url here and insert it here, then let's add a
price 19.99 and this is an awesome book, sounds like a good title. 

Now you can press add products and right now this does not support decimal
numbers, to fix this, we can change something in the add product view, there on
the number input we simply have to add a step attribute and set the step to
0.01, this means you can have well two decimal places essentially and increment
in this step size. 

I'll save this but not reload, for now I'll simply go with a number without
decimal places to not lose my other data and hit add product and indeed on the
starting page, it's now showing this product with all the data I entered. 

So now we improved that and we made a major step forward, therefore on both
these pages obviously we see it, let's now of course also work on making sure
that as an admin, we also see the products here and we then not just see them
but we can also edit or delete them. 

That will be the next step. 

---