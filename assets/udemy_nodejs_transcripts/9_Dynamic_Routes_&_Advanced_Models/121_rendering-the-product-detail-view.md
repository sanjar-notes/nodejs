## 121. Rendering the Product Detail View

<strong><em>no description</em></strong>

So let's add a view or we do have the view but let's add some logic in that view
and for this, I'll take the code from one of my other simple views like
orders.ejs class and paste in there so that I got the head and also my
navigation and so on. 

Now in here, I don't want to output nothing there of course instead here, I want
to output my product information, so my product detail. 

For this I will quickly give this main element here a class of centered and find
tune my css code real quick, in the main css file let's simply add a class, you
can add it anywhere, I'll add it relatively at the top centered where I set text
align to center for now, so that everything is centered horizontally. 

Now in there, I'll output my h1 tag and there I expect to get information about
the product we loaded, so here I want to get some product and output the title. 

Now right now we're not rendering this view and we're not passing the data into
it but eventually we will. 

So here is my title, then maybe render a horizontal line and then let's display
an image for this product because we got an image, right. 

So I will add a div here and in this div and image and there I will output
product image url, that is the field in which we are storing the image, check
your model in case you're not sure and as an alt text I'll output product title.


Now below the image, I want to output a h2 tag where I output my product price
like this and beneath that, a paragraph with my product description, just like
this. 

So that is my detail page there and if we now save this, we have to make sure
that we render this view for our detail route, so in our controller where we do
get this single product data instead of redirecting here, I'll remove that and
instead of logging this to the console, I'll say res render and I want to render
my view in the shop folder and there it's the product-detail view, so basically
the filename here, product detail and we have to pass in some information. 

We do that by passing a javascript object and in there, we now need to pass in a
product property because we're accessing this here in the view. 

So back in our shop.js file, let's pass in product and set this equal to our
product we're retrieving here. 

So product on the right side of the colon is the product we're retrieving,
product on the left side is simply the key by which we'll be able to access it
in the view. 

With that, let's save that and go back to products and load the details here and
we get an error that we're missing the page title, showing us which line is
throwing the error and also tells us page title is not defined and this makes
sense because in the head of our of each page, we're outputting the page title
here, so we also have to pass that into our view. 

So in shop.js here, let's make sure we don't just pass the product but also the
page title and here we can actually use product title to dynamically set the
page title to the title of the product. 

With that simply reload this page, I'm also missing the path now because in the
navigation, we're using that to determine which path is active and now there the
question is which path do we want to highlight? 

In a navigation file here, we obviously have no path, no link to this exact
product but I think it makes sense to highlight the products link here because
we're still in the products area, just in the detail for a single product. 

If we want to highlight this, the path we should pass is /products because
that's the path we're checking here. 

So in shop.js . 

file, I'll set path to /products here because this is the path for which I want
to mark the navigation item as active. 

Now if we reload, this looks better and now here this doesn't look too shabby. 

We got a nice detail page here, does the trick for now, let's maybe finish it up
by adding an add to cart button below the product but with that I'd say this is
what we need for the moment. 

So let's go back to our product-detail.ejs file and below all that information,
I will now add a little form which leads to cart with a post request because I
want to add that product and I'll add a button with class button and type submit
and the route for this is missing still where I say add to cart and now with
that if we reload, we got that button here too. 

So this is now working and this is looking decent. 

With that I'd say why don't we work on that add to cart functionality as a next
step. 

---