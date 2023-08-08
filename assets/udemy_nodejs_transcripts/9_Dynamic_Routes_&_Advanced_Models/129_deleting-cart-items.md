## 129. Deleting Cart Items

<strong><em>no description</em></strong>

So let's edit the cart model now, we got the static add product method, now I
need a new static method which is delete product. 

There I get an ID of the product I want to delete and I also want to get the
price of that product, you can also name this product price because I'll need to
update the total cart price of course. 

So with that, what do I need to do? 

Well first of all I need to get my cart, so I need to read my file here and copy
that line and of course you could also refactor this for now I'll simply
duplicate the code here to make it a bit easier to understand. 

So there I read my file, I try to read in the cart and if I got an error here, I
can already return because that simply means somehow I didn't find a cart, so
there certainly is nothing to delete right so I can just ignore this. 

Otherwise we will continue so if we get no error, we'll continue and now is the
part where I want to update the cart. 

For this, I'll have my updated cart here and take all the properties of the old
cart and put them into a new object with that spread operator, I now want to
update both the products and the total price. 

The cart total price should be reduced by the product price, however this would
be incorrect because if we have the product in the cart three times, it should
be reduced by the product price times three. 

So let's postpone this for later,  let's first of all find out how often we do
have the product in the cart. 

And for this I'll have my product index and I'll find the product in the updated
cart in the products array with the find index method and there, this goes
through all the products and I'll check for the product where the ID matches the
ID of the product I tried to remove from the cart. 

This is now my index of the product, however here I could even find the product
right away, just product like this because I will remove it differently from our
products array. 

For now I just need the product to find out what the quantity is because
remember, we're storing the quantity in that qty field, so const product qty
equals product qty, you don't need to serve that in a separate constant, just a
bit easier to read and now with that quantity, I can use that here to have the
cart total price be my cart total price minus the product price I'm getting as
an argument times product, whoops,  product quantity. 

So now I'll reduce the total price by the product price times how many times I
had the product in the cart. 

So that is one important piece of information and now I can also update my cart
products here, whoops, products and set it equal to, whoops not that cart by the
way, the updated cart down there, so updated cart total price, updated cart
total price and updated cart products is now updated cart products which for now
is the old products array but now I'll call filter again just as I did in the
product model, there this function runs over all elements in there and keeps
only ones where I return true, so I want to return true for all products except
for the one I'm removing, so here I will return true only if the product ID is
not equal to the ID I'm looking for. 

So all other products are kept. 

And with that, I can write the cart back into my file by copying this, write
file and store my updated cart there. 

So this should now in theory work, I can now also go to the product model and
there I now need to import my cart model, so const cart equals require cart like
this and now with that imported, in here I can simply call cart delete product
and pass the ID and I also need the price now. 

To get this, I will extract my product before removing it so I'll have my
product here by searching my products with the find method for the product where
the ID matches the ID I try to delete, so now I got that product information
here which allows me to pass in the product price to my delete product method. 

So now we are able hopefully to delete a product by its ID and also to then
delete it from the cart if it was in there and right now for example, if we have
a look at our cart, we do have that ID, the milk can, we do have that in there
so this should be gone if we delete it. 

So now in the admin controller in post delete product, we can use product and
then delete by id and pass in our prod ID here, like this and then we can also
redirect to /admin/products. 

Now by the way a little side note, it would be best if we have a callback in
delete by ID so that we only redirect once we're done and the same is also true
for updating by the way. 

There the callback in save would be best for redirecting, for now I'll not do
this, later we will add this little functionality. 

But let's now see if that works, if I delete the milk can here, I get an error,
cart is not defined in my cart.js model, deleting the product work though, if
you check products.json, you don't find it anymore so this worked but in the
cart model, yeah I'm trying to get all cart fields but of course I'm looking at
the file content so I should use this. 

This is a bit annoying because now I deleted the product whilst I still have it
in the cart but it's no problem, I will simply recreate it and then hack the ID
into the products.json file. 

So let's go to admin products, add a new product real quick, test, get that
image again, set the same price so that I correctly update my my cart price here
and remove the correct price and then some description test. 

So now this exists again. 

Now let's just make sure that I copy the ID that I have in a cart and replace
the one that was newly generated in products.json so that we really well delete
the correct one from the cart too. 

Save all of that and now let's give this a try, if I click delete, if I reload
this first of all so that we load the new ID here too and I click delete, cannot
read property, find of undefined is now the problem in the cart model. 

And that problem here is that of course is still a string json format so I need
to parse it before using my file content. 

So let's save this, same problem as before, I will quickly re-add this, add some
dummy text as an image, doesn't really matter, set the price, some dummy text
here, wI will not see the image here because it is not a real link but that does
not matter. 

Now before doing anything, let's go to products.json and again replace the newly
created ID with the ID in the cart, like this, reload this admin products page
and click delete and now this looks much better, now this seems to work and in
the cart indeed, products is empty and the total price was reduced to zero. 

So this is working and now let's finish this module up by also making sure that
we do display cart items on the cart view here. 

---