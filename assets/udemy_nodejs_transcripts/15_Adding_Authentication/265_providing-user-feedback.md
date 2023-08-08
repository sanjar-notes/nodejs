## 265. Providing User Feedback

<strong><em>no description</em></strong>

We've got all the core features that are related to authentication implemented,
now I want to work on the user experience a little bit at least. 

Right now when we login and we for example try to login with invalid credentials
where we don't find the email or the password does not match or we try to create
a user for whom the email already exists, then we are just redirected without
any error message being shown on the page. 

Now I will dive deeper into how to validate user input in the validation module
of the course but here we're not talking about validation so much but really
about giving some feedback to the user in general. 

Now when rendering views with the render method as we are doing it here,
including data that should be rendered on the page was simple, by the way
isAuthenticated can be deleted here because we always include this as a local
and that is the case for all our routes as a side note, so you can remove that
isAuthenticated thing from all render methods but this is not really what I
wanted to do here, it's a little side thing we can do though. 

The main thing is that it's easy to pass data to our views inside of the render
method as you can see, it was never a problem to get our data into the views
there. 

However it is a huge problem if we want to pass some data into the rendered view
when we are redirecting as we are doing it here because upon a redirect,
technically a new request is started, a new request to /login in this case and
on that new request, we don't know that we got here because the user entered an
invalid e-mail or anything like that, when we triggered this new request this is
treated in the same way as a request that was triggered by clicking on the login
button in our menu. 

So we have no way of finding out if we want to display an error message or not
and hence in the render method of get login where we show that login page, we
don't know if we want to include some error message. 

Now to solve that problem and store some data before we redirect which we then
use in the brand new request that is triggered by the redirect, how could we do
that? 

Well you learned if you want to store data across requests, you need a session. 

So we can use a session for that but of course I don't want to store the error
message in the session permanently, I want to add something to the error
message, kind of flash it onto the session and once the error message was then
used, so once we pulled it out of the session and did something with it, I want
to remove it from the session so that for subsequent requests, this error
message is not part of the session anymore and for this, we can use another
package which makes this really easy. 

We install that with npm install --save and then the package is called connect
-flash, if you hit enter, this gets downloaded and added to your project, you
can restart the server thereafter and now connect flash is really simple to use.


First of all we initialize in our app.js folder, file, in there we install it or
we import it just as we import other packages, you can store it in a constant
which you name however you want, I'll name it flash and I will require connect
flash here. 

Now flash then needs to be registered you could say, initialized, I'll do this
here at the bottom, you need to do it after you initialized the session, so
certainly after this middleware, there I will call use and I will simply call
flash as a function here. 

Now we can use that flash middleware anywhere in our application on the request
object. 

So now let's save that and let's head over to auth.js and let's say here when
we're logging in and we don't find a user with that e-mail which is the problem
here, we want to flash an error message into our session and we do this now with
request and there will be a flash method now added by this package. 

This flash message now simply takes a key under which this message will be
stored, we could name this error and then the message and in this case this
would be invalid e-mail or password. 

Now you could also say just invalid e-mail, some people advocate not being as
clear as people can otherwise guess which part of the credentials was wrong, I'd
argue they can test this anyways by trying to sign up with that e-mail but
whatever you want, you can output or flash such an error message. 

Now with that it's in session and it's in there until we use it. 

Now we want to use it here when we do render the login page, here I want to
include an error message variable let's say and that error message variable will
simply pull that by using request flash again and here we now just access the
key for which we want to get the message. 

So in my case that key is what I specified here, error, so now I can pull that
message out with error. 

So whatever I stored in error will now be retrieved and stored in error message
and thereafter, this information is removed from the session. 

So now error message will be set and will hold a value only if we have an error
flashed into our session and therefore we can now move over to our view, to the
login view and display the error message here. 

Let's say above all of that I add a div and for now let's make this really
simple and just output our error message, so here error message is the variable
in which I'm storing it. 

Obviously I want to check if that exists before I render this, so I will wrap
this with some ejs if statement where I check if error message, this will not be
treated as true if it's simply not defined so if we simply are not able to
retrieve anything and then let's try to output it like this, let's see if that
works. 

If I go back to my application and I reload that login page, that seems to work
and now let me enter an invalid email and indeed I see invalid e-mail or
password. 

If I do enter a valid email but an invalid password, I don't see that because
there I don't flash anything onto my session yet. 

So this is working, now let's quickly reformat that, I'll do that in next
lecture, you can skip it and download the finished formatted code if you want to
and thereafter, let's add this in other useful places too. 

---