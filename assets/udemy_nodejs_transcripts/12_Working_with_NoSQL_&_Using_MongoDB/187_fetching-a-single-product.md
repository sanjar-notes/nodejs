## 187. Fetching a Single Product

<strong><em>no description</em></strong>

So we're able to fetch all the products, let's now implement the code to fetch a
single product and for that, I'm back in the shop.js controller file and here it
is the get product function I want to work on. 

Here we get the product ID as part of the url and then we want to use our
product model to somehow find the fitting product and therefore we of course
need to work on the model again. 

And feel free to implement this on your own if you got some mongodb knowledge,
it's a great challenge then otherwise of course we'll just do this together. 

So how would I fetch a single product? 

Well besides having my static fetch all method, I'll add another static method,
find by ID and you can name this however you want of course. 

Here I expect to get a product ID as an argument and then just as before I'll
call get db to get access to that database connection we have and I then want to
return the result of an operation where I use my collection and there, I will
now pass products again because it's still the same collection I want to
interact with and I will find a product here but I'll find only one product. 

And to do that, I'll narrow down the result set with find and then I'll pass a
javascript object to it which allows me to configure a filter and here, I want
to look for a product where _id is equal to prod ID because that's the ID of the
product I'm looking for. 

So with this, I'm returning theoretically all products which have this ID but I
know it'll only be one so I can use find like this and I'll only get back one
product or do I? 

Well actually find will still give me a cursor because mongodb doesn't know that
I will only get one and here we can use next, the next function to get the next
and in this case here also the last document that was returned by find here. 

So here I can then add then and catch and as always, log any error I might have
and then in then where I will have my one product, there I will log it to the
console for one and then I will return my product. 

So now this should hopefully yield my product here. 

Now with that, if we go back to the shop controller with find by ID, I either
have an error or I get my product and I try to render the product detail page. 

Now let's go to the routes and there to the shop.js file and we need to comment
in that route here for getting the product details. 

If we now save everything, let's click on details here and one thing you can see
is that this doesn't seem to work right, we always get redirected to /products
page. 

So if I go back to the starting page and we can tell the difference by the
distance between the dollar sign and the character, on the starting page if I
click details I just get forwarded to products, now why is that? 

Now this actually happens because no product ID is passed when I click details
and therefore we end up in this route. 

Now why is no product ID passed? 

If we have a look at our view and there add our index.ejs file in the shop
folder, in there we got our details button and I do actually add the product ID
here but what is the error here? 

Well I access product.id here but with mongodb, it's _id, so I should use
product_id and the same of course on the product list page, there I should also
use product _id. 

So in all the places of the app where we used product.id, we should now use
product_id. 

And with that if we reload that page here, the starting page or products page
doesn't matter, if I now click details, now something else happens. 

Now we get stuck here because we have an error but that is better than before
because now at least, we do have an ID which we try to find. 

So what's the issue here now, why do I get cannot read property title of null? 

Well for one it's worth noting that null is printed here as well and that null
should be stemming from my product model from find by ID when I console log the
product. 

So it looks like we didn't find any product for that ID and what could be the
reason for that now? 

The reason for that is that is that the ID in mongodb is actually stored a bit
differently and we can see this in compass, the ID is actually such an object id
thing. 

Now I did mention that mongodb stores data in bson format and this binary format
of json is not just used because it's a bit faster to work with, it is but also
because mongodb can store some special types of data in there and object id is
such a type. 

It's a type added by mongodb, it's not a default javascript type, actually it
doesn't exist in javascript at all and it's simply an ID object which mongodb
uses because this generates and manages IDs which look random but actually
aren't, so IDs for example are created in a way that if you create an ID now and
an ID one second later, the ID one second later will alphabetically be a higher
value than the previous one but that's just one thing. 

So object ID is an object provided by mongodb and if we look for equality, we
can't compare _id which in the database will only hold object id values with a
string because a string is not equal to the object id and the string in here
does not count, mongodb will not compare this, it compares the entire object,
the entire object ID. 

So to fix this, we simply go into our product model and in there, I'll import
mongodb by requiring mongodb from the package and now I can use mongodb to get
access to that object id type. 

So here when I compare, I can use mongodb.objectid and I can create a new, this
is a constructor, a new objectid to which I pass a string which will be wrapped
by that. 

So now if I save that and I try reloading the page for that ID, now you see this
works because now I create such an objectid object and therefore here when I'm
telling mongodb find me all documents where the ID stored in the database is
equal to that, mongodb will now succeed because we now pass on objectid object
to the comparison instead of just the string. 

And now this works too. 

It's very important that you keep in mind that mongodb stores IDs and _id and
that it uses the special objectid type for that. 

---