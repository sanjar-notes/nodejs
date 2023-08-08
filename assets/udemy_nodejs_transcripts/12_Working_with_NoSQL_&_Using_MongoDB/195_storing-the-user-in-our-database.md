## 195. Storing the User in our Database

<strong><em>no description</em></strong>

Ok so time to use our user object and the question of course is where do I want
to use my user object? 

Well I want to use that user object when creating a new product, right, when
saving a product, I want to store a reference to a user here or embed the entire
user data as you learned. 

However for products in users, you could actually find arguments for both
approaches here, you certainly don't want to enclose all the user data in an
embedded document because that would mean that if the user data changes, you
need to change that data in all products but if you do include something which
is unlikely to change very often, like the username for example, well then you
could certainly go ahead and embed that together with the ID so that you always
have that ID to fetch more data about the user if you need to, you've got to
find by the method in the user model after all or that you have at least some
snapshot data like the username available immediately, if that should change,
you need to update it everywhere. 

The alternative to this is that you just store the ID, so just a reference and
therefore if you need connected data, you always have to fetch it manually from
two collections  but on the other hand you might not do that too often and
therefore here indeed when I fetch the product, I don't really need the user
data, we're not displaying the user name anywhere in our app, so I actually just
want to store the user id so that we know who is connected even though we're not
fetching that a lot. 

Now what does this mean for our application here though? 

Well it means that when creating a new product, we can pass the user id, we can
accept the user id here, so this user ID is equal to user ID, we store this as a
property of our product now and with that, we have all we need in the product
model. 

Now we need to make sure that we do pass that user data when creating a product,
so in the admin.js controller when adding new products, here I want to pass null
for the product ID because we dont have that when creating a new product but for
the user id, I want to pass the ID of the user which as you know we now store in
our request. 

We do this in the app.js file right, we have that middleware which we set up in
an earlier module where we find that user and where I then store that user in
our request. 

Now this is a bit of a constructed example because I'm storing it just to
extract the ID which I hardcoded here, so we could just hardcode it into our
code anyways but the idea here of course is to show you how you can extract the
user in one central place and then reuse it in any other route and that's the
idea here. 

Later once we get an authentication, we'll manage that user a bit differently. 

So for now, we just have that user object in the request and therefore in the
admin.js controller, here I can access request user and then _id which will be
just a string here because when retrieving data, the object id is converted to a
string for us, so we have just the string here. 

Now with that, we should actually store the user ID when creating a new product.


Let me first of all delete that old product and then let's quickly add a new
product here and I get an error that I can't read Property ID of undefined and
this should be coming from inside our admin.js file here when I try to access my
user _id, so something seems to be going wrong here. 

I'm storing the request user here though, let's go to the user model, find by
ID, let's add then and catch here and catch any error we might be getting when
fetching that user and here I'll also console log the user object I'm getting
right before I return it again. 

And with that let me try to reload the admin product, add product page and I now
get an error. 

We did retrieve the user here but then I sent duplicate headers by the look of
it, yeah because I'm calling next too often here in app.js, . 

since I added the other code again, I don't need to call next at the bottom of
it. 

So let's save that to not call next too often. 

Let's now reload this page here and now I just fetch the user with the ID which
is a string here, so that is actually valid. 

Now let me try adding this again and now this works, so it was that error with
the double next. 

So now if we have a look at our products here, we see that products now also
have a user ID which is just a reference pointing at the user who did create
that product which is one way of establishing relations the way you already know
from MySQL of course, this is not an embedded document but here, the argument
simply is when we're fetching products, we don't really need any user
information hence we do it just like that. 

This of course will change once we start storing orders, there you could say it
does make sense to store information about the user, for example the e-mail at
least and for the product you want to store the title and the price maybe. 

So there it makes sense to suddenly aggregate this together. 

Speaking of that, why don't we work on cart items and orders next. 

---