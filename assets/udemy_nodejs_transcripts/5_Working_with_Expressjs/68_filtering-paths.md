## 68. Filtering Paths

<strong><em>no description</em></strong>

There is one other notable feature about the express router that I want to show
you, now we have a catch all route and we got our outsourced routes here. 

Now sometimes these outsourced routes have a common starting path, so let's say
all the admin routes actually are triggered with admin/add-product and admin,
maybe also add product, we can repeat the path here because we got different
methods, get and post, so these will be two different routes too. 

So that is one important take away already, the same path can be used if the
methods differ. 

Of course here in the form, I should also point at add product then but there is
another important take away. 

If we have such a setup where our paths in such a router file start with the
same part or with the same segment here, we can take that segment out of this
route here and then go to the app.js file and add it here, so add that segment
as a filter. 

Now only routes starting with /admin will go into the admin routes file so to
say and not only that, it also will or expressjs will also omit or ignore this
/admin part in the url when it tries to match these routes, so now /add-product
will match the /admin/add-product route because /admin was already stripped out
here you could say, let me show this to you in practice. 

If I reload my add product route, we get page not found because this does not
exist anymore, this is now /admin/add-product and indeed, here is the form and
if I now add my book again here and hit add product, I get page not found and
the reason for that is that of course here in form action, I'm leading to
/add-product but this should be /admin/add-product too because we want to reach
that route which is the admin.js file which is only reachable through requests
that have /admin at the beginning. 

So let's give this another try, let's go to /admin/add-product and let's try
adding that book again, now we are redirected and now we can also see that we
are logging this here. 

So this filtering mechanism here in app.js allows us to put a common starting
segment for our path which all routes in a given file use to outsource that into
this app.js file so that we don't have to repeat it for all the routes here. 

Implicitly, this route is reached under admin add product and so is this route
here, this one with a post request and this one with a get request. 

Now this can be a bit challenging to wrap your head around but this is another
core thing you have to understand, how these requests are funneled through and
how they may reach this file if they start with /admin because we are filtering
here and how in that file, the /admin part is then not checked again but it only
checks the second part and therefore reaches this or these requests route here. 

---