## 431. Extracting User Data From the Auth Token

<strong><em>no description</em></strong>

The basic create post mutation is in place but now we need to be able to
validate our token and extract the user from it and that is not too far off on
how we did it in a rest API. 

First of all, we need to ensure that we send the token in a header of our
incoming request and if we have a look at our frontend code and there at feed.js
which is where we do create new posts, we do that in the finish edit händler,
there we do indeed attach our token to the outgoing request and this is still
the wrong url here but this is how we will send the request in the end. 

So we'll have that token in the url and previously in the rest API, we use
isAuth middleware to get our token from there, validated, extract the user data
and add the user data, the user ID to the request object and that is pretty
close to what I want to do now. 

I will just tweak it a little bit, I'll name it auth because it's not just there
to validate authentication, it will also give me the user data but that is
something purely cosmetic. 

In there I will still first of all get my auth header, I'll check if it is set
and if it is not set, then I will do something different though, I will not
throw an error, instead on my request I'll set isAuth to false so that I can
handle this inside of my resolvers and then I will return next to continue with
the next middleware and not execute the other code here, that is why I also have
the return statement. 

If we do have the auth header, we continue, we extract the token as before, we
try to decode it just as before, make sure this key here matches the key you
used in your resolver for signing the token by the way, if these two don't
match, you have no chance of validating your token. 

We catch an error but if I get an error, I again don't throw it, instead I set
request isAuth to false and return next here too to not execute any other code. 

If the decoded token is undefined, I also throw no error, instead here again I
set isAuth to false and I return next. 

And if I make it past all these checks, I will get my user ID from the decoded
token and I will set isAuth to true, so that is a new property I add to the
request and I call next. 

Now this tweak middleware is something I add in app.js before my graphql
endpoint. 

So here, I will simply import that auth by requiring it from middleware auth,
this is my middleware and I will add it here like that. 

This middleware will now run on every request that reaches my graphql endpoint
but it will not deny the request if there is no token, the only thing it will do
is it will set isAuth to false and then I can decide in my resolver whether I
want to continue or not and this is the next step. 

In my resolvers there, I don't care about isAuth in create user and so on, so
there I will just not do anything with that information. 

In create post here, I will first of all check if request isAuth, if that is not
true because then I know hey the user is not authenticated, I certainly don't
want to grant access to creating a post. 

So if the user is not authenticated here, then I will create a new error, not
authenticated and I'll set my code of let's say 401 and then I'll throw my error
and therefore the other code in this resolver here will not execute. 

If the user is authenticated, we can continue and then we validate the input and
then before we create the post, we can now also get the user from the database
because remember that we do store the user id in our request as well. 

So in the resolver right before creating the post now, I can get my user by
awaiting user find one or not find one, I can actually use find by ID of course
and there I pass in request user id, so exactly the thing I'm storing here. 

I passed it in and now I get a user. 

If I don't get a user here, then something is wrong and I will throw an error,
so here invalid user maybe, set the code to 401 and throw that but if we make it
past that, we have a user object with which we can work. 

And now in the newly created post, I can set the creator equal to my extracted
user, so to the user I got from the database. 

Once I created the post, I can now also use that user and access the posts of
that user to push the created post onto that list of posts, so to set up that
connection. 

That is now it and now we need to work on the frontend to also send a request to
this endpoint so that we can see that in action. 

---