## 254. Implementing an Authentication Flow

<strong><em>no description</em></strong>

So here I got a very simple sign up form which is a pretty typical sign up form
that though, you have to enter an email, you have to enter a password, confirm
the password and click sign up. 

Now in that sign up view, I changed my button label and there I also want to
point at the sign up route in the action now, /signup, send a post request to
reach that sign up, the post sign up route here which ultimately triggers the
post sign up action. 

Now in this action, we want to store a new user in the database, now which steps
does this include? 

Well obviously we want to extract the information from the incoming request, we
want to read the email from the request body email field and make sure you check
your view, how these inputs are named because you retrieve the values on request
body by these names, so email, password and confirm password in my case, so
request body email should work, here I will have request body password to
retrieve the password and then I will also retrieve my confirm password here
from confirm password, so these are the three values that should reach this
route. 

Now typically what you would do first is we would validate the user input, so
for example we would check is this a valid email address and do password and
confirm password match and we will do this in this course too but actually I
will have a complete module where I dive into how to validate user input because
you can of course do a lot of cool things when it comes to that and therefore I
dedicate a whole module to that. 

For now we'll ignore this and that means for now you of course don't have to
enter a valid email and you don't have to enter a valid password, you don't have
to confirm it either but of course you should do all that to have a realistic
testing environment, we'll add validation later. 

We still need the values here, at least the first two because the next step is
that we create a new user or actually there is one step we want to do before we
create a new user, do you know which step it could be? 

Well we want to find out if a user with that e-mail already exists because there
should not be any duplicate e-mails in our database. 

For that we actually can do two things, when using mongodb you could create an
index in the mongo database on your email field and give that index the unique
property. 

Now this is something you can do if you know how mongodb works, if you get a
little bit more experience with it which you can get with my mongodb course,
there I do show this scenario for example but this is only one option of
achieving this. 

An alternative is that you simply try to find a user with that e-mail, so for
that we'll use our user model which is of course a mongoose user model and there
we can find a user, we can find one user because we already know we don't want
to create a user with that e-mail if we find only one user who already has that
e-mail and we find that one user by passing a filter with these curly braces and
we'll look for the email field in our collection, so in the documents in our
collection and see if we find a user where the email field holds a value equal
to the email we're extracting here. 

So right side of the colon is the email we're extracting, left side is the field
we're looking for in the database. 

Now here we get back where we can call then to find out if this worked, we also
might get an error which I'll simply log here then and in then, I will get my
user object, so my user document you could say, you can name this however you
want. 

Now we know that if user doc exists, so if this is not undefined, then we do
have a user and if we do have a user then I certainly don't want to create a new
one with the same e-mail. 

So if this exists, I will actually return a response and I will redirect back to
/signup to inform the user that this did not work, right now not much informing
is going on as you can tell, we just redirect without showing an error message,
this is also something which I'll show you how to better solve this, how to show
error messages to the user, for now we'll just redirect back to the sign up page
and we'll not create a new user. 

If we make it past this check, we know that no user with that e-mail exists yet
and therefore we can create a new one So what we can do here then is we can
create a new user object with new user and we configure our new user and there,
we store the email, the e-mail we're retrieving here and we'll store the
password, like this for now. 

One important thing, in the user model there, right now I have a name and an
e-mail and no password. 

So I will change the user model, I don't really want to store a name, you could
do that but I'll not do it here but instead I will store a password for the user
which will be of type string and which will absolutely be required like this, so
my user model changed slightly here. 

Now with that change in the user model, if we go back to our post signup action,
I can create a user like this, we can also add a cart here, the cart by default
will be an object where items is equal to an empty array like this and this is
now a valid new user which we can save in database by calling save as you
learned and then I can return this so that we can chain another then block here
which will be called once this save action completed, so this function here will
be executed once saving is done. 

And here we can then redirect to let's say the starting page because here we
then know the user did sign up or to be precise, let's redirect to the login
page because after signing up, you need to login. 

So this should now be an authentication flow that does check for the existence
of a user and then create a new user. 

I'll quickly also go to my app.js file and at the very bottom here where I
always create a new user if we don't have one yet, I will get rid of that code
because now we have a real user creation flow so we don't need that dummy user
anymore and I will also head over to compass which I'll start to connect to my
mongo database again and in the connected database server if we have a look at
the shop database, in users we obviously have one user, the dummy user we used
before, now let's delete that user now, we don't need it anymore. 

And with all these changes and all these files saved, let's reload the sign up
page and now let's try creating a new user with a dummy e-mail, dummy password,
you don't really need to enter a confirm password because we're not checking
this anyways and click sign up. 

Now this is looking good because I'm on the login page so I was redirected, I
also have no server error, if I now reload my users collection in mongodb, in
compass, I also see this is a user with the credentials I add. 

So we did add a new user but we have a huge problem with that user, can you
identify it? 

We'll fix it in the next lecture. 

---