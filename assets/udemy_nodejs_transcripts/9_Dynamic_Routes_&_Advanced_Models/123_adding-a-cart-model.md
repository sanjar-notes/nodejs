## 123. Adding a Cart Model

<strong><em>no description</em></strong>

We're now working on the cart and right now, we don't have a cart, we got a
product but not a cart, let's now add a new model here, the cart.js file because
the cart is like a separate entity in our project you could say. 

Therefore I'll again export a class here and I'll name that class cart, so that
is pretty similar to what I do in product, there I export the class product but
now it's class cart and now we have to think about how we want to manage that
cart. 

Now obviously we want to have a cart that holds all the products that we added
and we also want to group products by id and increase their quantity in case we
add a product more than once. 

So to do all of that, I will first of all create a constructor here which allows
us to create a new cart. 

Now when this cart is created, I'll add a products property here which should be
an array and there I imagine having some objects in there which do maybe hold
information like the ID and important, also the quantity of this product. 

We can also add an information like total price which initially is zero let's
say and this of course increase with every product we add. 

Now what we need on this cart though is a way to add and remove our products
obviously. 

Now the problem we have is the cart itself is not really an object we'll
constantly recreate, not for every new product that we add we want to have a new
cart, instead there always will be a cart in our application and we just want to
manage the products in there. 

So the approach I want to take will actually be a different one, I don't really
add a constructor instead I'll add a static method, add product like this. 

Now this will take the ID of the product I want to add and the goal here will be
to then fetch the old or previous cart from our file for now, analyze that and
see if we already have that product, find existing product and then add new
product or increase the quantity. 

That is what I plan to do, so let's start with adding the logic for fetching a
cart from a file. 

For this I'll import the file system here and also the path helper here, whoops,
path to construct a good path. 

Now in product.js, we see how that path should be constructed so we can copy
that basically, go to products, to cart.js and then add it here. 

Now the difference is that the file will now be named cart.json and in there
we'll store an object that represents our cart and then here, in this part here
for adding a product, I want to use the file system to read a file and that will
be the file at this path so my cart.json file and we have a callback where I
either get an error or or the file content. 

Now if we have an error, we know that the file doesn't exist yet and therefore
we got no cart yet. 

So if we got an error then our cart will have to be created otherwise we know
that we, well get an existing cart. 

So here I'll add a new cart first of all which will have products that are an
empty array and maybe that total quantity we were talking about, the total price
excuse me which is zero. 

And therefore if we don't have an error, again that inverse logic, if we don't
have an error then we know we got an existing cart, so in this case my cart
should be equal to the parsed file content. 

We'll store it as json so I'll parse that with that json helper. 

So now at this point after the if statement, we know that we will have a cart
and now we can analyze it and add a product, so let's analyze the cart and see
if the product we're trying to add already exists. 

So we'll search for the existing product by taking our cart products in there,
remember we'll have products in the cart which is an array and by then finding
an element in there. 

So again we'll loop through all the products and have a look at each of them,
each prod, so in each product we'll have a look and we'll see if the product ID
matches the ID of the product we try to add. 

Now if we got an existing product already, then we simply want to increase that
quantity. 

So let's say we assume that each product object that gets stored in there is not
just a product object having the data in our product model but also that it has
an extra quantity field. 

Now if we have an existing product, then I want to create a new product and for
this I'll create a new variable, updated product and here in this if statement,
so if we have an existing product, I'll use updated product  and now next
generation javascript with the object spread operator, I'll take all the
properties of the existing product and add them to a new javascript object and
then on that updated product, I'll set the quantity equal to the old quantity
plus one. 

So I'll simply increment the quantity by one and since I distributed all
properties of existing product into updated product, the quantity will be
available there already because it was available in existing product. 

Now if we have a new product, I'll set updated product equal to and I should put
that into an else block, so if we have a new one, I will set updated product
equal to a new javascript object where I add information for that product and
that will be my ID let's say. 

So ID will be equal to the ID I'm getting as an argument and I'll set the
quantity to one because we added just one. 

Now the remaining thing is that I want to update the price of the cart. 

Now we got the cart here with the total price and the total price will always
rise by the price of the product we added. 

Now I don't have that information in here though, so I expect to get it as an
argument, product price and therefore here after this if else block, I can say
cart total price equals cart total price plus product price right because we
want to, price because we want increase that. 

So now we got our product added, we found it and we also analyzed it and added a
new product, increase the quantity, now we just need to save the cart back to
our file. 

And of course the cart should now also contain the updated product, that's also
important. 

So we updated the price thus far, let's now also update the products, so the
products on our cart should equal the old products and here again I'll use a
next gen javascript feature by spreading the existing products of the cart, so
this will now be an array with all the old cart products and now the question is
what do I want to do? 

Well if we are creating a product for the first time, so if I'm in this else
block, then I simply will add the updated product as a new additional product. 

However if I got an existing product here, I don't want to add a new product
instead I want to replace the old one and to do that, I need to find out where
in my old products this existing product was located, so which position it had. 

To do this I'll get the index instead of the product, so here I'll have the
existing product index and then I'll add my existing product which is simply
cart products at this existing product index, so one extra step but this now
allows me to use that index to replace the item in our cart products here. 

So there, I will set cart products equal to cart product, so first of all
copying the old array just as we're doing it down there but then I'll not add
updated products, instead I will set cart products and overwrite existing
product index, so at this position I will replace the element with my updated
product. 

So now the updated product is either replaced or added to the cart products and
the price is updated, now we can save it back and for this, we can use the file
system write file and write it to that path and then of course also define what
we want to put there and I want to write my cart into the path, obviously in a
stringified version, so as json and then here I have a callback where I might
get an error which I want to output so that I see if I do have one and which one
it is if I got one and then I am done. 

So this is now an add product method that hopefully does the trick, let's simply
try it out. 

So for this, let's go to the shop controller and in post cart, I want to add my
product. 

This of course means here first of all I need to get the product because I need
its price too, so I will use product find by ID for my product ID and then I
have this callback where I get my product, so here that is the product that is
retrieved from the products database so to say, from the products file and once
I have this, I can use the product information to update my cart. 

So in here, I now want to use my cart model. 

First of all, let's import it, cart by requiring it from the models folder and
there from the cart folder and with it being imported, let's go down to post
cart and say cart add product and now cart the model basically serves as a
utility model you could say, we're not instantiating it instead were using this
static function and I'll use add product to pass in my prod ID and also my, here
product that is what I'm retrieving from the product file, my product price
because that is also information that I need in there. 

With that let's see if that works by going back to our app here and clicking add
to cart, now looks good because we're logging the error here and if we see null
that means there was no error and now we got cart.json and in there, I got
products which is an array of products with an ID and the quantity and the price
is stored as a string which is a bit suboptimal here I have to say, so we'll
have to work on that but besides that, this is looking good. 

Now if I add another product or the same product again, then we see indeed the
quantity was increased, the price is misbehaving because it's stored as a string
and therefore concatenated, so we'll have to do something about that. 

In cart.js the price we're extracting, it's stored as a string in our product
model, so what we have to do is here when we work on the price, I have to add a
plus in front of product price to convert that string to a number and now if we
quickly delete cart.json to start from scratch and I add my element to the cart
again and I do that again and we now look into cart.json, now this is looking
better. 

So this is now working, this is our cart model added but with that let's go back
to our routing topic which we had in this module and let's see what query
parameters are and how they can help us with editing a product. 

---