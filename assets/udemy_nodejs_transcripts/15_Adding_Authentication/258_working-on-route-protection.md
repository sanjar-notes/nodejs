## 258. Working on Route Protection

<strong><em>no description</em></strong>

Now that we are able to sign up and sign in, we have to work on route
protection. 

We already have a setup where we only show the menu options we should be able to
interact with but even when I logout and therefore my session is gone, even when
I do that, I can still manually enter admin add product and reach that page and
I could even try to create a product here, I would fail then because there would
be no user object on the backend where I tried to get the logged in user but
this is not the user experience we want to offer, we don't even want to be able
to load this page if we're not logged in and for that, we need to protect our
routes. 

Now how do we protect routes? 

Well to protect routes, we want to check where the user is authenticated before
we render back let's say the add product page. 

So in admin in the admin controller, in get add product which loads that page,
before we render that page, I want to check if in the request session is logged
in is set and to be precise, I want to check if it's not set because if this is
not true, the user is not logged in and if the user is not logged in, then I
want to redirect let's say to the login page like this. 

So then since I return here, this code will not execute and I won't load the
added product page. 

So now let me try to reload this page, keep in mind I'm not logged in and I'm on
the login page. 

So this works, I am redirected here because session logged in is not set. 

On the other hand if I do login now, so if I do enter my valid credentials here
and I try to access add product, this does work because now I make it past this
if check. 

Now this is a code we could add to every route which we want to protect but
adding it like this is a bit cumbersome, so let me show you a better way of
protecting our routes or a more scalable way in the next lecture. 

---