## 198. Storing Multiple Products in the Cart

<strong><em>no description</em></strong>

So I'm now able to store some data in the cart, at least in a very basic way but
obviously we don't just want to overwrite the existing cart all the time, we
want to be able to store multiple products in there and increase the quantity in
case we already do have a product in there. 

So we need to finteune our code a little bit and we already started, so I'll
comment this back in where I do check whether a certain item already does exist.


Now I just need to tweak that code a little bit, here I need to look for Product
ID because that is where I store my product IDs in the items in the cart. 

So I'm looking for product ID because I'm storing the ID in productid down there
and now if that is something else than minus one, we know that this product
already exists in the cart. 

So I can add a new quantity field again and set this to one by default but if
cart product is greater than zero or greater equal than zero, so if it's
anything else but negative basically, then this means this product already
exists. 

So then new quantity is cart product, that is actually the index so let's maybe
name it cart product index, so this is then actually equal to this cart items
for that given index we just identified and there we'll have a quantity plus
one. 

So this is the new quantity if that item already exists, so if it already is
part of our cart, if not we'll go with the default of one and therefore here, I
will always update to new quantity. 

However I also don't want to update by always overwriting items with a new array
with exactly one object, instead I want to add a new object to that array if the
product does not exist in there or if it does exist in there, I want to update
that one product, so how do we do that? 

Well one of the simplest ways and you could use other approaches where you
leverage some functions mongodb has but one of the clearest approaches you can
use is that you get the updated cart items, that you create such a constant and
then, you access your cart items and you create a new array where you copy in
all the existing elements with the spread operator with the three dots. 

So this gives me a new array with all the items that are in the cart and they
are now stored here and I can now edit this array without touching the old array
due to the way javascript works with reference and primitive types. 

So now I can edit my updated cart items and now I just need to differentiate, do
we already have that item in the cart or not. 

So I'll actually move that up here before my if check and then here if I make it
into this if statement, I know that we have this product already. 

In that case, I can access updated cart items for the cart product index I
found, so now I have access to that item I'm interested in, I know that it
already existed so I can set its quantity equal to the new quantity like this. 

Now else if the item did not exist before, I'll take my updated cart items and
simply add a new one with push. 

I'll add a new cart item and I'll add a new cart item which looks exactly as
described down there, so I'll just grab that code and add it here. 

So now I either update the quantity of an existing cart item or I add a new one
and then down there for updated cart, I can always set my items equal to the
updated cart items because that will always be an array with all the old
elements because I copy it first and then with the update added, so either with
the quantity increased for the existing element or with a new element added to
the cart. 

So then I can safely have my updated cart down there and save that to the
database with all the updated items in there. 

So if I save that now, I'll first of all add a second product real quick so that
we, whoops, so that we have some alternatives here and then I'll go to products
and I'll add this first one with $12 to the cart. 

Now if we update this in compass and we look into the cart there, we see this
was added again even though it already existed. 

So our logic is not too convincing, if I press this one more time, we now see it
in there three times I'd imagine, yeah, three times the same object so clearly
our logic fails. 

Let's see what's wrong and I found the issue, it was this comparison up here. 

The problem we have here is the product I'm getting here, right, the product I'm
getting as an argument is a product I just retrieved from the database. 

Now the _id we have in there actually is treated as a string in javascript but
is not exactly of type string, since I'm using three equal signs in my check
here however, I am telling javascript that this should only return true if these
two do not only match by value but also by type and technically this is no
string even though we can use it as such. 

So one solution is to use two equal signs or to use toString on both here, so
here and here to make sure we only work with strings here in both cases. 

And with this adjustment made, I can edit my object here by double clicking into
some field and then we can mark the latter two objects here in the array for
deletion by clicking on the cross on the left, click update thereafter, now this
is updated, we only have one item in there with quantity one but now if I go
back and I click add to cart and I do update this in compass, I should still
only have one object but now with quantity two. 

If I do add my other element here though by clicking on add to cart here and I
do update, now I should have two elements in the cart, one with quantity two,
one with quantity one. 

If I click add to cart again and I update this again, it should still be two
objects, now both with quantity two and so on. 

So now this is working, now I am updating the cart, this is now an add to cart
functionality, a basic one implemented on our own. 

Now of course we want to be able to also display the cart items. 

---