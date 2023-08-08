## 428. Adding a Login Query & a Resolver

<strong><em>no description</em></strong>

Now that we're able to create new users, how does authentication work in the
graphql world? 

Does it work in a similar way to rest APIs, do we use sessions again? 

Well remember this slide, a graphql API is also stateless and client
independent, so generally we still authenticate by using such a token which we
then attach to every request that should be able to access protected resources
and a login action is in the end just a normal query where we send some user
data and where we want to get back a token, right. 

So in the end what we can do here is the following, on our backend code, in our
schema, I will now define a real query instead of my dummy placeholder hello
query which I'll name login. 

Here I'll need some data and I could again define my own input, like here I did
for user input data but also to show how to use multiple arguments, I will
expect an email which is a string and a password which is a string and then I
will return not a user but some data that contains let's say the user id and the
token because these are the two pieces of information I happen to need here and
that makes sense as a response. 

Of course you could also return the overall user object. 

So here I'll define new type, I'll name it auth data and that will be my token
which is a string and my user ID which will be a string, this is the data I will
return when someone sends a query to login. 

Now we need a resolver for this of course, so let's head over to resolvers and
after create user, I'll add my login resolver, there again I get my args and I
can use destructuring again to retrieve the email and the password argument
which I both get because I defined both here in my login query. 

Again I want to use async await, so I will turn this into an async function with
this syntax and in there, in my login resolver, the goal  now of course is to
find a user with the right email address and then confirm the password. 

So first of all, I'll get my user by awaiting for user find one where I look for
an e-mail address in the database that should match the e-mail I'm getting as an
argument. 

If this is not set, if the user is undefined now, I know that I've found no user
with that e-mail address and therefore I can create a new error where I say user
not found or whatever you want to set as an error message. 

I can set a code here just as I did it for create user of let's say 404 because
we didn't find the user or 401 because the user could not authenticate, I'll go
with 401 and I'll throw that error. 

If we have passed this if check, then we know that we have a user with that
e-mail address, now we need to check the password. 

For that we used the bcrypt package and there, the compare function and we pass
in the password, send with the request and the stored hashed password. 

Now this is an asynchronous operation which gives us a promise so we can await
that and I get back the isEqual response. 

Now if it's not equal, then I know the user entered a wrong password, so I can
create a new error here where I say password is incorrect and I can also set an
error code or 401 here and then also throw that error of course, otherwise both
the email exists and the password is correct and now I can generate a token. 

And for that, I'll again import my json web token package by requiring json web
token here and then down there in the login resolver, I will generate a token by
running JWT sign, here you now pass the data you want to encode in the token,
that could be your user ID which you get from user_id toString to convert it to
a string, maybe you also want to encode the email by getting that from the user
you retrieve from the database and the second argument to the sign method then
is your super secret secret which you use for signing the token which you then
also use for verifying it, something we'll do later and I'll configure the token
with the third argument by setting the expires key in that object you pass to
the third argument to one hour, so that the token expires after one hour. 

That is exactly what we did in the rest API section too. 

Now I will return that token in a token key and make sure to match that schema
you defined here, so token and user ID is returned. 

So in the resolver, we return the token on the token key and the user ID which
is again my user _id toString. 

And now with that, we have a login query in place where we send like a get
request to log the user in, to get the token and so on you could say. 

Now we need to wire that up to the frontend in the next step and then of course,
test it. 

If you're feeling bold, also try that on your own of course. 

---