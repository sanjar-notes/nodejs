## 168. Adding New Products to the Cart

<strong><em>no description</em></strong>

To ensure that we can add products to the cart, we need to work on the post cart
method here. 

The post cart method is responsible for adding new products to the cart. 

For this, let's get rid of the existing code there because we'll rewrite it from
scratch, well almost, I'll keep the code where we get the product ID because I
still need to do that. 

Next I'll first of all get access to the cart in exactly the same way I did it
up there in get cart with request user get cart and then my then block, so I'll
repeat that and then have then and thereafter also catch here. 

And catch as always I'll just log any potential error I get and in then here I
simply have access to the cart. 

So now we have the cart available. 

Now the third step is that I want to find out if the product I'm trying to add
is already part of the cart because if it is, then I just need to increase the
quantity, if it's not I need to add it with a quantity of one. 

So I will return cart get products here with a where condition where I restrict
the retrieved products to the product with my prod Id, like that. 

So now I only retrieve that single product and in the next then block, I will
get an array of products as you learned but we know that this will only hold one
product at most, it might even hold no product if a product with this ID is not
part of this cart yet. 

So here I'll retrieve my single product as the first element of this array but
first of all I need to check if products length is greater than zero. 

I'll right this a bit differently,  create a product variable here and assign a
value to that variable if we do have products, otherwise it will stay undefined.


So now we do have this check in place, then I'll create a new variable, new
quantity and this will be one by default and then I'll check if product is
anything but undefined, so if we actually do have a valid product. 

If that is the case, I need to increase the quantity, so if we do have a product
here, I now need to basically get my old quantity for this product and then
change it. 

We'll do this later because right now we don't have any products in there so
let's now only work on the new product case. 

So if we got no product here, we know this product is not part of the cart yet,
so what I'll do at this point here is I will return a call to product find by ID
because I need to find the general product data for this product now, for my
prod ID it's not part of the cart but it's of course still in the database in
the products table and here, I will have a nested then call because it makes
things a bit easier here because I will execute two very different kinds of code
for the case that we have an existing product in the cart or that we have to add
a new one and therefore find it first of all. 

So here I know this is my product as it's stored in the products table and this
is the product I want to add to my cart and this can now be done by returning
and now I need to access my cart again. 

Now my cart is available here in this anonymous function but not in this one. 

To make it available down there too, I'll create a new cart to variable or fetch
the cart maybe to not always rename, use the same name and then here I'll store
the cart in fetched cart, so now it's not only available here but in this
overall function here and therefore down there, I now have access to my fetched
cart and on that fetched cart, I can call add product. 

It's another magic method added by sequelize for many to many relationships, I
can add a single product here and I will add it to this in-between table with
its ID. 

So here I add the product I retrieved, I just need to also make sure that I set
this extra field I added to my cart item, this is the in-between table but for
every entry, I also want to have quantity and if I have more than just two
matching IDs, I need to tell sequelize that there is an extra field that needs
to be set and I do this by passing an object to add product as the second
argument and there I'll add through, you might remember through from app.js,
there we use that to tell sequelize which model to use as the in between model
and therefore as the in-between table, now I'm telling sequelize, well for that
in-between table, here's some additional information you need to set the values
in there, so that's another object and there I'm basically setting the keys or
the fields that should be set in the in-between table, in this case it's the
quantity field which should be set to new quantity. 

So this is the case that I add a new product for the first time, new quantity
will be one here and I'm storing the product with that quantity. 

Let's see if that works, if I save this and I go to products, got no products so
let's quickly add one, just with some dummy data to speed this up. 

If I go to products and I click add to cart, we're not redirecting which is why
we're stuck on this page but we got no error here by the looks of it and if we
refresh or load cart items, we see a new product was added or a new element was
added to the cart with quantity one pointing at that cart with ID 1 and the
product with ID 1, so this seems to work. 

Now let's just make sure we also well do see our carts page, so here I'll add a
then block where I simply call res redirect/cart. 

So let's try this again now and now I get an error on that cart page and that is
what I mentioned before, this will now break. 

So before we handle the case that we add a product to the cart which is already
in the cart and therefore increase its quantity, let's make sure we can see the
cart items on this page again. 

---