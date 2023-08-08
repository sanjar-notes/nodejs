## 108. Working on the Navigation

<strong><em>no description</em></strong>

So let's work on the navigation and for now let's simply add links to all
important views. 

So we got our /shop route so to the starting page, I also want to have a
products link going to let's say /products and this is a route which doesn't
exist yet which we'll have to add. 

I want to set the active css class there if the path is /products and in our
controller where we render this view, we of course have to make sure that we
then provide this path property with the right value. 

Now this is one additional link, the product detail is something we don't need
to add here because we'll go there by clicking on a product, not from the main
navigation. 

The cart is something I want to have here though so I'll add another item here
in the navigation, my cart which should be reachable by going to /cart and of
course the path I check here that also is /cart but don't forget this path here
doesn't have to match this path here but it's simply easier to remember if we
keep that close together. 

Now for the admin area, I want to have that add product link still, I don't need
an edit product link because that should be triggered by clicking on a product
in the admin products list but obviously I need a link for that then, so besides
add product, I want to have an admin products link here which simply goes to
admin products and loads a list of all the products for the administrator with
administrative options and therefore here the path is also admin products. 

So this is looking good and if we now reload this, we see a bunch of new items
in our main navigation. 

Now in mobile view, this gets well a bit cut off, for now I will leave this and
add it in-between sections and then also append the code of course to make this
responsive, let's not focus on the css now though, let's focus on our node
logic. 

So we got all these items added and of course cart and so on, these routes all
don't work because we haven't registered these routes. 

Now this is a great practice for you, we got the links here so you know which
parts I want to use, you can now go ahead and add these routes, add fitting
controller functions or even new controllers if you want and make sure you
render the appropriate views. 

And if you're really feeling fancy, you can even go into these views and render
the navigation as well as some dummy content there. 

This is all stuff we did thus far, we'll do it together in the next lecture but
definitely feel free to try this on your own first. 

---