## 190. Finishing the "Update Product" Code

<strong><em>no description</em></strong>

So we worked on the product model to make the save method more flexible and now
in the admin.js controller in post edit product, there we already have code
where we find a product by id and this will work because find by ID is a method
I created in my model, so here we have the product or maybe we should name it
product data because here, I will now create a new product constant by using my
product constructor, so my own product class and there, I will pass my updated
title, my updated price, my updated image url and my updated description and my
ID. 

Now actually, we don't even need find by ID then anymore, we can just get rid of
that and for now also of that and simply create a new product with all the
updated information and we now also need to pass the product ID, there you just
need to make sure that you create a new mongodb objectid object. 

So make sure that at the top of the file, you do actually require mongodb and
now you can of course also create a new constant, name it object ID or whatever
you want and extract that objectid constructor out of mongodb like this and then
you could just write new objectid and reference this basically, so we can now go
down to post edit product and pass a new objectid here with new objectid and
wrap that Prod ID you're extracting from the url here and wrap that or from the
body of the request and wrap that into object ID. 

Now we have that new product and now we can simply call product save because we
just modified the save method to support both creation and updating. 

So let me save all of that and let's give this a try. 

Let's reload that view here maybe, change the price to 19.99 and click update
product, now we get a page not found, let's ignore that for now and let's
instead go back to mongodb compass and click that refresh icon here. 

Now that doesn't look like it worked though right, the price is unchanged but I
also did not get an error, so what's wrong here? 

Well you need to go to your admin.js routes again and uncomment this post edit
product route otherwise editing products will not be possible. 

So now if we load that product to edit again and we change that price, now this
looks much better or at least partly. 

If we have a look at mongodb compass, we see now it looks like I made a mistake
with the assignment of values, so my description and I can simply edit this
here, my description now simply was the url and the other way round, so let me
change both and click update here. 

Now if we load this page again, it should work but the most important thing is
our method worked. 

Now what did I mess up? 

If I go to the admin controller, I'm assigning price, image url and description,
well that is in the wrong order, it should first be the description and then the
image url but that was only a little logical mistake I made. 

If I edit this again back to 12.99, you see now this is working and this also
works, let's see how it works if I edit two fields at the same time and this
also works. 

So this is how we can update a product with the help of mongodb and with the
help of update one. 

---