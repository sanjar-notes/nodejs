## 196. Working on Cart Items & Orders

<strong><em>no description</em></strong>

So we worked on products and users, it's now time to work on the cart and the
cart items again and that will now change now that we're using mongodb. 

So let me start with the cart model, now what is, what's the overall goal we
have here? 

Well obviously for every user we have, we want to store a cart right and that
user will have a cart and that cart will then hold the products. 

So actually with mongodb, this is a great place for embedded documents because
we have a strict one-to-one relation between a user and a cart and therefore
there is no need to manage this with a reference, I could actually get rid of my
cart items, my cart model so that I just have product and user and for now, also
the orders and now on the user model, there I also want to store my cart items. 

Now the question is how, the answer is we get our shop.js controller and in
there we got code to store something in a cart,  here for the user we got the
cart and then we got the products to see what's in there, update it and then
save it back. 

Now we can do that with the help of the user model. 

Let's say on a user object, instead of just having save I also add a new method,
add to cart, something like this. 

Now here add to cart would be a product I want to add to the cart of course,
essentially what we're doing here in shop.js already, here we already fetch or
we got everything we need to fetch a product which we could then add to the
cart. 

So I expect to get a product here which I can add and then in add to cart, I can
have all the logic I need to find out if that product is already inside of the
cart and therefore if I just want to increase the quantity or if it is not and
therefore I want to add it for the first time. 

Now to understand how this works you must not forget that add to cart will be
called on a user object and we'll create that object with data we fetched from
the database with the help of find by ID, here we will return a user. 

So therefore we just need to be able to accept more data in a constructor, for
example the cart so we can also store the cart in our javascript object here
which will be based on the data stored in the database. 

So now we can assume that we'll have a cart property on our user and now we just
need to find out if that cart contains a certain product already. 

Now the cart will essentially be an object let's say that looks something like
this, an object with some items, so an object which has the items array in
there. 

So what we could do if we assume that this is the case, we could create a new
constant, cart product and then use this cart items and find, let's say the
index of a product in that cart with the same ID as the product we're trying to
add again. 

So I'll pass a function to find index which simply is a function javascript will
execute for every element in the items array and then here I want to return true
if I found the right product in my items array and this will be the case if cp
which is the product in the items array, if the _id there matches the _id of the
product I'm trying to insert. 

If that is the case, so if this returns a valid index, so something else than
minus one which would be the default otherwise, then I know this product already
exists in a cart and then I just need to find out what its quantity is. 

Now we'll do this a second step, first of all we can assume that there will be
no products in the cart because we're just starting from scratch, so let's add
the code to add a product without checking whether that product exists yet, so
we can comment this out for now and instead create a constant, maybe named
updated cart which is an object where we might have an items property which is
an array where I will now include my product. 

However not just the product as I'm getting here, I also want to add a quantity
field, so I'll actually say product quantity and this is how you can add a field
on the fly in javascript equals one. 

Now another approach, maybe a bit more elegant than that is that in items, you
create an object with curly braces because we'll add an object here and then you
use the javascript spread operator, three dots to pull out all properties of
this object so of the product object and then with a comma, you can add or
overwrite a property, so here I'll add the quantity property and set it to one. 

Whatever approach you choose, this will create an object which holds an items
property which is an array of in our case only one object, one product with an
additional quantity information. 

And now I want to update the user to store that cart in there, so I will get
access to my database with get db and I'll reach out to my users collection and
I'll update one user in there and I'll update the user with this user ID here,
so what I need to do is I need to accept that ID as an argument. 

So this _id will be equal to ID let's say and then here I can say I want to find
the user where _id is equal to new and I'll use object ID which I extracted up
here because I need that for the comparison where this is equal to this _id and
once I found that, I'll describe how to update and I'll use $set where I pass an
object which holds all the information about which field to update in which way.


And here I essentially want to keep everything as it is, I dont want to change
the user name or anything like that, I'll just set cart equal to updated cart,
that is it. 

So cart which I expect to have in a user in the database will now receive
updated cart, so this object as a new value which will overwrite the old one and
this is important, it will not merge this with the old one, it will not merge
the elements in the items array, it will simply overwrite the old cart with the
new cart. 

Now I can return this here, this update one call and what this should do is
well, it should update our user to add a product to the cart, for now it will
always overwrite any existing products in the cart, we'll fix this later but for
now, this should work. 

Now let's wire it up in the next lecture. 

---