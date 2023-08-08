## 295. More Validators

<strong><em>no description</em></strong>

Now that we learned how to add validators, it's time to add more validators for
our sign up, for example I want to make sure that the password is also at least
six characters long. 

Now for that we add another middleware, another check function call and what you
can also do is you can wrap these into an array. 

That is optional, that is not required but of course it keeps your checks kind
of grouped together and maybe makes it clearer to read that this block is all
about validation. 

Now instead of check, you can also use a different function besides check which
as I mentioned checks the body, the parameters, the query parameters and so on,
you can also add just body, just param, just query, just cookie or just header
to check just a certain set of features of the incoming request, so I could use
body instead of check to make sure well you can look for a specific field but it
has to be included in the request body. 

So for this email, we would extract that e-mail from the cookies, the headers,
anywhere, doesn't matter because we'll be in the body but it would look for it
anywhere. 

Now for the password I want to show you an alternative and typically you would
use the same approach for both of course and I could say well please check the
password value in the body of the request, so if there happens to be a password
value in the headers, I don't care about that. 

So now I'm checking for password in the body and now again you can add your
validators. 

You could say isLength, that is a built-in validator which you have to configure
with some options in the form of a javascript object where you can set a min key
to let's say 5 and you could also set a max length if you wanted to. 

So now we have the min length and we can also enter a different validator like
isAlphanumeric to only allow numbers and normal characters, so we could add that
too and if you don't add with message here by the way, then this means it will
use the default invalid value message. 

Now maybe you want to use a default message for all validators but you don't
want to repeat with message after every validator where you then enter like
please enter a password with only numbers and text and at least 5 characters. 

This could be the error message but of course if we now repeat with message
after every validator, this is a bit stupid right, it's a bit redundant, so for
such a case where you have wanted the same error message for all your validators
but it should not be the default invalid value error message, you can just grab
that error message, remove with message here and simply add it as a second
argument to the body or to the check function and now this will be used as a
default error message for all your validators. 

So now this would be a check we could add, checking for the password being at
least 5 characters long and only alphanumeric, in production you want to use
more secure requirements, a longer password and you of course want to allow
special characters but here just for demonstration purposes, this is fine. 

And now if I save that I can enter a valid email address but this password is
too short, it's only one character, right. 

So if I hit sign up, I get well good job I mean that's the forbidden email but
if I now enter this, I get please enter a password with only numbers and text
and at least 5 characters. 

If I do enter some new account email and then here a password that is long
enough and that is only text and characters, well I happen to use the email
already but other than that it succeeded. 

If I enter something totally else, this simply worked and if I enter a valid
email address, so this one doesn't exist yet but I enter a password that is long
enough but has a special character, I fail because I only allow alphanumeric
characters. 

So this is another example for adding validation and how to add multiple checks
for one and the same request, now in the next lecture, let's see how we can
compare our passwords for equality. 

---