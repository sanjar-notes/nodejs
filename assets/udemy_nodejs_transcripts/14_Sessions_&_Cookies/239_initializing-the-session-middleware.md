## 239. Initializing the Session Middleware

<strong><em>no description</em></strong>

To implement a session, we'll need another third party package, we'll need
another package which helps us with managing sessions. 

For that we'll install it with npm install --save and the package is named
express-session, it's a package which is actually part of the official expressjs
suite but not baked into expressjs itself but now we already got it installed
and now we're ready to use it. 

To use it, we'll go to our app.js file because we want to initialize that
session early on, we want to initialize that session when we, well when we start
up our server then we want to initialize the session middleware at least and the
session will then be used for every incoming request. 

So in here we create a new constant, so we basically import something here which
I'll name session, the name is up to you and I will require express session,
that is what I'll require here, so that is the package we just installed. 

Now with that installed, we can set it up here along with the other middleware
let's say. 

There we register another middleware with app use and to app use, we pass
session and we execute this as a function and to the function, we pass a
javascript object where we configure the session setup. 

For example we need to set a secret, this will be used for signing the hash
which secretly stores our ID in the cookie. 

So here I'll set a secret, you can enter any text here, it should typically be a
long string, I'll name it my secret but again in production, this should be a
long string value. 

Then you should add the re-save option and set this to false, this means that
the session will not be saved on every request that is done, so on every
response that is sent but only if something changed in the session., this will
obviously improve performance and so on. 

Also there is the save uninitialized value which you should set to false because
this will also basically ensure that no session gets saved for a request where
it doesn't need to be saved because nothing was changed about it and that is it.


These are the core things you need to set. 

You could for example also configure the session cookie, you could give it a max
age by setting a date or add the expires key, so you can configure that cookie
but you can also go with the default settings. 

And with that, the session middleware is initialized and we're now ready to use
the session. 

Now let's start using it in the next lecture. 

---