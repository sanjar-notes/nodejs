## 109. Registering the Routes

<strong><em>no description</em></strong>

So let's start with registering the routes then and for this I will go into the
routes folder. 

There we have admin and shop and this still sounds like a decent differentiation
and let's start with the shop related routes. 

Right now we got the starting page, now we will also need a get route for
/products because if we have a look into our navigation.ejs file, this is this
new link which we added, so /products. 

We'll also need /cart because that's another new link we have and this will also
be a get route and I will of course also add controller functions but I'll first
define all the routes. 

So I'll also need /cart and later, I'll also need a route for the checkout
process, so /checkout is already something we can also add and obviously you are
free to edit any of these paths to your liking, just make sure to then adjust
the links you might have in your application. 

Now besides visiting /products, we will also need a single product and that will
then actually contain some new logic to which I will come back so let's stick to
these general routes for now. 

Of course we also need more than just the shop routes, we also got some admin
routes, in a navigation for example, we got the new admin products here and then
we'll also need a route for editing, we'll add this later and for deleting, also
something I'll add later. 

So for now let's simply go to admin.js and there I will add a new get route
because I want to load a new page and that will just be /products. 

Now never forget this is just as the other routes also already in a path that
starts with /admin because this is what we filter for in app.js and of course
we'll also need a controller function for that. 

Ok so this is looking good, now how about the controllers? 

Now we can follow different approaches there, obviously most of the things we
have are still related to products but we also got some new routes like cart or
checkout and later we'll also add orders for example. 

So we got that, now these are implicitly of course related to products right, we
do buy products in the end but we could also argue that semantically or from a
logic perspective, they rather belong to the general shop idea. 

So now we might be back to actually using a shop controller and a new admin
controller so that we can split our logic by these two sections, alternatively
you could of course also think about using a products controller and a shop
controller and have everything related to products only in the products
controller and things like cart and checkout in the shop controller but I will
go for this setup. 

Now that of course means that my two admin related routes, get add product and
post add product should be removed from the shop.js file and go into the
admin.js file, this makes more sense. 

I will also need my model here though, so let's take that import and also add it
here in the admin.js file. 

This has implications for my routes because in the admin routes, I'm still
importing the shop controller, well this should now become the admin controller
and therefore I should also rename it to admin controller up here and then
replace it down there and a similar thing needs to be done in the shop.js file
in the routes folder. 

There we import the shop controller which is good but I should also name it shop
controller then and then of course also replace that. 

So this looks a bit cleaner to me and with that, we can now also hook up our
other routes. 

For this of course we first of all need to add them though, so let's start with
shop.js and there I will export a new page and that should be my get index
function here, there I want to render the index page so I will get my middleware
function here and in there of course I also want to fetch some products and
render a view. 

For now I will therefore simply copy the logic from get products, so for now the
two pages are the same but I will render shop index here, so using that index
page view here and even if we have the same products on there, we can of course
work on the view and show a different starting text there for the starting page,
anything like that. 

OK now we got get index and get products and if we go to the routes file, this
means that for slash anything, I actually want to load the get index function
here in my controller because that is the starting page and it's for /products
that I want to load get products instead. 

We also need to load the cart and checkout pages and therefore let's go back to
the shop controller and there, we got get index and get products, I will export
something new and that will be get cart and there again, request, response, next
is what I have here and I will render a new view here and that view will be
shop/cart, pointing at the cart.ejs file in the shop folder and I will pass some
data to it, for example I need to set the path to /cart. 

By the way for product list here, I also need to set it to /products because
that is the path we're checking for in the navigation, we can also change the
title here maybe to all products and on the starting page, I leave it at shop. 

I pass the products to both views, I don't really need that code anymore, that
is a relict we have from the handlebars times, we don't need that so we can
remove that. 

Now for the cart view, I will therefore also add a page title and there, I will
simply say your cart and that is it for now, later we'll also add or load the
cart items but let's not focus on that for the moment. 

Last but not least, let's load the checkout page with get checkout and there we
have a request, the response and next and here I then also render a view, the
view here is shop checkout and then we need to pass some data where I set the
path to /checkout and where I also set the page title to checkout, so that all
our views get the data they should need. 

Now that's looking good, let's go back to the shop.js file in the routes folder
then and there we can use these new routes. 

For the cart route, we can use shop controller get cart and for checkout, we can
use shop controller get checkout, the two new controller functions we created. 

Now we're almost done with the controllers and the routes, at least the basic
setup, let's now go to admin.js and there we also have one route, products, so
let's go to the admin.js in the controllers folder and there I will add a new
route, exports get products is my normal middleware function and here I
basically want to do the same as I do in get products in the shop. 

Here I simply want to fetch all products and then render my view, so I will copy
that code, go to admin.js and put that into this route, fetch all products but
of course then render a different view, I want to render admin/products, so this
view here should be rendered. 

I will also name it admin products and the path will be /admin/products to mark
that correctly in the navigation. 

With all that setup, if we go back and reload, we see a white page which is a
good sign because it's not an error and we do see a white page because actually
for slash nothing which is the route I'm on here, we load or we execute get
index in the shop controller and this actually yields us shop index which
happens to be an empty ejs view, so therefore we see an empty page, makes sense.


Let's take the code from product list.ejs and copy it into index.ejs and if we
leave it as it is and we reload, we now see shop and we see the products, the
same is the case for the products page because they share the same code for now,
cart is empty again and therefore we should add some content there too, at least
we should include the head and the navigation so that we see something, so let's
go to cart.ejs and add that include of the head, we don't need product.css here
for now, we got the body start and then we get the navigation and then let's
simply also add end.ejs so that we have a valid html document. 

With that added, if I reload this route here, we also see cart with nothing on,
add product should still work and admin products won't work, let's copy the code
from cart.ejs and let's head over to products in the admin folder, in the views
folder, paste it in there so that we at least see that and therefore if I now
click on admin products, it looks like it tries to render the 404 page but has
an error there. 

Now that means two things, for one our route seems to be wrong, in admin.js in
the routes folder, /products should be right, yeah but I didn't hook up my admin
controller there, so we should add admin controller get products here in
admin.js in the routes folder and on the other hand, also our 404 page had an
issue because there we see that the path is not defined, so what I'm missing
here is that for my 404 controller, the error controller to be precise, I also
need to add a path here because I try to extract that path in my navigation and
therefore I also should set the path here and I can set it to /404, doesn't
really matter, it just needs to be there. 

So now reloading works because that's admin products but now even an unknown
route will work again. 

So this is looking good, also note that the active item is displayed correctly
in the navigation and therefore we made a huge step forward, we added a bunch of
views, the fitting routes and controller actions even though they don't do that
much yet. 

Now it's time to work a bit on the views and add a bit of logic already. 

---