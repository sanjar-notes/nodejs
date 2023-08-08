## 131. Deleting Cart Items

<strong><em>no description</em></strong>

Let's make sure we can also delete items in the cart and for this in cart.ejs, I
will change my list item a bit, in there I'll add a div first of all or maybe
let's add a paragraph to be semantically more correct which will output the text
for this cart items, so things like the name and the quantity and then I will
also add a little button there, wrapped in a form. 

The form should go to cart delete item maybe, the method will be a post method
and in the form I will of course have my button with a class of button with a
type of submit which says delete. 

If we now reload the cart here, we see delete this is the button, we can
certainly work on the styling but for now I just want to make sure that it
works. 

Now this is the delete button and if I click that, it well should delete this
item of course. 

So cart delete item is a route we now need to add and therefore let's go to
routes here in shop.js because of course this is a customer action, our
customers will manage their cart and there below the cart I'll add a router post
method, cart delete item. 

Now we need a fitting action in the controller, so in a shop controller here and
there I got get cart and post cart, now I will also have exports post cart
delete product maybe, you can of course use any name you want and in here we'll
have to remove that product from the carts but only from the cart, not the
product itself. 

Well to do that, let's first of all extract the product ID from the request body
product ID and therefore we need to make sure that we pass it there too, so in
our form let's again add this hidden input with a value of our p product data.ID
and then a name of product ID so that we can extract it by that name on our
backend. 

And with that added, with this hidden input added here, let's now go back into
the controller and with that ID let's access the cart and then there, we can
delete a product right. 

Now that delete product function takes the ID of the product and we do have that
but it also takes the price and therefore, we should get that product
information first. 

So let's also call product find by ID here and get that product for this ID and
add a callback with the retrieved product, simply so that we can get the price
before we well issue the delete request. 

So in there, in this callback I will call delete product and now I can pass in
product price too and of course we could have also used a hidden input to pass
the price to the backend but I think this is the cleaner approach, if we only
pass the ID through the request and then we do all the data retrieval on the
backend in our node express code. 

So now we get delete product and with that we can also send a redirect request
back to cart and in theory, this should be all we need. 

Now of course the missing thing is that we connect our cart delete item route to
the newly created shop controller action, the post cart delete product action. 

And with that added in the shop.js file in the routes folder, we can reload our
cart page here, click delete and we see our products and by the way you can
ignore these errors on the right, these are related to my local network here. 

So now I got no products in the carts and if we have a look at our cart.json
it's indeed empty, product.json still has the products though. 

And if I quickly add another product with no real image, like this so that I
have more than one and I add both to my cart and I delete just a book here, only
that is removed, also in carts.json. 

So this seems to work just fine, let's also delete this one now, seems to work
good and with that, we improved our app a lot and you hopefully get a bit of a
feeling for how you can pass data around and how you can work with your models. 

Now correctly you would say that of course our current approach here in the
modules is a bit suboptimal because working with the file and so on, it's not
that great, we can also improve some things in the controllers because for
example as I said, we should redirect if we know that the deletion succeeded and
not right after this line  because since we access a file in there,
theoretically we should use a callback here too. 

But these are all things I will do once we finally also added the database,
something we will do in the next module now. 

So time to move on to this exciting big block of the course. 

---