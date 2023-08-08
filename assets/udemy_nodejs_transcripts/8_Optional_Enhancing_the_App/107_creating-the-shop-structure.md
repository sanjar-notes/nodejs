## 107. Creating the Shop Structure

<strong><em>no description</em></strong>

So back in code, let's quickly think about our project. 

In the end, what we're building here is an online shop, so what we need is a
starting page, we need a page where we can view all the products that are
listed, we also want to be able to create new products, to edit products, as an
administrator also to delete products, we want to be able to add products to a
shopping cart, to go to a checkout page and pay for the products and then also
as a customer, we want to be able to see our orders. 

So that's a lot of stuff and we'll build all that logic throughout the course
but we can already get started and for that I will get started in the views and
I'll try to add the views for the different things we'll need, we get add
product and shop.ejs thus far. 

Now let's add more views here and I will also split them in sub-folders to group
them together basically. 

I will add an admin subfolder and I'll move the add product view into the admin
subfolder for example, I'll also add another subfolder and that will be my shop,
so this is the customer facing part you could say and there I'll have my
shop.ejs file, though I will rename this to product-list.ejs because that is
what I want to have on this page in the end, it should be a page with a list of
all my products. 

Now this of course is not a complete list of all of the views but we already
need to add some changes as I restructured the folder structure here, for the
product list for example for my includes, this path is not correct anymore,
product list is now in the shop subfolder so I first of all need to go up one
level until I can dive into the includes folder. 

So here in that path we should have ../ which means up one level and the same
here for my navigation. 

So all that should be done and also for end.ejs here and of course the same for
add product, there you want to go up one level, here also up one level and down
there, up one level. 

With this adjusted, we also need to make sure that we render the correct views
because in our controller, the products controller, we return the shop view here
but this is seen relative from inside the views folder. 

However first of all, we rename this to product list and second it's now in a
subfolder named shop. 

So actually we have to go into shop and then /product-list, this is the new path
to our view. 

And the same here for add product, admin add product here this is now in the
admin subfolder, so we should go into the admin folder and then render add
product. 

With these changes in place if I reload my page here, this should all still work
and indeed I can still switch, so the existing views are rendered correctly so
that seems to work. 

Now we can add more views here and for that in the shop for example, I'll have
an index page, so the starting page basically, right now this is my product
list, well I will add a new area, the products area which should render the
product list and the starting page should be a different page and in the end, it
will be very similar but it should display less products let's say. 

Now in the shop, I also want to have a product-detail.ejs view where if I click
on a product, I can see that and I want to have a cart.ejs view which I can
basically see if I click on the cart in the menu and we'll have to add this menu
item of course. 

And there's one remaining view for now and that is my checkout.ejs view which
will be the checkout flow which we can start from inside the cart. 

Now in the admin area, we got add product, I also will add edit-product.ejs so
that we can do that too and I will also add my list or product list.ejs view. 

Now we got a product list view already in the shop area, the admin of course
also needs to be able to see that and just to avoid name clashes or confusion,
you could name it like this, wouldn't be a problem but to not confuse you when I
refer to these views, I'll name it products.ejs in the admin area and product
list in the shop area but you could absolutely use the same name because they
are in different folders. 

So now we got that setup and we'll add more if we need more but that looks
decent, now let's go to the navigation and there I also need to work on the
available navigation items because right now if I structure this a bit different
to make it easier to read like this, we get two navigation items, one for the
starting page and one for adding a product in the admin area. 

Now of course you could argue that you in general don't want one navigation with
all the normal customer options and all the admin options but that is something
we can tackle later, for now in the next lecture, I want to continue working on
this and add all the links to all my views for the moment so that we can then
refine this throughout the course. 

---