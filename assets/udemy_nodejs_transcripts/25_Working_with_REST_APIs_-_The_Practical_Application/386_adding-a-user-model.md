## 386. Adding a User Model

<strong><em>no description</em></strong>

Now we worked a lot on our posts, I now want to work on my users and for that,
we first of all need to add a new model in our node project. 

There, I'll add a user.js file where I define how a user should look like in my
application. 

So here I'll import mongoose and of course feel free to do these steps on your
own, we did them a couple of times, I will access my schema here and then I'll
define my user schema with new schema here and we'll add some properties of
course, by the end I'll export a mongoose model which I'll name user hence it'll
get stored in a users collection which uses this user schema. 

Now how should a user look like? 

Obviously that is totally up to you, to fit my frontend, a user should have an
e-mail which will be of type string and which is required, a user also will have
a password which is of type string and which will be required. 

A user also will have a name in my application, type string and required, you
guessed it and a user here also will have a status, so status is also of type
string and required, that is this thing which caused this error in the frontend
all the time because we couldn't load it. 

Now a user will also have a couple of posts, so I'll add my posts here, this
will be an array and now each object in that array will be of type schema types
object ID because this will be a reference to a post and therefore I add this
ref key and add the post model, so I'll store references to posts in my users or
on my users. 

This is how users should look like, if you want you can also add the timestamps,
I don't need them here, so now I got my model set up. 

We can now use that model to set up a sign up and later, also a login route. 

So let's create a new route and I'll name that user.js or maybe auth.js because
it will be authentication related. 

In there just as before, we import express by requiring express, we then create
that express router by calling express router as a function like this and we
have of course export this router. 

Now in-between we define our user or our authentication related routes and there
for example, I want to have a post route and you could argue that you also set a
put route maybe, let's go for a put route because actually we create a user
once, so we could also say whether it's new or we overwrite existing data, we
put the data but both would be fine. 

Here we'll have sign up as a route let's say and then I need some controller of
course. 

Now I'll also add validation and to actually reach these routes, we have to go
to the app.js file and there where I import my feed routes, I'll duplicate this
and also set up an auth routes constant where I import routes auth. 

And then at the bottom of the file where I have my feed routes, I'll also add
/auth to forward requests that start with /auth in the path to auth routes. 

Now we are able to reach these routes and now we need the controller. 

So let's work on the controller and add validation in the next lecture. 

---