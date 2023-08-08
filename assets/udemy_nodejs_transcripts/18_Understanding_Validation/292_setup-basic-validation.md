## 292. Setup & Basic Validation

<strong><em>no description</em></strong>

So I'm back in our project and there for example we got the first cases where we
could add validation, the login and the sign up pages. 

There we want to validate, for example on the sign up page that the email
address is a valid email address with an @ sign and a domain ending, that the
password for example is at least six characters long, whatever your requirement
is and that the confirm password matches the other password, that would be
helpful too and later when we create a product where we for example enter a url,
we might want to validate that this is a valid url. 

So these are all things that we can add with the help of proper validation and
that is exactly what we'll dive into now. 

Now to add validation, we'll use a third party package, the package we'll be
using is called express validator and you can simply google for express
validator to find these official docs which are always worth checking out, in
there you find quick command on how to install it and then you find a link to
the full official docs which is this separate webpage where you learn all about
using it and this is really a good idea to dive in because I will introduce you
to this package, if you want to learn all the ins and outs about it, definitely
check out this documentation. 

So let's first of all install it with this command here, so just using npm as we
did it for other packages too. 

So back in our project code which is the code I've finished with in the last
course module, we can simply enter this here to install express validator into
this project and once this is done, we are ready to use it. 

So let me restart my development server with npm start and now let's find out
how we can use express validator and let's start with our authentication routes
for that. 

So here we obviously have our auth controller with the different controller
actions and we got our routes folder with the auth.js file. 

Now typically you want to validate on your post or your non-get routes because
you want to validate whenever the user sends data and that is not the case for
our get routes for example but for posting the login data or posting the sign up
data, I want to validate that data and I will start with the sign up, with post
sign up, with this route. 

Let's say we want to add some validation to that route and we want to ensure
that our e-mail here is an email, the password is at least let's say five
characters long and that the confirm password matches our password, these would
be some nice checks which I want to add here. 

Now to add that with that package installed, in my auth.js file in the routes
folder, I can import something from that package, let's name that exp validator
or however you want to name it and require express validator here. 

However the import here looks a bit different, we import a sub-package because
express validator is basically made up of a couple of sub-packages you could say
and there we need the check package which is the package you use for well all
the validation logic you could want to add. 

We can also use a next gen javascript syntax because exp validator which we
import will be a javascript object and we can use a feature called destructuring
where we use curly braces on the left side of the equal sign and then you add
some property names which you want to pull out of the object that this would
give you. 

So here and you can find it in the official docs, we'll get a check function
actually, so in the object which we import and which we would have stored in exp
validator otherwise, there will be a check property that holds a function and we
can import validation result, though we don't need it here we'll need it later. 

There also are other functions you can import and again the official docs are a
great way to dive in deeper. 

What this does is in the end it just gives us a check function which we import
from this package here and now adding validation to a route is really simple. 

For this post route, if we want to add validation, we add an extra middleware,
remember you have that path and then you can add as many middlewares request
handlers as you want and I'll add a new one here and I'll add a new one by
adding my check function and calling it here and check this function will in the
end return a middleware. 

So here I then just enter the field name or an array of fields which I want to
check, now how does this work? 

Well I can simply add check and then the field name. 

Now we can have a look at our sign up view to find out that for example there,
we'll have an email field, so it's this name I'm looking for. 

We have an e-mail field in there, so email will be the name of that field in the
requests we're receiving, so in our auth route here, I can check email. 

Now this tell this middleware, the express validator that I'm interested in
confirming that e-mail value or that I'm interested in validating that value, we
then call a method and this will in the end then return a middleware that is
understood by expressjs . 

So we call a method on this object which is returned by this check function that
now allows us to do all kinds of checks, for example isEmail. 

Now there are a bunch of built-in methods and I will show you where to find them
in a second and what this will now do is it will use this package to check the
email field on the incoming request and it looks for that field in the body, in
the query parameters, in the headers and in the cookies and it finds that field
and then checks if that is a valid email address and that is the first step. 

Now with that, we have this middleware in place, now we can go to our controller
here under controllers of course and import another part of that package. 

So here I will also import with this destructuring syntax because this package
just exposes a bunch of stuff and I only want to get some specific things and I
import from express validator check here as well and there we now need to import
the validation result, validation result will be a function that allows us to
gather all the errors prior validation middleware like this one might have
thrown or might have stored. 

So now we just have to go to the post sign up route because that is where I did
add my middleware and in here, I can now simply extract my errors and store them
in a constant, errors by calling validation result on the request and in that
request, this express validator middleware which we added here will have added
errors that can now be retrieved. 

With this middleware here in the auth.js file on the routes folder, we are
collecting errors so to say or this middleware will store some errors it found
in an errors object so to say and this validation result function will go
through that errors object managed by that middleware on the request and will
then collect them all in this errors constant and we can then use that constant
to check if we do have errors. 

Now how does that work? 

Well we can simply check if errors and then there is a method we can call, there
is the isEmpty method and isEmpty will return true or false depending on whether
we got errors or not and if this is not empty, that's why I add an exclamation
mark to check the inverse, if this is not empty, then we could return a response
where we set the status code to 422 which is a common status code for indicating
that validation failed, so it's an error status code, it will still send a
response just with this different status code and then we can call render here
and render the page again. 

And I don't redirect here because I want to redirect upon success, if we fail I
will render the same page again, so here I will render the same as I do in get
sign up, here we can copy that render message, that render call here I should
say. 

We do that same rendering here without res, just render, I render that same
page, auth sign up and I can also add my my errors there, the error message is
then not message like this but I can output errors and then there is an array
function which I can call to return an array of errors I might have and we can
also output this here, with console log to get a feeling for what's in there,
errors array like this, let's see what we got in there. 

Now if we save all that, with that in place with the middleware and the error
collection mechanism, let me enter something here, test which is not a valid
email and let me hit sign up. 

Now I get a message here which is the default browser validation because I set
this to type e-mail in my sign up view here, I have type e-mail and this adds
this default browser validation. 

Now one thing you can do is you can add no validate to the overall form,
validate to disable this check. 

Now by default you want to add it because it is a nice client side validation
that can improve the user experience but here to see how it works without it and
to allow me to make deliberate mistakes, I will disable it for now with no
validate added to the form, not the input but to the form and then if I reload
that page and I do enter something invalid again, I can submit. 

Now don't be confused by the error message, this is to be expected because we
don't get a message, we get an array of errors but if we check our server side
console, we see that this console log where I log an array of the errors that
was collected gives me that array and we get the square brackets, it's an array.


An array of objects and in that object, we find out which parameter was the
problematic one, what value was entered and which message was generated by the
validation middleware and this is a message we can use to output an error
message if we want to. 

---