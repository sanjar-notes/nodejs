## 130. Displaying Cart Items on the Cart Page

<strong><em>no description</em></strong>

We're already able to work on the cart, now I want to display cart items on
cart.ejs. 

There I simply will add a main section before the end ejs include, that's
important and now first of all, what do we need to do here? 

We need to check if we do have products and if we do have them, then we want to
display them and I will simply display them in a really boring list for now, we
can add styling later, just want to see if that works. 

So let's go real quick to the shop controller where we load the cart and there
first of all we need to be prepared to fetch all products because we want to
return them to the cart. 

However of course not all products we have, just the products we have in the
cart. 

So for this we need to go to the cart model first of all and get delete product
and add product, now we need a way to get all the products in a cart. 

So I'll add a new static function, get products here and in this function I will
access my file and simply return the product IDs. 

I need to get a callback therefore which I can call once I got the products and
then I can use this function here to read the file and in here I know I get my
cart, this time doing it correctly with json parse file content, this is now the
cart and actually I'll name this get cart and not get products because I will
return the entire cart here in my callback, this is all I want to do. 

Now obviously this can fail if we have no carts yet so I will check if we have
an error and if that is the case, I will call callback null here and otherwise
in the else block here, I will return a cart with valid values. 

Now we can go to the shop.js controller in get cart and here I call cart get
cart. 

I will have to pass a function there, the callback function I just added in the
cart model where I will eventually receive the cart and I will render my view
inside of this function. 

However I don't just need the cart, I need a little bit more information about
the products too, so I will use my product model then to fetch all products here
and I will add my callback here and make sure that this is nested in the cart
function and we're having a lot of callbacks here but it's still readable, later
we'll also find another way of working with a lot of depending async actions. 

So now I got my cart and I got the products, now I just need to filter out the
products which are actually in the cart. 

So I will go through all my products, so for product of products looping through
all the products I have in there and I will check if this given product is also
stored in a cart and I can check this because in my cart, we got the product ID,
right if you have a look at cart.json here, we'll store the product IDs. 

So I'll check if carts products, if I do find this product here, so if the
product I'm looking at in the cart, if the ID of that product equals my product
ID here and of course this is some code that can be improved if you store large
quantities of data but we won't store large quantities of data in our file here
anyways, we'll use a database for that and therefore for now this is perfectly
fine. 

And if I do find an ID in the cart, then I know well the product is part of that
and therefore I will create a new constant here, cart products which is an array
and I will simply add that product to cart products then, so cart products push
and I will add the product I'm currently looking at in this iteration of this
loop. 

So this product I'm looking at, if it's part of the cart I'll add it to cart
products. 

This means that after the loop is done, I'll have an array of cart products that
contains all the products which are indeed part of the cart. 

Now important, just adding the product like this does not suffice instead I'll
add an object with a product data field which holds the product and also a
quantity field because the quantity is stored in a cart too but not in that
product I'm looping through because these are just the products I'm storing in
the product.json file, obviously there is no quantity in there. 

In the cart however, every product I store there does have a quantity attached
to it. 

So in shop.js here, I will also store the quantity of the product I'm looking
at. 

Now I'm exracting my cart product here, so actually I'll store this const, cart
product data, I'll store the cart product I'm finding in the cart products array
in cart product data and I'll check the existence of that then and if that
exists I know there is some data about this product in the cart, I then store
the original complete product data from the product model and from the cart
product data, I'll take the quantity. 

So now we got quantity and product data in there and we push that object to cart
products and cart products is now what I want to return, so here I'll return a
products field which holds cart products, this is sent to my view. 

Now if we have no products in the cart, then cart products will simply be an
empty array and I can check for that in my template. 

So now let's go to the cart.ejs file and first of all I'll add an if statement
and check if products and now remember, products is simply this key here I'm
sending into my view, so I'll check if products length is greater than zero and
then close that and I'll also already define an else block here because I want
to render something if we got no products in a cart too. 

So here in the else block and you need to close that curly brace thereafter, in
the else block I'll render h1 tag where I say no products in cart, like this but
here of course I want to render the products in the first block of the if
statement. 

So here I'll render unordered list for now where I simply loop through all the
products, again using ejs products for each product and that is an anonymous
function here like that, then close the forEach loop here by closing the curly
brace of that anonymous function and then the bracket of this forEach method
here. 

Now in here I want to output the product information and now it's important to
keep in mind that product here, maybe we should name it product data, that this
does actually hold or does actually refer to a product with a product data field
and a quantity field and the product data field is the product I'm interested in
but I also need the quantity. 

So maybe even I don't name that product data but just p and then in here, I can
output p.product data, referring to that nested product data which holds the
product information like the title, so .product data.title would allow me to
output the title. 

And then also maybe in brackets and this is no ejs syntax, this is normal
hardcoded text here but then in there I use ejs again to access p.quantity and
remember p simply is that object we passed t that cart products array on our
backend code. 

So now let's see if that works, if I save this and I reload this cart page, we
see no products in cart. 

If I go to products here and I click add to cart, we indeed see that on our
page. 

If I add this one more time, we see it twice. 

So this is now working, the last step is that I want to be able to delete it. 

---