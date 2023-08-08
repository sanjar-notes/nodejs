## 268. Adding Additional Flash Messages

<strong><em>no description</em></strong>

So were you successful? 

We added our flash message here when we used an email which we did not find, now
obviously if we have a password that does not match, here where we also redirect
to login, I also want to flash my invalid email or password message onto the
session. 

So this is another great place because if we now save this, on the login screen
I might have a valid email but an invalid password and I get this error message,
with valid credentials, it of course works fine though. 

Now we can also do something when signing up because when signing up, I'm
checking whether an email address already exists, well before redirecting here I
can also output something there, email exists already, please pick a different
one, something like that. 

If we now save that and I enter the e-mail address which indeed does already
exist, well then I'm redirected without having any effect and that makes sense
because we flashed a message but I'm not outputting it, so we need to go to the
login page and copy that code for outputting an error message and then go to
sign up and there above the form, let's also output the error message here but
of course for this to work, we also need to extract it when loading the sign up
page. 

So that code which I'm using in get login to render my error message, I need
that in get sign up too and then there I also need to pass this error message
variable to the view which holds that message I'm extracting otherwise we can't
display it even though we flash it into the session. 

So now with that, let's try this again, let's reuse a password, an email that
already exists and now I get this error, if I do create a valid user with a
valid email, this works however. 

So now if we quickly check our users collection, we see that was added. 

So these are some messages I can flash onto the screen, you could add more, for
example after logging out you could also output some confirmation for that but
this should do it for now. 

It was a nice practice and improves the user experience a little bit. 

---