## 279. Implementing the Token Logic

<strong><em>no description</em></strong>

So we want to be able to enter an email address here and then receive an email
with a link that allows us to reset the password. 

Now for that, we need to first of all create a unique token that also has some
expiry date which we will store in our database so that the link which we didn't
click includes that token and we can verify that the user did get that link from
us because if we just, well let the user now change that password, we got no
security mechanism in place, so we need that token to put it into the email
we're about to send to only let users change the password through the email that
contains that token, that's an additional security mechanism. 

So let's work on that token creation then and for that first of all, I'll export
a new action in my auth controller and that will be post reset, so that will
basically the action that should get triggered once we clicked that reset
password button here and in there, I need to generate that token. 

Now nodejs has a built-in crypto library which I can use for that, so I'll name
that crypto and require crypto like that. 

This is a library that helps us with creating secure unique random values and
other things but we'll need that unique secure random value here. 

So here in post, we settled and use that crypto library which I stored in a
constant here and I will call random bytes to generate some random bytes, I want
32 random bytes and this will call a callback function here, so this is the
second argument, a function will be called once it's done and there I either get
an error or a buffer, a buffer of these bytes. 

Now I have an error here then I want to return redirect back to let's say reset
and we could flash an error message here if we wanted to, I'll also log the
error so that we can debug it but if we make it past this check, we do have a
valid buffer and then we can generate a token from that buffer, simply by using
buffer toString and there we just need to pass hex because that buffer will
store hexadecimal values and this is information toString needs to convert
hexadecimal values to normal ASCII characters. 

So then we'll have a token. 

Now that token should get stored in the database and it should get stored on the
user object because it belongs to that user, so let's first of all go to our
user model and there, I'll add two new fields, I'll add a reset token and I'll
just assign a type of string here. 

Now important, this is not required because not always this token will be there,
only if we requested a reset and we'll have a reset token expiration or however
you want to name it and that will be of type date and now I want to store that
token on the user which we plan to reset. 

So first of all I need to find that user in the database and I'll use the
mongoose user model for that, to find one user where the email matches the email
we're trying to reset and that email which we're trying to reset can be
extracted from the request body email field because on our reset view here, we
do have that email field. 

By the way important, the action here should be /reset to reach the right route
but with that, this is prepared and now in our controller, I'm finding a user
who has this email. 

Now let's add then and catch, handle any potential error we might get by logging
it for now and then in then, we should get a user or undefined if that user does
not exist. 

So in here I want to check if we don't have a user. 

If we don't have a user, then I will flash a message as you learned it in the
authentication module onto the error key, no account with that e-mail found or
whatever message you want to show and then here I'll return a redirect to
/reset. 

If we make it past this if check, then we are looking for an e-mail address that
is stored in the database and now for that user which I retrieved for that
e-mail address, I want to set the reset token equal to the token which I
generated and I will set the reset token expiration equal to date now which
gives me the current date and the time plus one hour and this now has to be
expressed in milliseconds, so you should use 3,600,000milliseconds, this will be
one hour. 

So now I'm assigning these two fields and we can call user save to then update
our user in the database. 

Let's return this so that we can now chain another then call here, another then
block which will execute this function when user save succeeds. 

So at this point of time, we know that the updated user was stored in the
database and now we want to send that token reset email. 

Now I showed you how to send e-mails in the last lecture, in the last module I
mean, so make sure you through that because I will now use that transporter
again which I created there, the node mailer transporter which we use for
sending email and I will send an e-mail to the e-mail of the user which we
found, so to user e-mail, excuse me, to request body e-mail we can say, so to
the e-mail we're requesting the reset for, the subject could be password reset
and now in the html code, I'll use a next gen feature, back ticks which allows
me to write multiline strings which makes it a bit easier to read. 

I'll add a paragraph where I say you requested a password reset, so users should
be worried if they get that if they did not click this link to set a new
password and you could include more information like the fact that this is only
valid for one hour. 

Now this link here, this will be anchor tag leading at some url and that url
will be in our case your localhost 3000 and then let's say reset and then the
token which we have. 

Now since I'm using this back tick syntax, I can dynamically embed values with a
special syntax where I use ${} and now I can inject variables and their values
into this string and the values of the variables will be placed in that string. 

So here, I can now output that token which we generated here, so now I am
placing that in the url because that token is then what we'll later look for in
the database to confirm that this link was sent by us because only we know the
token. 

So this will send an email and at the same time, I will redirect back to the
starting page let's say because the next instructions are received in the email
of course. 

Now let's try this out in the next lecture. 

---