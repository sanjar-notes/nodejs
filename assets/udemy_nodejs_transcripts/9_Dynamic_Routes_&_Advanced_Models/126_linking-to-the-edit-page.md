## 126. Linking to the Edit Page

<strong><em>no description</em></strong>

Let's make sure we can reach that edit product page through a route and for that
on our products page here, on the admin page this added link here, added product
should also include the ID of the product and again we can use ejs to simply
inject that into our path by accessing Product ID. 

That's all we need here, if we now reload this page and click edit, we get
redirected, what could be the issue here? 

Well remember that we added our query parameter right and we're checking this
query parameter in our controller and if we don't find the added query
parameter, added mode will be undefined and therefore we get redirected. 

Now this is of course just a bonus but it's important for you to understand how
query parameters work and therefore we have to set this too when creating our
link to this page. 

So let's go back to products.ejs and don't just add this ID but also simply
append that query parameter where I set added equal to true. 

With that if I now save this and I go back to admin products and click edit, now
we load this product for editing. 

So this is looking good, let's now make sure that clicking update product which
does already reach the correct route does then also do something. 

And for this first of all in admin js, we need to register this route. 

So let's add a new post route which is at added product, this will not receive
any dynamic segment because it's a post request so data can be enclosed in the
request we're sending, so let's now work on the controller here and add a new
action, post edit product which of course receives the request object, the
response object and the next function as all our middleware functions which our
controllers just are and in here, what do we have to do? 

Well we basically want to construct a new product and replace the existing one
with this product This means that we have to do some work on the product model,
we'll do that in the next lecture. 

---