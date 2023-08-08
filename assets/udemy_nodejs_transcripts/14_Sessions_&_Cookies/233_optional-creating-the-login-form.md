## 233. Optional: Creating the Login Form

<strong><em>no description</em></strong>

So let's work on that login page and for that I'll first of all add a new routes
file which I'll name auth.js and in there, I want to manage my authentication
related routes. 

Now for that, I will first of all set this up in a similar way to my other route
files which means I will set up the express router, so let me simply create that
here, we don't need the admin control though, so we have that router and I'll
then export that router and for now I need one get route in here. 

A get route for /login then which will load the login page, so /login is what I
want to handle here and as always, we have our request response next function
here for handling that incoming request. 

Now in order to reach that route, we of course need to register it in the app.js
file and in app.js, first of all let's import that route, so I'll duplicate my
shop routes, name them auth routes, the name is up to you of course and it's in
the auth file in the routes folder, so that file we just added and with the auth
routes added there, I will simply add them below my shop routes. 

Just like the shop routes, I have no leading filter so every request will go in
there and anything which is not found in the shop routes will therefore go into
the auth routes and in the auth routes, I will handle /login, this route here. 

Now in here I simply want to render a page and I want to render a page in the
let's say auth folder and just as I do this in the shop controller here, I will
also create an auth controller for that. 

So let's maybe duplicate this get orders action from the shop controller, add it
here and let's name it get login and then I don't need to find any orders or
anything like that, that of course can be removed, I just want to render
something, I want to render auth login here, the path will be /login, your
orders well I will simply name this login and I don't pass any other data. 

So it's a really simple controller action in my auth.js file and with that in
the auth.js file in the routes folder, I can simply import that, so here I will
import my auth controller by requiring that from the controllers folder in the,
whoops, the auth file there and then here for login, I will not use that
function but point at my controller with the get login function. 

Ok so now we get the same setup we used for the other routes and now we have
that login controller action which will render the login page with the
appropriate title. 

Now let me head over to navigation.ejs real quick and make sure that this gets
highlighted when we are on the page and for that I will copy that class
assignments, that css class assignment, add it here and the path should be
/login or whatever you assigned in your controller action. 

With that out of the way, let's add that folder and file in the views folder, so
I'll add an auth folder here and in there a login.ejs file because that is just
what I try to render my controller right, there I try to render auth login. 

so we need to have that path and file in our views folder. 

And for that I will really just use my product excuse me, my admin, my edit
product page because there I have a form and I will move that into the login.ejs
file, I will include head.ejs, I don't need the product.css but I need the
forms.css . 

I will include the navigation, then this here will receive a new class, we can
name this login form and see how we have to adjust the styling for that then. 

The action here, well that action will always be the same, we don't have
different modes here, the action is always login and we send a post request to
that login route. 

And then here let's say we have an email address, we name that field email here
and we give it an ID of email, it's also of type email and not of type text and
let's not start with a default value, so we don't need that here and we also
need a password let's say, so let's add password here, name this password and
give it an ID of password and the type here will also be password so that the
characters are hidden and with that, we get also rid of this value here. 

Now we don't need the other form controls so we can get rid of these form
controls, slso of the hidden one for now and let's simply add a button at the
bottom which is of type submit and which simply says login, so a really simple
form. 

With all of that in place, if we now click onto that login button, we are indeed
loading that login page. 

Now the styling is a bit off because we need to style that login form and for
that, I'll real quick add a new css file which I'll name auth.css and in there
on the login form, let's have a look at the product form, I think we can just
reuse that style here and yes we could have therefore also like refactored it
into a global style but I'll just do it like this. 

And in login.ejs, we now just make do, need to make sure that we do also import
that new auth.css file I just added. 

So if you now reload this, this looks pretty good. 

So now we got this in place and as I mentioned, I will not implement a full
login flow right now, we'll do that in the next module where we dive into
authentication and everything that belongs to it. 

But here I want to show you how we can use a cookie to save the information that
this user is logged in and for that, we'll continue in the next lecture and see
how we can use cookies. 

---