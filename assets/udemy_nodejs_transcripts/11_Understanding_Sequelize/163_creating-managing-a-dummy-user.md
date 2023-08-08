## 163. Creating & Managing a Dummy User

<strong><em>no description</em></strong>

So we need a user and as I mentioned, for now we have no authentication process,
so for the moment I will create a user manually. 

First of all, I will remove this force through call because I don't always want
to overwrite my tables otherwise all our products and so on will always be gone,
so I'll go back to sync now that the relations are set up and once all the
tables were created, so in this then call here, I actually now also want to
create my user and therefore here, I will use my user model and first of all
check if I find a user with the ID one and this is of course just some dummy
code to see if I do have one user because I only need one for now as we have no
authentication and if I do have it, I'll not create a new one, if I don't have
it I will. 

So here I have user find by id one and I will return this and therefore also
take app listen out of this then block and then add a new then block where I
will get my retrieved user. 

Here I'll then check if I don't have a user, so if this is null because if I
don't have a user, I want to create a new one by calling user create and there
I'll pass in a javascript object where I set the name to Max and the email to
some dummy e-mail, you can enter any values you want here, just make sure you
populate all the fields you defined in your user model. 

This also returns a promise so I'll return this too but also we might never
execute this because we already got a user. 

So for this case I'll return user but now we're inconsistent because now this
anonymous function either returns a promise or just an object, we should always
return the same so that we can chain then here successfully and therefore I will
actually call promise resolve here which is essentially a promise that will
immediately resolve to user. 

Technically you can omit this though because if you return a value in a then
block, it is automatically wrapped into a new promise, just wanted to highlight
that you should make sure that the values are equal but here it's managed for us
and therefore here I now definitely know that I got a user, we can console log
the user here and I also start listening to my server here. 

So here's my user creation result that I get back and if I go back to my
workbench database and I refresh the users table, we see the user here too. 

And if I do restart my server with npm start, that still works and it doesn't
create a new user here because we already have one. 

So this code is working as it should, I'll comment out this and with this change
made, we now always have a user available. 

As a next step, I'll will register a new middleware because I want to store that
user in my request so that I can use it from anywhere in my app conveniently. 

So maybe here I'll add a new middleware, I'll simply add a function with request
response in next as you learned it before in this course and in here, I want to
reach out to my database and retrieve my user with user find by id one. 

Now you might be wondering if this can ever return a user and if we only create
it down there. 

Now keep in mind, app use here only registers a middleware so for an incoming
request, we will then execute this function. 

Npm start runs this code for the first time and npm start is what runs sequelize
here not incoming requests, incoming requests are only funneled through our
middleware. 

So npm start runs this, this code which sets up our database but never this
anonymous function, it just registers it as middleware for incoming requests. 

So this code will only run for incoming requests which on the other hand can
only reach this if we did successfully start our server here with app listen and
that in turn is only true if we are done with our initialization code here, so
we are guaranteed to find a user here. 

So we can find a user by id here and what do we want to do with my user in the
then block then? 

Well I want to store it in a request. 

So here I will set request user equal to user and we can do that, we can simply
add a new field to our request object, we should just make sure we don't
overwrite an existing one, like body. 

But user is undefined by default, now I'm storing the user I retrieved from the
database in there. 

Also keep in mind the user we're retrieving from the database here is not just a
javascript object with the values stored in a database, it's a sequelize object
with the value stored in the database and with all these utility methods
sequelize added, like destroy. 

So we're storing this sequelize object here in the request and not just a
javascript object with the field values, it is that we got the extended version
here and therefore whenever we call request user in the future in our app, we
can also execute methods like destroy. 

So with that, all I need to do is I need to call next here of course so that we
can continue with the next step if we get our user and stored it. 

Now with that, we've got the user set up and retrieved, let's now make sure that
we can also use it to create new products that are associated to that user. 

---