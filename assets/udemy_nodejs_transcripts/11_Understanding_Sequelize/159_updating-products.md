## 159. Updating Products

<strong><em>no description</em></strong>

Let's make edit work and for this, we first of all need to load the product that
gets edited so we're looking at the get edit product function in the admin.js
controller. 

We still want to retrieve that edit mode thing and the product ID as we did it
before. 

We can also still find a product by ID, however as before, we'll not use a
callback function here but our promise where we catch any errors we might have
and then here we pass that function which gets the product to then. 

If we get no product, we redirect which is fine and otherwise we'll render the
view with our loaded product. 

With this tiny change already if we save this and we reload the edit product
page, this is looking good, the fields get populated with our values. 

Now we just need to make sure that if we do change something and we save it,
this does get saved to the database correctly. 

For that, we of course have to have a look at post edit product which gets
called once we submit this page. 

There, we retrieve all the data we need which is good but we won't save our
product like this instead here, we'll use the product model and first of all
here, I want to find the element in the database which we do want to change,  so
I'll use find by ID here and I'll pass my prod ID to find it. 

Then you know the game, we got then and catch, so let's just handle any error by
logging them for now and in then, let's work with the product we retrieved, that
product now needs to be updated. 

So here we can simply do that by now saying product title equals updated title,
so we can simply work with all the attributes our product has per our model
definition and change them, please note this will not directly change the data
in the database though, it will only do it locally in our app, in our javascript
app here for the moment. 

So I can also change product title to updated price, to updated price, I can
change the description to updated desc and I can also change product image url
to updated image url. 

Now as I said this will not directly edit it in the database, to do that we
simply have to call product save. 

This is another method provided by sequelize and this now takes the product as
we edit it and saves it back to the database. 

If the product does not exist yet, it will create a new one but if it does as
this one, then it will overwrite or update the old one with our new values. 

Now here we can again chain then and catch but to not start nesting our promises
which would yield the same ugly picture as nesting callbacks, we can now return
this here, so we return the promise which is returned by save and we can simply
add a then block here and this catch block, whoops, this catch block would catch
errors both for this first promise here and for the second promise. 

This then block will now handle any success responses from this save promise
here, so here we get back result and I will simply log updated product. 

Time to save that and to go back and edit this by adding a couple of exclamation
marks. 

Let's click update product now, we get redirected to the products page, here we
don't see our change though but if we reload, we do and in the database if we
refreshed that here, we are of course also can see that change here. 

Now do you know why we didn't immediately see that change on our admin products
page though? 

Well the reason is we redirect here and as you learned, javascript and nodejs
simply executes your code from top to bottom but async operations like this
simply get registered and started and then here for promises, we registered that
this function should be executed once the promise is resolved. 

So it will not wait for this to finish but instead move onto the next line and
the next line is this one here, so it will redirect before our promise is done. 

So we should simply move redirect into the then block here. 

By the way this also means that for now if we have an error, we never load a new
page which is not the best user experience but we'll learn more about error
handling in a separate module of the course. 

So for now, this is the setup I want to use and with that if I now edit this and
I remove the exclamation marks and I do let's say also change the price here, if
I now save that, now we immediately see the new values because now we only
redirect after the update was successful. 

---