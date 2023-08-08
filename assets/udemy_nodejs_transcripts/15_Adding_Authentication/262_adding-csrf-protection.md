## 262. Adding CSRF Protection

<strong><em>no description</em></strong>

So we added csrf token protection but it will only work if we are visiting our
get index page. 

Now we want to have such a token and by the way also, our authentication status
on every page we render. 

What we can do to get it onto every page is we can remove it from our render
function here and instead tell expressjs and this is now totally unrelated from
csrf thing, tell expressjs that we have some data that should be included in
every rendered view. 

We'll do this in the app.js file and there after this middleware where we
extract the user but before all our routes, I'll add another middleware, a
normal middleware with our normal middleware function with the three arguments
and in there, we can use a special feature provided by expressjs, we can access
a special field on the response, the locals field. 

This allows us to set local variables that are passed into the views, local
simply because well they will only exist in the views which are rendered. 

So there, we can add our isAuthenticated property which I removed from the
render function where I access request session is logged in and I can also add
my csrf token variable which I get from request csrf token from this function. 

So now for every request that is executed, these two fields will be set for the
views that are rendered and then we have to call next so that we are able to
continue. 

With this if we go back and we reload this page, seems to work, seems to work
and now let's also try signing in where we also have a post request and now this
fails and now do you know why? 

Well because I do pass my token into all views but in the views, I still need to
use it. 

So for that, we have to repeat the code we added to the navigation, we need that
hidden input with that name and that value and we have to add it into all our
forms and that is something you just have to do. 

So for example here in the Add to Cart post form, we need that hidden input with
the csrf token and also in admin edit product, we need somewhere in that form
that hidden token input. 

The same for our auth routes of course, when logging in we need that hidden
input and the same for signing up, this is required. 

In the products.ejs in the admin folder, there we also have a form for deleting
a product, we need the token in there too. 

And in the shop in the cart, we also have a delete cart item button, we need the
hidden input there as well and also down there for the order now button, this
also sends a post request and we need our hidden input there, our csrf token. 

On index.ejs we don't need it, in add to cart I just added it so there we
already have it, in the product list page, it's the same, it was added to add to
cart and on the product detail page, I also only have add to cart. 

On the orders page here, we also have no post form. 

So now we should have this token everywhere where we need it and if you save all
that and you now go back to your let's say starting page and you visit the login
page and you do login, this now works because we have that token, we also can
add items to the cart, we can also order them, well there is an error which
we'll fix in a second. 

So for now let's not order them but let's delete them, this works and generally
this works. 

Now let me fix this bug here which is not related to the csrf token in the next
lecture real quick but this hopefully and that is the main takeaway here, shows
you how to use csrf protection and this is a crucial thing which you have to add
to any production ready application, it's not optional otherwise you'll have a
huge security issue on your page. 

You need to add this to ensure that your sessions don't get stolen. 

---