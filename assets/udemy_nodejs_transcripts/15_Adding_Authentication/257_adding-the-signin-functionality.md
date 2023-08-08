## 257. Adding the Signin Functionality

<strong><em>no description</em></strong>

Now that we are able to sign up, let's also add some functionality to ensure
that we can sign in and for that, we obviously have our login page and when we
enter something here, we reach our post login route here. 

Now in there we still have the old dummy code where we just find our default
user which by the way won't exist anymore because we deleted it and then we
would create a session. 

This is obviously not the approach I want to use anymore, instead what I want to
do is I want to find a user in here but I want to find the user by the email the
user entered, so let's first of all extract that. 

Let's extract the email from the request body and let's extract the password
from the request body, these are two pieces of information I need for signing a
user in. 

And then here I'll not use find by ID but find one to find one user with a
specific e-mail and there should be only one user with an email in the database
and I'll find the user by looking for the email field in the documents and
comparing it to the e-mail value we are extracting here. 

Now if I find a user here so if I make it into here and I then have a user, then
I know that we can check the password next. 

If I don't have a user here, so if user is undefined, I didn't find a user in
the database and then I can simply return here, not execute the other code and
simply redirect back to login for now because the login failed because we tried
to use an e-mail which does not exist in the database as we didn't find a user
for it. 

If we make it past this if check, we know that the e-mail exists but now we need
to validate the password of course. 

We'll do this with the bcrypt package again because the password is of course
stored in a hashed form and I mentioned that we can't reverse this, so how can
we now compare the password? 

Well remember that bcrypt was responsible for creating the hash, bcrypt uses a
certain algorithm for that and we can essentially pass the password the user
entered into bcrypt and let bcrypt compare it to the hashed value and bcrypt can
then find out if the hashed value does make sense, taking into account the
algorithm that is used for creating that for the password you entered as plain
text. 

So if that plaintext password, if you would hash it could result in the hash
password and if the answer is true, then you know the user entered a valid
password. 

And for this, brypt has the compare function and there we enter the password we
want to check, so the password we extract from the incoming request and then the
hashed value against we want to compare it and that is found in our user
document which we get from the database and there of course in the password
field. 

Now this also returns a promise, so here we can add then and a catch block. 

Now if we have an error here, so if we fail to compare this, then I also want to
redirect back to the login page but if we make it into the then block, then I
want to check whether we were successful. 

Now important, with compare we'll only face an error if something goes wrong,
not if the passwords do not match. 

In both a matching and a non-matching case, we make it into the then block and
result will be a boolean that is true if the passwords are equal, so we could
also name this do match to make this clearer and it will be false if they are
not equal. 

So here we can check if do match is true, that means the passwords are equal,
the user entered a valid password and then we could return to not execute any
other code, we could return a redirect to the starting page. 

If we don't make it into there, then we want to redirect back to the login page
because then the user entered an invalid password. 

Now we also want to set a session as we did it before and that session code
should only be set if we have a matching password, so if the user did
authenticate. 

Then we can still set is logged in, we can still store the user in the session
because we still need the user object and the user here keep in mind is the user
we retrieved from the database and we want to save that session and only
redirect in that session after we saved it successfully. 

Therefore we should also return this to avoid code execution of this line
because the callback here will execute asynchronously, so this needs to be
returned to not execute this line here, in here we don't need to return then
because after this line, this line can't be reached because this line is in a
callback in a different function. 

So with all that in place, we should be able to sign in if we do enter a valid
password, let's give this a try. 

So keep in mind my email is test2 and I used tester as a password and first of
all I will try a wrong email, I'm redirected back to login so this didn't seem
to succeed. 

We can also quickly go to the sessions and clear all sessions here so that we
can really prove that no session was created. 

So now let me enter a valid email but an incorrect password and I'm again
redirected back and no session was created here but now let me enter the valid
email and the valid password and now I'm on the starting page. 

I see all options which is looking good, we get no error here and if I have a
look at my sessions collection, we've got a session here because now I am logged
in, this is the user object with which I'm logged in, so this is correct and now
we got a working login flow, taking into account our email and so on. 

---