## 122. Passing Data with POST Requests

<strong><em>no description</em></strong>

You now learned how you can display product information by getting that
information out of the url, now we have a similar problem for adding a product
to the cart. 

We get that add to cart button but in the end when posting our data, we also
want to know which product to add to the cart. 

However here, I will send a post request right, add to cart sends a post request
and this has one important implication, we can pass data in the request body. 

This was not possible for a get request but for post request you typically use
the request body, this is also what we use when adding a product. 

For adding a product, we have a form and as I mentioned there when we added this
the first time in the course, this automatically gives us a request which puts
all the input data and so on into its body but this only works for posting data,
this is not available for getting data but for posting data, we therefore don't
need to add anything to the url because we can put the information in the post
body. 

So therefore what we should do on product detail in this form is we should
simply pass some important information as part of the post request. 

So I will add an input here and I will make it of type hidden so that it doesn't
really get displayed on the page but still is encoded in the request that is
getting sent and I will give this a name of product ID, the name is up to you
though and now we also need to store a value here and that value will be the
value that is added to the request for that product ID and here I'll use ejs
again to output product ID because I still want to pass that ID to my backend so
to say, to my node express app but I don't want to use the url because I do use
a post request so there's no need to use it. 

You could do it though, you can also add a dynamic segment for post requests,
that would work too but there is no need to do it here. 

So let's pass that data with that hidden input and let's now work on the backend
on our shop.js file. 

There we got get cart but get cart is not the route we're working on right now,
we'll use that to display the cart then but for now I need a post request. 

So let's add a new route which accepts a post request, still to get to /cart,
that doesn't change but now we need a new controller function and we'll add one
here, maybe near get cart, maybe in front of it or after it that's up to you,
exports post cart and there I also will get my request response and next
function as arguments. 

And in here we will now have to retrieve the product ID from the incoming
request and then also fetch that product in our database, so in our file and add
it to our cart. 

We got no cart yet though so this is also something we'll have to work on. 

For now let's simply extract the data as a first step, the prod ID by accessing
request and now since it's part of the request body, we'll access request body
here and then product ID because product ID is the name I'm using in my view
here on the hidden input. 

So therefore here, I got this available, I can console log this for the moment
and thereafter I can simply redirect, maybe to just /cart here and this will
then load the get route, so it will render the cart page. 

So with that let's go back to the routes file and let's connect the newly
created controller action with the post route there, so post cart should be
connected here and now if you save that and you go back to the details page and
for now only there this button will work and you click add to cart, I'm on the
cart page and in the console we see that random ID which was generated, that
random number being logged. 

So this is working, now obviously we're not storing that in a cart right now and
before we work on that, let's actually go back to the product detail page and
grab that entire form here and make sure we also use that form in all the places
where we also have add to cart buttons. 

So let's add it on the product list.ejs file, now important there I also have
product ID available, so I also access a product field so this is working here
and let's add it to index.ejs and there I also have the product object available
which is now important all the time of course because I'm accessing product ID
here and since this is exactly equal in all three views, we can also add an
include add to cart ejs and put that entire code into that include here and then
simply well include that include. 

So instead of having that code here in index.ejs, we can use the ejs tag with
the minus to add include and then we go to well up one level and then into
includes and then add to cart and we use that same code also in the product
detail page here and also in the product list page. 

So there I also want to replace this form with my include. 

Now let's see if that still works, if I now go to products, now we get this
error because if you have an include in a for loop or in a loop in general as we
have it here, we're looping through all the products and then product is a local
variable available in that loop only, then in include, included in the loop
unfortunately doesn't get that variable by default but you can pass it to that
include here and you can do so by adding a second argument to the include
function where you again pass an object and simply add that variable again. 

So here this product is what will be available in include and on the right side,
you include or you add the value you have available in this file, so product in
the loop is now passed to product in the include. 

This of course needs to be done for all our include, so also in the index.ejs
file and not for the  one in the product detail though because there, it's not
inside a loop, so it's available globally and therefore works and now if we
reload here, this works, starting page works and the details page also still
works and we can go to the cart on all these pages. 

This is looking good, we're also outputting the ID here so this is working. 

Now as a next step, we'll have to work on that cart. 

---