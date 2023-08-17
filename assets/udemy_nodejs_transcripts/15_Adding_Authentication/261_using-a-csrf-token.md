## 261. Using a CSRF Token

<strong><em>no description</em></strong>

So csrf protection is an important thing and to support that or to add it to the
app, I'll quit my server and I'll install another package with npm install
--save, the name of the package is csurf, this is a package for node express
which allows us to generate a so-called csrf token. 

Basically a token, a string value we can embed into our forms, so into our pages
for every request that does something on the backend that changes the users
state, so anything like ordering something, anything that does something
sensitive which we want to protect against. 

We can include such a token in our views then and on the server, this package
will check if the incoming request does have that valid token. 

Now how does this protect us? 

Well the fake sites might send a request to your backend and they could
theoretically use your session therefore but the requests will be missing the
token and they can't guess the token because it's a random hashed value and only
one value is valid of course and the package here which runs on the server
determines whether a token is valid, so they can't guess it and they also can
steal it because a new token is generated for every page you render. 

So with that package installed, let's rerun npm start and let's use that csurf
package and how do we use it? 

To enable csrf protection, we go to our app.js file and in there first of all at
the top, let's import this package, I'll name the constant csrf and I'll require
the csurf package. 

Please note the package is named csurf, the tag pattern is csrf, that is why I
named the constant like this, you can name it however you want of course. 

Now we can create a new constant where we initialize this you could say, so down
there maybe where we initialized some other things too, I'll initialize my csrf
protection by executing csrf as a function. 

Now you can pass an object here where you can configure some things, for example
that you want to store the secret that is used for assigning your token, so for
hashing them, that you want to store them in a cookie instead of the session
which is the default but I want to use the session, the default and we also
don't need to set any of the other values, you can dive into the official docs
of that package to learn more but the default settings should work fine. 

So with that, we get this csrf protection middleware here and we now just have
to use that as a middleware. 

So here after we initialized the session, that's important because csrf, the
package will use that session now. 

After we initialized the session, I'll add csrf protection, so basically the
constant which holds my created middleware here. 

So now with that, csrf protection is generally enabled but we still need to add
something to our views to really use it. 

Right now if I save this and I go back to my app and I reload this page, this
works, if I go to orders this works, if I logout, this fails, I get an invalid
csrf token here and this is already showing us how we or what we have to do in
general. 

It failed here because that logout action here actually was a post request and
for any non-get requests because you change data via post requests typically,
for any such requests, this package will look for the existence of a csrf token
in your views, in the request basically in the request body. 

Now to make sure that such a token is there, we first of all need to ensure we
have it available in our views, to do that we have to pass data into our view. 

So let's say I'm on the starting page slash nothing, so in the controller
actions, that is my get index action, this one. 

Now here we would have to pass a new piece of information into the render
method, you could name it csrf token, that name is up to you and you get it from
request and then there, there will be a csrf token method. 

This method is provided by the csrf middleware which we added by this package. 

So now this will generate such a token and we'll store it in csrf token which we
then can use in our view and there we could use it for example in the navigation
where I have my logout button form. 

In there we would have to add input which is hidden so that no real input is
rendered but where the value now is a value we output with the help of ejs and
that value here will be our csrf token and the name here is just a field I'm
storing that token in when rendering that view, this field, csrf token. 

With that if I reload this page, let's inspect the logout button here in the
developer tools and let's make sure that in the navigation.ejs file, we don't
just add it to the mobile logout button but also in the other menu here. 

So with that changed, let me reload this and now when inspecting the logout
button, you will see that there we also have that input with the value of this
token and this here is the csrf token which was generated by the package. 

If I now click on logout, I still get an error here though, the reason for that
is that my package csrf does not know that this hidden input contains my token,
it's just a hidden input without any name. 

So what we have to do is we also have to give this a name and here important,
the name has to be _csrf because the package which we added will look for this
name, so for an input with that name and the same of course should be done here
in the mobile login button. 

Now with that if we reload this view, if I click logout, now it works because
now the package is able to extract that csrf token. 

It also finds out that the token is valid and therefore it allows us to proceed,
so now it's not just a session that matters but also the existence of this
token. 

Now we can add this to all our render functions because we need it in all our
routes but that would be a bit cumbersome, so let me show you an easier way of
getting data like this or also isAuthenticated into every page we render and not
just some. 

---