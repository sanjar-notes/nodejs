## 392. Using & Validating the Token

<strong><em>no description</em></strong>

Now that we're generating a token and we're passing it to the client, we need to
make sure that the client can pass back the token to the backend, to the rest
API and we then check for the A, existence and B, validity of the token before
we allow the request to continue. 

So for example on our feed routes, on all these routes, none of these routes
should be public, so if no token is attached to the incoming request, we should
simply block access here and this is what I'll work on now. 

For that I'll add a new middleware and I'll create a new middleware folder for
this, you could place it anywhere though and I'll name it isAuth.js, that is the
name of my file. 

In there, I will import my json web token package because we'll need that
package to validate incoming tokens, then I'll export one function in that file
and that will be a normal middleware function with request, response, next so
that I can use it as a middleware and now I first of all need to extract the
token from an incoming request. 

Now currently we are not attaching the token to any requests, how could we
attach it? 

If we go back to our frontend let's say in feed.js for loading posts we want to
attach the token, how could we do that and there are a couple of options. 

You could add a query parameter, something like token equals and then enter your
token value there and then append other query parameters, that would be a valid
option, nothing wrong with that. 

You could include it in the request body but that is not ideal because for
example get requests have no body, so that is not a solution you should use
unless you never have authenticated get requests. 

A great solution is however that you use a header. 

It keeps your urls beautiful, of course that might not be the most important
argument but still, it keeps your urls beautiful and a header makes a lot of
sense for meta information like well the token which it is in the end. 

So let's add a second argument in the load posts function in the feed.js file in
the frontend, a second argument there to the fetch method and here I will add
some headers to this request. 

Now I will not add the content type because I'm not sending any data here but I
will add the authorization header. 

Theoretically you can add any header you want but this is an official header, a
header you officially use for passing authentication information to the backend
and please remember that on the backend in the app.js file where we added our
course headers, I did enable the authorization header, you need to have that
enabled for this to work. 

So now I'm setting my authorization header there and I'm setting it to a value
which is not just the token but actually bearer whitespace and then this props
token allows you to get the token in the react app. 

Why bearer? 

Well this is just a convention to kind of identify that the type of token you
have and the bearer token is simply an authentication token, you typically use
bearer for json web tokens. 

It's not a must, you could actually work without that but it's a common
convention and therefore I want to keep that convention. 

So this is how I could add my token to that get posts request on the frontend,
now on the backend to extract it in my isAuth middleware, I will create a new
variable or a constant token and then access my request and with the get method,
I can get some header value. 

The header is the authorization header of course and there, I will get this
bearer whitespace token. 

Now I'm only interested in the token of course, so I will split on the
whitespace which comes after bearer and I'll get the second value which is the
token then, so this is the token, now I will try to decode that. 

So I will actually use a try catch block because it could fail and I will create
a new variable here, decoded token and decoded token will then be JWT and there,
you have a verify method, this will both decode and verify your token. 

You also have a decode token but this will only decode it and not check if it's
valid, so definitely use verify here and then you pass in that token which you
extracted from the header and then that secret and that has to be the same
secret you used for signing the token of course, so the same secret you used in
your auth controller, this one otherwise you'll not get a matching result. 

So this is the secret which we will use for validating the token. 

Now this could fail, so here I'll have a catch block and there, I want to add a
status code to my error of 500 and then I will throw the error here. 

Since I'm in a middleware, now the expressjs error handler would take over,
otherwise we know that decoding worked and I'll check if it is undefined which
would be the case if it didn't fail technically but it was unable to verify the
token. 

In this case I'll create a new error, not authenticated, add a status code of
401 and throw this error. 

If we make it past this if check, we know that we have a valid token however and
that we were able to decode it, so now I'll just extract some information from
the token, the user id and I will store it in the request so that I can use it
in other places where this request will go, like in my routes and there I'll
just access the decoded token which now simply well is basically the part on the
right here, we can now access that data since we decoded it. 

So there I can now access my user ID field which I stored in the token, this
will be useful for later, authorizing access to for example deleting posts
because now I know the user ID stored in the token and that should match the
user id of the post we tried to delete later and then I can forward this
request. 

So we'll either have an error if we have no token attached or everything will be
fine. 

Now we can add that middleware to our routes and I will add it to my get posts
route. 

So here get posts should use that middleware, therefore I first of all need to
import it by requiring it from the middleware folder, isAuth and I will add it
like this here. 

Now I only can get posts if I do add a token. 

First of all, let me show you how this fails, if I remove this header, so this
extra configuration on my get posts request in the frontend. 

If I remove that and I reload the page, I get failed to fetch posts and in the
console log, I also see that here because it fails to read split of undefined,
we get a technical error because in my middleware, it can't get anything from
that header because the header is not defined. 

Therefore we could add an extra check here and first of all get the header, auth
header would then be request get authorization and if this is undefined, so if
we can't find the header, then I will already create an error here, not
authenticated because we don't even append the token so we certainly are not
authenticated. 

I can set my status code of 401 which is better than 500 and I can throw that
error and then down there, we know that we do have the auth headers and we know
we can split it, so that's an improved way of handling that. 

Now if we reload on the frontend, we still get that error but technically we now
have a 401 error which is better. 

Now I can add that code back where I add the token but let's try adding some
rubbish here which is not a valid token, now if that reloads it still fails and
it fails because now the json web token package has a problem with the format of
our token. 

So now let me revert this and add the valid token and now as this reloads, now
our posts load because now we are validating this and we have a valid token
indeed. 

So this is now how we can validate on the server side, how we can check whether
the token is valid and then grant access and now we just have to do that for all
our routes before we then also make sure that only users who created something
can delete it because right now of course, well I can delete everything as you
can see. 

---