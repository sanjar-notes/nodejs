## 231. What is a Cookie?

<strong><em>no description</em></strong>

So what is a cookie? 

Well here's our setup, we got a user using browser and we got our server where
our node application runs on. 

Now the user interacts with the frontend with the views we render with the ejs
templating engine in this course but of course I'm talking about any views you
might be rendering in your project with which ever templating engine you are
using and from inside that view, let's say we have a form there to add a new
product, we submit a request to our node server. 

Now let's say that request requires us to store some kind of data in the
browser, let's say we're not working with the add product page but let's say we
have a login page and when the user logs in, we want to store the information
that the user is logged in somewhere so that when the user reloads the page and
therefore technically a new request is sent, we still have that information
around that the user is logged in and for that, we can send back a cookie with
the response we send back upon the request. 

So the user submits the login data and we return a response which can be a new
view to which we redirect to user but we also include our cookie and that cookie
simply is important to well telling the user or to storing that information that
the user is authenticated. 

We can store that information in the browser, so in the frontend so to say, in
the environment the user interacts with and we can send this with subsequent
requests to include the cookie there to send the data we stored in the cookie,
like for example that information that we are logged in to the server, so
cookies are stored on the client side. 

Now this is really abstract, let's simply try it out in our application. 

---