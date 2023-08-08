## 297. Adding Async Validation

<strong><em>no description</em></strong>

Our sign up validation is looking pretty good but there is one thing which we
are validating in a bit of a strange way right now and that is the fact whether
the e-mail address is taken or not. 

Right now I'm doing that in my auth controller and there by the way we will not
need confirm password anymore, we're checking this ahead of time but in auth.js
I do check for e-mail existence here. 

Now logically it would make sense to check that as part of our validation right
and the good thing is we can do that. 

Let's grab this code where we find one user here, let's grab that code and let's
head over to the auth.js file in the routes folder. 

In there let's first of all import our user model by requiring it from the
models folder and there from the user file so we need that and then here on my
e-mail field, I got this custom validator. 

I'll comment this code out because I want to keep it for you as a reference but
now we'll add a more well a check that makes more sense. 

I will add my code here where I find one user with that e-mail address, now that
e-mail address on the right side here is the value of course which you are
validating because we're doing this on the e-mail field, so value will be the
entered email, I'm searching for that e-mail and then here if I have a user
document, well then I will not do it with this flash message and so on anymore
instead I'll just take that error message and inside of this if block which is
inside of my then block here, I will return a new promise reject call. 

A promise is a built-in javascript object and with reject, I basically throw an
error inside of the promise and I reject with this error message I used before. 

What this means is that now after this then block, I could another catch block
to catch this but I will not do that here instead let's close our function curly
braces and the normal brackets from the custom function and now what I'll do is
I will return user find one. 

Now what will this do? 

The express validator package will check for a custom validator to return true
or false, to return a thrown error or to return a promise. 

If it's a promise as it is the case with this because here we ultimately return
a promise because every then block implicitly returns a new promise, so if we
return a promise then express validator will wait for this promise to be
fulfilled and if it fulfills with in our case nothing, so basically no error,
then it treats this validation as successful. 

If it resolves with some rejection in the end though which will happen if we
make it into this if block, then express validator will detect this rejection
and will store this as an error, this message will then be stored as an error
message. 

And this is how we can add our own asynchronous validation, asynchronous because
we have to reach out to the database which of course is not an instant task but
express validator will kind of wait for us here. 

So now we have our own async validation in place and now we should still check
for email existence but we don't do this in controller anymore because there, I
will in the end get rid of that entire user find one thing here, instead I will
instantly start with b crypt and I'll also remove one pair of brackets at the
bottom and this semi-colon and this catch block. 

And now what I do have here is I instantly start with hash in my password and so
on creating that user because I can rely on the user to not exist already inside
of my controller because I do check for its existence ahead of time in my
auth.js route with the help of that validation middleware. 

So now let's go back and let's add an email address and a valid password of a
user that already exists and indeed I get e-mail exists already, so that is
great. 

If I however do add an email address that does not exist yet and I do enter
valid passwords, I get my sign up page here or my login page because the user
was created successfully. 

So this now works and this is how you can add async validation. 

---