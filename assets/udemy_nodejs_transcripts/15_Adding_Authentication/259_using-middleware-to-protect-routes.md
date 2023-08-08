## 259. Using Middleware to Protect Routes

<strong><em>no description</em></strong>

As I mentioned in the last lecture, we could protect our routes like this but
this is not really a scalable way, we would have to add it to every route which
should be protected, to every controller action. 

So instead I want to create my own middleware which I can add on every route
that should be protected and for this, I'll first of all create a brand new
folder in my project here. 

So in the root of the project, I'll add a middleware folder, you could name this
however you want, it doesn't have to be named middleware. 

In there I'll add an isauth.js file and you can also name that file however you
want and I will simply export a function here, a typical middleware function
where you get request, response and next and then you execute some code. 

So I want to export such a function here. 

Now in that function, I'll simply implement the code I showed you in the last
lecture, so I check if we are not logged in and if that is the case, then I will
return res redirect login like that, otherwise I'll call next because otherwise
I want to allow the request to continue to whichever route the request wanted to
go to. 

Now this is the same logic as before but it's wrapped in a middleware, now we
can go to the routes folder and there, you can actually add as many handlers for
any route you want and the request will be funneled through them from left to
right. 

This means that in here, I can now import my isAuth middleware by requiring it
from my middleware folder, isAuth like this and isAuth can now simply be added
as an argument to get and you can add as many arguments as you want, as many
handlers as you want therefore and as I mentioned, they will be parsed from left
to right, the request will travel through them from left to right. 

So the request which reaches get product goes into that isAuth middleware first
and in the isAuth middleware, we might be redirecting and we don't call next,
hence the request would never continue to that controller action but if we make
it past the if check here in the middleware, we do call next, so the next
middleware in line will be called and the next middleware in line would be our
get add product controller action here. 

And this means that we can now add this isAuth middleware to all the routes here
because these routes actually all require authentication and in the shop.js
file, there also are some routes that should be protected, so I'll import isAuth
here too by requiring it from the middleware folder, like this and then there
too, I want to protect get cart because we need to be authenticated to have a
cart, I will protect post cart, I will protect deleting a cart item, posting an
order and viewing the orders, so all that is protected with the help of isAuth. 

So now this means that if you are not logged in, you actually can't access these
routes. 

I am not logged in here, now let me show this to you and let me logout and now
I'll try to access admin add product and you see I end up on the login page and
the same if I try to access cart, I end up on the login page. 

I can visit products and the details and so on but I can't visit the rest. 

So now we have route protection in place and we don't just hide the menu items
here but we really check the authentication status with the help of the session
on the server side and there, the user has no way of manipulating it, so now we
ensure that some routes, some methods are only available to logged in users. 

And indeed if I do login again, I can of course add a new book here for example
with that same image we reused a couple of times but it's still new. 

So let's add this, this works. 

So all of that can be done, all of that is supported here, you see we can edit a
product, we can also delete a product if we want to, this all works but we
protect it against unauthenticated access. 

---