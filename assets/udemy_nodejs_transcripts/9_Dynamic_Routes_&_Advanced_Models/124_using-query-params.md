## 124. Using Query Params

<strong><em>no description</em></strong>

<v Maximilian>We worked a bit on the cart model.</v> Some things are still
missing. 

For example, we never display our cart and we also will never really... 

We're not able to delete an item from the cart but let's ignore that for the
moment. 

Let's instead focus on editing a product. 

We get the edit-product.ejs file and in the end, what I wanna do in there is I
want to render the same form I have for add-product. 

The difference will be that I want to pre-populate that form with the values of
the product I wanna edit. 

Now, if I'm using the same HTML code in the end, it would make sense to reuse
the same template. 

If you ever plan on using a different one, it doesn't, but here it makes sense. 

So what I'll do is I'll take my add-product.ejs code and move it into
edit-product because I find this to be the more generic name and I'll delete the
add-product.ejs file. 

So now we just have edit-product.ejs with all the HTML code in there that we
need. 

Now, first of all, that means that I have to load that file in admin.js when we
load getAddProduct. 

I no longer need the add-product path here, I need edit-product here only. 

The path down there can stay add-product because that is what we use for
highlighting a certain navigation item. 

By the way, we can get rid of these additional information pieces. 

So now this should still work. 

If I click on Add Product, I still see that form. 

So that's looking good. 

However, for editing a product, I now also want to have a route and I wanna use
that same view. 

So I'll copy that route here and add it maybe below postAddProduct to keep these
two together. 

And here I will have getEditProduct as a action name. 

And I also wanna render edit-product here. 

The difference is that here I plan on passing in my product information. 

But the problem is, of course, how should I reach this controller action? 

And my idea is that since I already have my Edit button here, if I click that, I
don't wanna call edit-product like this, I also want to add the ID of the
product I wanna edit. 

So if I grab a real ID from my products.json file like this one, then I would
have that in the URL and if I load this, now I want to have the form
pre-populated with the data for this product, and if I hit the Save button, I,
of course, don't want to create this product but simply edit the existing one. 

Now, this means that I need two things. 

The ID, I need to pass that, and the information that I want to edit a product
instead of create it. 

Well, if we go to our admin routes, we can add a new route, first of all, this
edit-product route here with the ID and you learned how that works actually. 

You can add a new route here. 

Get route will be at slash and then here the /admin is available for all routes
in the admin.js file anyways as you know. 

So it's just edit-product and then the ID, and again, this is a variable, a
dynamic path segment indicated with a colon. 

And then we can load the adminController and there the getEditProduct action we
just added. 

So this is step number one. 

And actually, we now already can go to our admin.js controller and here we
obviously know that we wanna edit a product. 

So what we can do is we can pass an additional information field to our view,
editing, and set this to true maybe so that we can check this with the if
condition to find out, for example, if upon clicking that Save button, we should
try to add the product and send a request to that route or try to edit it and
send it to a different route. 

But let's say we want to get an additional confirmation by ensuring that people
have to pass us a so-called query parameter in the URL. 

A query parameter can be added to any URL by adding a question mark and then a
key-value pair, separated by an equal sign, like edit equals true. 

And you can have multiple query parameters by separating them with ampersands. 

So we could also have title equals new, for example. 

So this is possible and this is so-called optional data. 

The path here, the route which gets reached is determined by the part up to the
question mark. 

So you don't need to add any information about query parameters you might get to
your routes file. 

These paths are not affected. 

But you can always check for query parameters in your controllers. 

So here we can check if const editMode, if this is set by going to our request
and there will be a query object. 

This is also created and managed by Express.js. 

And you can access your data here by simply trying to access the keys you got in
your query parameters. 

So for this query parameter that was added, you could check for edit. 

This would be your key. 

So I can try to access edit here and only if this is set somewhere in the list
of query parameters, which can be separated with ampersands as I mentioned, if
this is set, then I will get the value which is set. 

So now I would have true in editMode. 

And if I don't have it, if I don't find it, I'll simply have undefined, which
conveniently is also treated as false in a Boolean check. 

So we can then pass editMode here and now we only enter editMode if this is set.


And therefore, we could also check if not editMode and then simply redirect. 

Now, this is kind of a redundant thing here to do to be honest because actually
here, we already know that we wanna edit the product. 

But I want to show you how you can use query parameters to set optional
information, pass additional information. 

Often, this is also used for something like tracking users or for example, for
keeping a certain filter the user set on a page. 

Here, I'll use it to explicitly set that editMode and redirect otherwise. 

So now I extract this and try to load this and therefore if I now save this and
I connect my newly created action here with the route as I already did it here,
if I now reload this page with the dynamic segment set and the query parameter
added, then I land on this Add Product page, which is incorrect. 

I need to change that path. 

But that means that I don't get redirected, so I made it in there and editMode
should be set to true. 

Now, we can also set the path here to edit-product to make sure that this is not
highlighted here. 

Instead, I want to have no highlighted section and this will not be because I
have no check in my navigation where I would look for this specific path. 

And I'll set the page title also to Edit Product for this route. 

So now if I reload this, this looks better. 

And as a next step in the next lecture, I now wanna use the fact information
that I noted I'm in editMode in my view to pre-populate this with product
information and then also to change the button caption and the button action. 

---