## 98. Adding Controllers

<strong><em>no description</em></strong>

In our project as I mentioned in the previous lectures, we already got some
views and we'll leave that exactly in the state it is. 

We've got that views folder with all our templates inside of them. 

Now what's missing is a folder for the controllers and the controllers
themselves and for the models. 

Right now that is all mixed into our route files or into our route functions
here, the way we route won't change, we use the router and we have such a
middleware function but actually, the logic that is executed here that is the
typical controller logic, we're interacting with our data even though that's
just one line here but still and we're then returning a view and that's exactly
this in-between logic that makes up a controller. 

So therefore you could of course say well we already got controllers, these two
files hold our controller logic and you would be right but especially as our
application grows if you put everything into your route files, this can quickly
become a very big file and therefore separating this into separate files can be
a good idea because you can then quickly see which routes you have and if you
want to see the code which executes per route, you simply go into the respective
controller file and function. 

So therefore let's create a new folder here and let's name it controllers, like
this. 

Now in that controllers folder, I will create controllers for the
functionalities I have. 

Now you can have a one to one mapping between your route file names and route
file number and your controller files but you can also split this differently,
maybe you want to group your routes by prefix, like here, these are all our
admin routes but the thing you execute there might fit two different
controllers. 

Let's say you have admin routes which allow you to change your admin user
profile and products, you might have all these routes in the admin.js file in
the routes folder but you do have two different controllers, the users
controller or admin controller and the product controller. 

So this is up to you and I will indeed create different files here, I'll have my
product.js file or products.js for my product related logic and I will put all
the product logic in there, so even my shop route here where I also work with
products, I'll put that logic in here because all logic I have in my app thus
far and this will change later but all logic thus far is related to products and
therefore, I want to have it in a controller that only works with product logic.


And if I later add some user logic, that will go into a user controller and
maybe we even split the product controller into a user product and an admin
product controller but for now, we'll leave it like this. 

So in that products.js file in the controllers folder, I now want to add that
code here basically. 

So this middleware function we're executing here, this code for add product
right where I just render this add product route, this can now go into there and
the question just is how  because this would be incorrect. 

Well in the end we want to link to this function and we want to link there from
inside our route, so here we basically want to add a link to this controller
function here. 

So therefore what do we need to do? 

We need to export this function in the product controller file and we can do
this and we'll have multiple exports by using exports and then any name of our
choice. 

Remember with this syntax, we can have multiple exports in one file easily. 

So here I will now export my get add product function here and the name is up to
you but I name it like this because in the end this is what we do, we get the
add product page. 

Of course you could also name it get add product page here but I will just
describe what this in the end helps me do and it helps me get everything I need
to add a product but you can name this to your likings. 

So now I get this product and I still have my function which receives the
request object even though we're not using it here but we still get that, the
response object which we are using and next because this still is a normal
middleware function expressjs understands because I will now import get add
product into my admin.js file and still using here on my route, this will not
change, I just split my code differently. 

So with that, let's add an import, by the way we can get rid of this root dir
import because I'm not using that utility anymore, you can also therefore delete
the entire file or even folder but that's just a side note. 

So let's now import our controller and there, I will import products controller
by requiring my controllers folder and there, the products file. 

So since I'm doing this from inside my admin.js file here, I need to go up one
level until I'm in the root project folder and then I go into the controllers
folder and then I pick that products file. 

So now products controller bundles all the exported functions and right now,
this is only one of course but it will become more. 

So back in admin.js here on this route where I want to use that, I can now
simply say products controller.get add product. 

And we don't execute this function so please don't add these parentheses,
instead we just pass a reference to this function. 

So we're just saying or we're just telling express, the express router that it
should take this function and store it and whenever a request reaches this
route, it should go ahead and execute it. 

Now we can repeat this for adding a new product, I'll cut this code and go to my
product controller and simply add a brand new export and I'll name this post add
product because this is what I do here, I post a new product I add the product
therefore through a post route and this will be the function I just copied. 

Now the problem here is that we refer to products which is of course something
we don't have in that file yet, so I should also go into admin.js and take my
products array which I have there, cut it out of there and then in products.js
in the controllers file, I will add this array and I'll change this later too
but for now, let's simply add it here, products should be our empty array. 

Now back in admin.js, we can now also use our new products controller function
we just added, post add product in exactly the same way we use get add product
and of course we can now tweak our exports here, we no longer need to export
products in our admin.js file because we no longer have that array in here. 

So instead I'll just export my router again as I'm doing it in the shop.js file.


So with module exports equal to router, that is what we have here too and this
just means that we now have to adjust the app.js file where we are importing
this, there I'm importing admin data, now a more fitting name is admin routes
again because now we just export routes and nothing else and of course that also
means that here where we use that, we just use admin routes because we change
that export. 

Ok good, so we get this set up, now let's also do the same for shop.js. 

There I also get a function which is related to products, so let's cut it and in
products.js here, I will add a new export, exports get products like this. 

If I do this, I have my function here which will in the end return or render
that page with my products and one important note, obviously products is now an
array which is available in that file, so products here doesn't have to be
extracted from anywhere and again we will change this. 

So this is now my finished products controller in shop.js, we can now remove
these two imports because we don't need them anymore instead I import my
products controller by requiring it from the same path as in the admin.js file
and here for this get route, I will simply say products controller get products.


With all that, let's save this and see if it still works. 

If I reload this page, this all seems to work and if I add my first book here,
this also works. 

So it's still working as before but now we're using a controller. 

Now let's see what else we can do here. 

---