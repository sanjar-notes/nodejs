## 393. Adding Auth Middleware to All Routes

<strong><em>no description</em></strong>

We added this isAuth middleware on the server, let's now protect all feed routes
with it. 

Now this is super simple, we just copy that middleware and we add it to every
route we have there. 

As the first middleware before we do anything else because if no token is there,
we don't even need to continue with anything else. 

Every route should be protected here, so we simply add this to every single
route. 

Now once you did add it to every route, you have to make sure that you pass the
token on the front end. 

So this header set up where you add this authorization header, this is something
you now need to add in a couple of places in the frontend, for example our edit
handlers there. 

There on the fetch request, we now should also add some headers and the headers
should contain our authorization token. 

If we scroll down further, we also got delete post handler, well there obviously
we also want to add some headers and that one header we want to add is our
authorization token. 

Of course we can also fetch single posts, so in this single post.js file in the
frontend code where we fetch a single post, we also want to pass that second
argument to fetch, add our headers and there, add the authorization header. 

Now we should be able to navigate around as long as we are authenticated but I
also want to lock down access to ensure that I can only edit and delete posts
which I actually created. 

Now in the last lecture, I deleted all posts, so let's make sure that we first
of all connect posts and users when we create new posts. 

---