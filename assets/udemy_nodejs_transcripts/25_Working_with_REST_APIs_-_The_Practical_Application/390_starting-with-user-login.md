## 390. Starting with User Login

<strong><em>no description</em></strong>

To implement authentication, we first of all need a fitting route. 

So in the auth.js route route here, I will add a new route, a post route where I
will log the user in, so it will be /login. 

We could add validation here but I don't really care about this because I will
check the email password pair anyways, so we can also directly go forward to our
controller action. 

So let's implement that, let's work on the controller action now and for that in
the auth file in the controllers folder, I'll add a new action which I'll name
login which of course is a function with request response next and then some
logic and in here as before, I'll retrieve my e-mail, whoops, from request body
e-mail, I'll retrieve the password from request body password and I now first of
all want to find out whether that e-mail address exists because if it does not,
then we already know that we can't login. 

So I'll use my user model and find one to find one user where the e-mail equals
the extracted e-mail I got here. 

We can succeed or we can fail with that, if we fail we'll use that same handler
we used before so we'll throw an error because here failing of course means that
we simply had some network error or some error with the database. 

If we make it into the then block, we had a user object but that does not mean
that we found a user, it could be undefined if no user was found, we basically
always end up in the then block if no error is thrown. 

So here I'll check if user is not defined and if it is not defined, I'll create
a new error object where I add or where I add a message of a user with this
e-mail could not be found, anything you want, where I'll set a status code of
and now you could choose different codes, you could go for 404 because no user
was found or 401 for not authenticated and then I'll throw that error. 

If we make it past this if check, we know that we have that e-mail address, now
we need to validate the password. 

For this, I'll quickly create a new variable, loaded user and I'll store my user
in that variable so that I can use it in other functions later too. 

Now I'll use bcrypt again and there I'll use the compare method to compare the
password the user entered with the password I got stored, so with that hashed
password, so user.password is password I'm looking for. 

I'll return this because this will give me a promise and hence I can add another
then block here. 

Here I get back true or false depending on whether this is equal or not and if
it is not equal, of course then the user did enter a wrong password. 

So here I'll create another error, wrong password maybe and I'll add a status
code of 401 again and throw that error but if we make it past the if check, then
we know the password is equal to the password the user entered. 

So the user entered a correct password and now we need to generate such a json
web token. 

Let's do that next. 

---