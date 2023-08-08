## 294. Built-In & Custom Validators

<strong><em>no description</em></strong>

We added the isEmail validator. 

Now there are way more built-in validators available from which you can choose
and you'll find them when you visit the express validator page because there if
you check the official docs to which this link points, you'll see that in the
end it's a wrapper around the validator js validator, so that's another package
that was implicitly installed with express validator. 

And here on the docs of validator js which is a different package which was
installed, you'll find all the built-in validators and what they do and how you
might configure them if possible and you see this is the one we're using,
isEmail, this is what I'm using here, we could configure it to change different
e-mail formats we want accept or not accept, we can check for emptiness, we can
check whether something is a full domain or a full url, we got all kinds of
things. 

We can check if a value is in a certain array of possible allowed values, if we
have a certain length will be important for the password and so much more. 

So you see there are a bunch of things we can check and definitely go through
this list to learn more about the built-in validators. 

You can also add your own validator though and to demonstrate this real quick,
let's say we're not just using isEmail, I also want to make sure it's a specific
e-mail I want to have. 

For that I can add custom here and now a validator is in the end a function like
this, a function that receives the value of the field we're checking, so the
value in the email field and optionally, an object from which we can extract
things like the location to which this was sent, the path or the request object
in case we need to extract more from the request. 

Now in this function, you want to throw an error when validation fails, so here
we could simply check if value equals and now let's say it should be
test@test.com because we don't want to allow that, that's just some dummy logic
here. 

So if that is the case, then I'll throw an error by calling throw new error with
a message of this email address is forbidden, something like that. 

Of course this is very arbitrary that I'm checking for exactly that e-mail
address but this is how you can generally write your own validators, in case the
many built-in ones don't suffice your requirements. 

So now if I save this, we should see that if I reload that page and I enter
test@test.com, I get this email address is forbidden, if I enter test2@test.com
then I get invalid value though. 

The reason for this invalid value here simply is that if we do succeed, we
should return true, so we throw an error if we fail, we could return false to go
with the default error message or we throw an error to have our own error
message or we return true if it succeeded and now you will see that if I enter
test2, this worked. 

Now this will actually be stored a bit strange in the database now because I
entered a new user with invalid password, with an empty password but we didn't
add any password validation yet. 

The key takeaway is that you saw how you can add your own validator, returning
true if it's fine, returning false or throw an error if it's not and how you can
use the many built-in ones and of course that you can chain them after each
other to add multiple validators to one and the same field. 

---