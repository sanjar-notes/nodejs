## 234. Adding the Request Driven Login Solution

<strong><em>no description</em></strong>

So in the last lecture we edit this login form which you can reach by clicking
on login here on the top right corner and you can simply download the attached
code to have that same starting project, if you download it just make sure that
you use your database credentials here when connecting to the database because
mine won't work for you obviously because I shut down the server after I'm done
recording. 

So I added this login page and we'll not implement authentication right now,
we'll do this in a separate module but this is a great dummy scenario for using
a cookie because let's say when we click that submit button here, the login
button, we will actually send a login request to the backend because that is
what we stored in the login form, here in auth login, we are sending a post
request to /login and since we do that, we should handle this and we want to in
a real scenario validate the e-mail and password, in this module we'll not do
that, we'll just assume that the input data is valid because it's not the topic
we'll focus on for now. 

So let's add a new controller action first of all in the auth.js file and I'll
name it post login. 

Now in post login, I will get my login data, e-mail, password and so on and I
don't really care about that data, so I'll just assume the user is logged in and
I will then redirect to just slash. 

However and now that is important, if we do it like this and we add a route for
this of course to our auth route file, so here this is post, a post request to
/login and we use the post login controller action, if I do this and then click
on login here, I am indeed forwarded to the /route. 

Ok so this could mean we are authenticated. 

Now let's say we want to store that information that the user is authenticated,
how could we store that? 

Well you could say I go into my controller and in post login where I do log the
user in, I store that information in my request object, is logged in because we
are already doing a similar thing in app.js right at the start, we fetch our one
dummy user and store that in the request so that we can use it for the rest of
that request, so in all the routes and controllers where we handle that request.


We can do the same here and set this to true, by default right at the start it
will not be set, so the value will be undefined which is treated as false and
that is the information I need. 

Now to validate whether that works, let's actually go to our views and there in
the navigation.ejs, I commented out two routes for which we could say we need
the user to be authenticated, let's comment them in but only render them if the
user is authenticated. 

So how would we go about that? 

Well we could use ejs for that of course and we can check if, let's say we
expect to get some isAuthenticated value here, so if isAuthenticated then we'll
do something, we'll render this part here and otherwise this will not be
rendered because we don't make it into that if block. 

So if I do it like this and I reload this page, I get an error that
isAuthenticated is not defined because we're not always rendering this to our
different views. 

So what we actually need to do since the authentication is part of every page,
for every render call here, we need to pass the information whether the user is
authenticated or not and for that I'll access request is authenticated because
that is exactly or is logged in, excuse me is logged in because that is the
field we're storing that information. 

So I'll access request is logged in because that is what I will set to true when
we do login, so I'll add isAuthenticated and store that value to every render
call here. 

Here and here for get add product, also on the error page here like this and
also in shop.ejs of course for all our routes here like this one, basically
every time when we call render, in all these cases I will add my isAuthenticated
information. 

So now that I added it to all routes and I saved all files, if I reload I still
fail because I obviously also need to render, I need to add it to auth.js, to my
render route there, so now if I reload, this works and we are missing these two
fields. 

If I login, we are still missing them though and why is that, do you know why
this does not work? 

Even though I am storing the information that I am logged in, in is logged in
when we click that button, I'm storing it in my request and then I use that
information in the request on every other route I handle and I pass it into
isAuthenticated which is the field which I'm using in my frontend, in my
navigation, there I am checking for isAuthenticated and that is what I am
passing to that frontend in my render calls here. 

Well the problem of course is yes I update is logged in here in the request and
what happens to the request once I send a response and we do send a response by
redirecting? 

Well the request is dead, it's done. 

With a response, we basically finished a request, we got a request and we sent a
response, we're done. 

This data does not stick around, this data is lost after the request or after we
send the response. 

So whenever we visit a different page, like here where we do get redirected, so
we get redirected here and we reach our get index action here in the end and
there, we do render the shop index page but this is a brand new request, the
redirection creates a brand new request and this is super important to
understand. 

We're working with totally separate requests and that is important because your
application, your page will have hundreds of users and obviously the requests of
all these users are not related to each other otherwise they could maybe look
into data that they shouldn't see and even the requests of a single user, so
requests made from the same IP address are treated as totally independent
requests. 

They are not seen in a bigger context or anything like that and this is a good
thing, this is deliberately designed that way and therefore any data we store
here can be used as long as we are working on the same request. 

That is why when we retrieve the user in app.js here and I store it in the
request, that is why we still can use that request user in all our action
controllers because they can again at a later point of time, this middleware
runs on every incoming request before our routes handle it. 

So the data we store here is used in the same request cycle, in our route
handlers in our controllers but if I do change the request at the end of its
lifetime, like here, right before I send the response, this data will not be
useful to us, it's really important to understand this. 

So let's now see how we could solve this in a better way. 

---