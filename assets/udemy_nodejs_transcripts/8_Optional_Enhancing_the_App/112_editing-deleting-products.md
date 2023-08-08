## 112. Editing & Deleting Products

<strong><em>no description</em></strong>

So let's work on the admin side then. 

We get a products.ejs file and in the end I want to render my products there. 

So what we can do is we can copy the product-list.ejs file content and in
products.ejs in the admin area, we can copy that in, if I now reload this page,
we see the same as we see on shop and products but obviously I want to show
different buttons there let's say, so that we can edit or delete them there and
of course we could even change the whole way we display the products but for now
let's focus on the logic and less on how we display that. 

So here I have my add to cart button, now time to change this maybe to an edit
button and let's add a second button where I say delete. 

With that if we reload, these two buttons are now there and obviously, they
don't do anything if I click them, just as the add to cart button doesn't do
anything by the way. 

So as a next step, I want to make sure I can load this to edit it and now to do
that, I first of all need to make sure that clicking this button does send a
request and actually I want to send a simple get request and get onto another
page. 

We could change this to a link with a reference to another page like this, if we
do that, doesn't look too bad, styling changed a bit because well some things
would have to be adjusted and I will do that later. 

Now we got that link which should of course now lead us to /admin/edit-product,
like this. 

If I do that we get to the Page Not Found page because we haven't registered a
route yet and the reason for this is that we don't just need to go to
/edit-product but obviously we want to go to a very different route here, we
want to make sure that we go to a route where we know which product to edit. 

So actually we'll need to pass something dynamic as part of that url, it would
be great if we could pass something like edit product for the ID 1 and then we
can retrieve that ID in the route that we're loading so that we know which
product we need to fetch from the database or from our file for now. 

Now this is some logic we'll add in the next module though because some people
might have skipped this module, so let's ignore this for now and let's focus on
deleting but to be honest we'll face the same problem there because we want to
delete a specific product and not all products obviously. 

So therefore here, we can also add a link but technically a delete process
should not send a get request to some route, instead here I will simply wrap
this in a form which leads to admin delete product and sends a post requests
there to indicate that we really want to change something and not just load
something or display something and then I wrap my button in there and give it
the type submit so that it does submit this. 

So now we get that connected and therefore on admin products, you see that
changed due to the form I added, we'll work on the styling or I will work on the
styling between modules, both styles or both routes will not work because we
haven't implemented them but we'll do that later. 

The same problem can be found for our Add to Cart here by the way, there I also
want to do something which needs extra information, I need to have the ID of the
product I want to add and I want to add it to the route we're loading or to the
path we're loading. 

So here I also want to have a form which goes to something like add to cart, we
don't have that route yet and then adds a method, post and then here I will have
a button inside of that form and obviously I don't just want to go to Add to
Cart but I would want something like add to cart one so that I know which
product with which ID to add to a cart. 

But again this is something I will do in the next module just as for the admin
routes. 

So for now, we're pretty much done, we added more views, we restructured our
controller a little bit, we practiced what we did thus far but now of course the
exciting thing will be when we finally start working more with dynamic data in
our route paths and when we therefore can start adding items to the cart and
editing and deleting items. 

We'll do that over the next modules of course. 

---