## 245. Making "Add to Cart" Work Again

<strong><em>no description</em></strong>

So I clicked add to cart in the last lecture and we're now failing to do this
and if we go back, we actually see an error that request session user add to
cart is not a function. 

So we somehow fail to execute our Add to Cart function, so basically our
functions that normally are available on the user object and why is that? 

The reason for that is that previously, in previous setups, we always store the
user in the request and this was a per request action anyways and we fetched
that user for every request in the middleware in app.js, right, so we fetch the
user from the database and mongoose automatically gave us a full user object not
just the data in the database but the full user model with all the methods and
we stored that user model in the request, with the session this works a bit
different. 

With the session we are not fetching this for every request instead we store the
user in our session upon logging in here. 

Now what happens to the user there? 

Well it gets stored to the database. 

If we refresh there, we can see here is our user object and this is now just the
data. 

Now for every new request, the session middleware does not go ahead and fetch
the user with the help of mongoose, it fetches the session data from mongodb,
that is correct but for that it uses the mongodb store and the mongodb store
does not know about our mongoose models. 

So when it fetches the data from the session database, when it fetches this
data, it only fetches the data, it does not fetch an object with all the methods
provided by mongoose. 

Now what can we do regarding that? 

Well one thing we can do of course and now we're reverting back a bit, we can
re-add that middleware which we had earlier here after we initialized our
session. 

So here I have my general middleware which we used before to store our user in
the request and we can take our logic from our post login route where we fetch a
user for a given ID, move that back into that middleware, so exactly what we had
before, instead of redirecting we'll call next so that the incoming requests can
continue with the next middleware but in here, we don't want to store anything
in the session because the session is already something which will be managed
for us automatically and for the incoming requests, we register the middleware,
the middleware will then basically look for a session cookie, if it finds one it
will look for a fitting session in the database and load the data from there. 

So by the time we reach this middleware, we'll have our session data loaded. 

Now this means that now we just want to use that session data to load our real
user, to create our mongoose user model and how do we do that? 

Well we don't need to reach out to the database again, instead we can again set
the user for this request only and now here I want to create a user based on
data stored in the session, so data that persists across requests and I will
create that user and store it in the request user which will then only live for
that request but it's fueled by data from the session and therefore it also
survives cross request you could say and I simply need to do that because I need
a mongoose model to work with, because the data we store in the session storage
in mongodb there, well we retrieve it as just plain data not as a mongoose model
with all the cool methods mongoose gives us and that is why we get this error
regarding add to cart not being found and so on. 

So here I will initialize request user and actually I don't want to find a user
by id like this, I will find a user by reaching out to request session user id. 

This make sense I guess because that is the data, the user is what I store in my
session and I want to get the ID and then find that user in the database with
the help of the user model which is provided by mongoose of course and then
here, I get back a mongoose model user which I store in request user and this is
exactly what I need now to make sure that I have a mongoose model to work with
so that all these cool mongoose methods work again and now we need to adjust
admin.js and shop.js again and replace requests session user with request user
again because that is where I'm storing my mongoose model user. 

So let's do that, in shop.js and in all the files where I do use requests
session user, I want to mark these all with command or control D and revert it
back to request user because now we store our mongoose model in that request
only object again, do the same in admin.js. 

So in, not for logged in because that's just true or false, we don't need to
turn this into anything but for all the places where I do use my request session
user here, all these places which should only be one here is now request user
again. 

Again this will not mean that it's now only existent for this request, the
mongoose model object is but it's fueled by data that's stored in the session
and therefore data that persists across requests. 

And now that we saved all of that, let's go back and let's try adding this to a
cart again and now this works as before as long as I'm logged in, if I do log
out we now get an error, that error is now stemming from my app use function
which is triggered for every request and this will simply fail after logging out
because request session user ID is not set there. 

Well we can fix this in this app use function app.js by checking for the
existence of requests session user and if we don't have one, so if I don't have
a user stored in my session, then I can just call next and I return next so that
the code thereafter, this one will not be executed, this will only run if we do
have a session user. 

So now with that, we can safely reload the starting page, this works. 

I can login again, I can add this to the cart, I can also add this from the cart
from the details page, I can delete this and I can log out and this should all
work. 

---