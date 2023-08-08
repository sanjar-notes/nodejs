## 388. Signing Users Up

<strong><em>no description</em></strong>

To store the password we should hash it so that if someone gains access to our
database, the password is not stored in plaintext. 

For that, I'll install a new package which we used before and that is bcryptjs
which allows us to hash a password in a secure way. 

After this was installed, we can rerun npm start and now in my auth controller,
I'll import bcrypt by requiring it from the bcryptjs package and in there, so in
down there in my sign up action, I'll use bcrypt and there, the hash method to
hash the password which is plaintext here with a salt of 12, so a strength of 12
so to say and I'll then continue or face errors here. 

Now if I have an error here somewhere, then it'll be a server side error, I'll
copy the logic from before, so from my feed.js controller where I just check for
the existence of a status code, if no status code exists, I'll set 500 and well
throw that error like this. 

In the then block however, we'll have our hashed password and that is the
password I now want to store in the database. 

So in here, I'll now create a new user with the help of my user constructor, so
my user model created through mongoose and I'll set the fields I need to set on
the user, so that would be email, password, name, status. 

Actually we can change the status here from require true to default of I am new,
so now we don't need to set it when creating a user, instead every user will
start with this status here, just a little adjustment. 

With that we don't need to set the status but we do need to set e-mail, password
and name. 

So the email is the extracted e-mail, the password is the hashed password, not
the extracted one but the hashed one to secure this and the name is the
extracted name. 

Now last but not least, I will call save to save that to the database and I will
return that so that we can add another then block where we get the result of
that database operation and here we know it will have succeeded, so we can
return a response with a status code of 201 because a resource was created where
I can return some json data with a message of user created and then maybe the
user ID which I can extract from the result which is the user object,
result._id. 

So now we're creating a user here, let's now save that and to see that on the
frontend, we need to go into the frontend code and in there to the app.js file
and here first of all, we need to correct our url and I also need to change
something so that we start in unauthenticated mode. 

Currently we are starting as if we were authenticated, I'll have to change that
in the frontend too. 

Now first of all in the sign up handler, let's fix that url and there, the url
will be localhost 8080/auth/signup and that will reach this route here right
because it's /signup and we only end up there for requests that start with
/auth. 

Now we defined a put request here on the backend so we have to set the method in
the second argument in this object we pass to fetch, we have to set the method
to put. 

We also need to append some data and that data will be of type application json,
so we should add the content type header and set this to application json. 

Last but not least, let's add the request body and here we'll need to use json
stringify to convert an object to json and that object will be a javascript
object with the e-mail which we can retrieve from auth data email, auth data is
an argument we'll get here and I wrote the code to make sure that we get the
data the user entered. 

So we'll get the e-mail, we'll get the password so let's also extract that from
auth data and we'll get the name from auth data, so everything which we extract
on the server side. 

This is now all passed to our backend, now in app.js, scroll up a bit more to
the very top, here in this state, you now should change isAuth to false so did
we start unauthenticated. 

Now when you when the page reloads, you start on the login page and you can
switch to sign up and there, let's create a new user, you can enter any name you
want and I accidentally hit enter which is good because we now see validation is
doing its job but now let me enter a valid password which you should remember
and click sign up and it still failed. 

Let's see what's wrong here, let's inspect for which field we're getting this 
by inspecting the network tab and then here we see ok all three fields give us
the error. 

That's kind of a strong signal that the data is simply not passed to the backend
at all, so something seems to be wrong there, indeed we can validate this by
clicking on headers, there we see there is no request payload added to this
request and that's simply a little mistake on my side. 

In app.js in the frontend code in sign up handler, here where I extract after
the e-mail and so on, that should be signupform.email.value and the same for all
the other fields too. 

So let's add sign up form in front of that and .value at the end, the same for
the name and this is how the data is stored here internally in the react app and
this how we should extract it. 

So let's give this another try, let's pick an email address, a name and a
password and now this looks much better. 

I get back user created, I'm forwarded to the login page here in my frontend, I
get that user ID and of course we can as always use mongodb compass to also take
a closer look at our database, there I got this messages database, if I reload
it now, I got a users collection in there and here I have that user. 

So that is working, the user also has a starting status, now we have no posts of
course. 

Now we can continue and we can work on logging the user in and that will now be
the interesting part because I already mentioned that authentication will now
work differently. 

---