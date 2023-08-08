## 224. Creating & Getting Orders

<strong><em>no description</em></strong>

Time to work on the last two pieces, the orders and again feel free to pause the
video and try implementing this on your own, it's always a great practice even
if you can't get the full result or full equivalence to my solution or if you
get stuck at one point, you can still then go back and watch the solution
together with me but you will still have a lot of practice by trying parts of
that on your own. 

So here's your chance to pause the video and we'll do it together thereafter. 

So let's dive into that together and let's work on our orders now, creating
orders and getting the orders, that is what we want to do and let's first of all
look into our controller for that, the shop controller. 

There we have post order, now what are we doing there? 

Well here first of all we got an unused variable which we can get rid of, there
we call add order on the user and that's essentially it,  so let's look into the
user model and let's see what add order did. 

Add order simply took our cart, so the products in our carts to be precise and
created an order object which contains the product data but also some data about
the user and then we inserted this into an order collection. 

Now since we worked with a collection there, we'll need a new model that's for
sure and the then is a result we just cleared the cart. 

So we get multiple steps we need to do here, first I'll add an order.js file in
the models folder because I'll need an order model to store data in an orders
collection. 

First of all let's import mongoose here by requiring mongoose like that, let's
create the schema constant where we access mongoose schema like this and let's
then define our order schema and how that should look like and of course here
you can really also go with the schema that works for you or that you want to
use. 

Now I will try to recreate the schema we used before where an order had the
items and the user data and that was it and the items were our products which in
the past was all the product data and the quantity. 

So here in my schema, I will have my products let's say, I named it items in the
past, here I'll name it products. 

Products will be an array of documents and every document will let's say have
the product data which will be of type object because this will be a full other
document you could say that is required and besides the product data, I'll have
to quantity for that product, could also name this just product here by the way
if you wanted to. 

So here the quantity and that will be a type of number and this should also be
required. 

Ok so this is how my products will look like, now I also will have a user and
there I want to have a name let's say where the type is a string and this is
required and what else did we store about the user in the past, well just the ID
so also have my user ID here which is of type schema types objectid and which is
also required and this will also refer to the user model. 

Now type object by the way is a bit of a shortcut, of course we could define the
full nested product with all the properties there, feel free to do that, I'll
just say well this is any object. 

So this is my order schema, now I'll export a model based on that schema with
mongoose model, name that order and hence the collection will be named orders
and then I got my order schema there. 

Ok so now I got my order model and that is new, we didn't use that before in the
last module, we could have but now we well we implemented it differently there. 

Now since we use a model based package again for interacting with the data, we
have to be more strict about that and that is a good thing generally and
therefore we have an order model again. 

Now with the order model added the question is how do we interact between the
order model and the user now? 

We had add order in the past and add order essentially just grabbed user data,
products, created an order and stored it, now I still want to do that but I'll
do it in a controller now. 

In post order, I'll work a bit differently, I will first of all import my order
model at the top from models order like this, so this import was added and then
down there in post order, I will create a new order object by using that order
model constructor. 

Now that order object needs to be initialized and it needs to be initialized in
the way we defined it here, so it needs to get products and it needs to get some
user data. 

Now the user data is a bit simpler, we got our request user, so here we have the
name which is request user name because remember, request user is a full user
object fetched from the database so there will be a name property and we also
want to store the ID of that user in the order, we also have like the user ID,
so we should store that as well, so we'll add user ID here and that will simply
be, well we can just use the entire request user object and as I mentioned
mongoose will pick the ID from there. 

Ok so this is the easier part, now we also need to add the products for these
users cart. 

However it's not that difficult because we already implemented something
similar. 

For getting the cart, we use this approach for fetching all the products that
are in the users cart. 

So in the end we can just copy this here, all the way up to the part where I
extract the products and reuse that in post order at the beginning here, just
make sure to close that then function here and here we now got the products that
are in the users cart. 

Now important is just products is not entirely correct, you should remember that
here we have an array of elements were we have the quantity and then the real
product data was nested in a product ID field but we can work with that of
course. 

We can now create our order inside of this then block and here, we can now add
products which should be an array of products and that should be an array of
products which is a bit transformed, so not the structure of products we get
back here but after some transformations, to be precise products for us need to
have a product field with the product data and a quantity field, that is almost
what we have but we have the product data in a product ID field here, not in a
product field but that is easy to fix. 

I will simply not just extract items like this, I will also map the items so
that I store the changed items in my products array and a mapped item should
still have its quantity so I'll keep that, the i simply refers to the item since
this function goes through all items in that array, so we'll have the quantity. 

And then we'll have a product field and the product field should have all the
product data so that we'll store everything that I had in i product ID before
because that was the old structure we had in there, now we have this structure,
we have an array of products which just have a quantity and then the product
detail data which is exactly the structure we expect to get in the order model
and now we can simply store these products in the order. 

And with that we got everything we need almost, now we just need to call save on
that order, so order save now saves that order to the database. 

And then we can chain then on that once we return order save so that we can also
redirect and so on. 

Let's see if that works by going to our shop routes again and commenting the
create order route back in and now back in our project, let me first of all add
a second product so that we get something to play around with and see that this
does not get added, this is just a dummy product obviously. 

So now in our cart we got no products, let's add a nice book to our cart,  maybe
also from the details page and let's not add the other product and let's click
order now. 

Now we don't find the page we want to redirect to, that's fine and the cart also
was not cleared because we haven't added that logic yet but let's have a look
into compass and let's see, if we refresh the entire setup, we got the orders
collection and in there I got an order with some user data, that looks pretty
good, let's quickly confirm the user ID, it ends with 8A8, that looks good and
let's have a look at the products there too and there I got a quantity of two
and I got my product ID. 

Well the product ID, is that what I wanted though? 

I wanted all the product data right, let's fix that in the next lecture. 

---