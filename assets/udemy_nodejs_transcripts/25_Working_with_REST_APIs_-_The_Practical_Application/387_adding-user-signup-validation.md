## 387. Adding User Signup Validation

<strong><em>no description</em></strong>

I will create a new controller, auth.js that is related to my users, to my user
data, to my authentication logic and in there I'll first of all import my user
model by requiring it from my models folder, the user file. 

Now we need at least two actions here and the first one is of course the action
to sign a new user up. 

So I'll name this action sign up and I'll get my request, my response and that
next function and in here I want to add all the logic I need to create a new
user in the database. 

So for that let's extract the email from request body email, let's extract the
name of the user from request body name and let's extract the password from
request body password. 

Now obviously to extract all of that, we need to know that it's there, so we
should add validation. 

For this I'll go to my auth routes again and just as in feed.js, I will add this
express validator check, so I will copy that import from feed.js and add it to
auth.js and on sign up, I'll then add an array of validation related middleware.


I'll check my request body and there, the email field whether it is an email,
you can also just to bring this back into memory define our own messages if we
want to, please enter a valid email, this will then be stored in the error
object we can retrieve. 

We can also add our own custom validator here to check whether the email address
already exists, for this I'll import my user model, so require that from the
models folder and then custom and you learned that in the validation module by
the way in case you want to dive deeply into that again. 

The custom function or the custom validator method here takes a function as an
argument which retrieves the value we're looking at and then an object from
which we can extract the request as a property with this destructuring syntax
and this function then should return true if validation succeeds or return a
promise if the validation actually uses some async task, so if the validation
does something which takes a little longer as in our case. 

So I will return user find one and I want to find one user where the email of
that user as stored in the database matches the value of the e-mail we're
looking at. 

Now then I have my user document here, so my user object as I've found it in the
database and if that is set and that's the only case I'm caring about, if that
is set then I will reject a promise, so I will return promise reject and that
will cause the validation to fail, all other scenarios will cause it to succeed
and then I'll return email address already exists. 

So that's just another validation we can add. 

Of course I don't just want to validate the email though, so let's also validate
another field in the request body, before I do that though, just one step I
forgot, I will normalize the email as well but now I can look at other body
fields like the password. 

The password can be trimmed and should then have let's say a length of at least
5 characters or whatever you want and I'll add another check where I'll look
into my body, there to the name, trim it to remove excess whitespace and this
should now not be empty. 

With that, I got all my validation logic added, now that I'm in here I can also
already import my controller, so my auth controller can be imported from
controllers auth and now I'll use that auth controller as the last middleware on
my sign up route and reach out to the sign up action in there. 

Now validation was added, now back in the auth controller, we want to collect
any validation errors right at the start and for that I need to import something
from the express validator package again and that will be that validation result
function which I require from express validator/check,  so this validation
result function here and I collect errors by calling that and passing the
request to it and now if not errors is empty, so if we got errors, then I know
that something went wrong or that I have errors and in this case I want to
create a new error where I say validation failed, something like that and I'll
set a status code of 422 and I can also maybe pass some data, a new property
I'll add where I store my errors array like this and then I can throw my error
here. 

Didn't do that before but this would allow me to keep my errors which were
retrieved by that validation package, I now just have to go to app.js, to my
error handling function and there retrieve the data from error, the data
property and also add this to the response I'm sending in case of an error. 

This is totally optional but just to show how you could keep your original
errors and pass them to the frontend as well. 

So now I'm doing this, I'm doing that validation and throwing an error if it
fails, if we make it past this if check, we know we have all that data we need
and now we can start storing the user in the database. 

Now there are parts of the authentication module which still matter here and one
of them is that we should encrypt the password. 

So let's finish sign up in a secure way in the next lecture. 

---