## 429. Adding Login Functionality

<strong><em>no description</em></strong>

Did you try it on your own? 

Well let's wire it up together. 

For that in the frontend, we need to go to the login handler which is where we
do login the users. 

In the login handler, I need to send a request to /graphql of course, it's a
post request and now I'll define my query, so my graphql query, you can name
this constant however you want. 

It's a javascript object with the query keyword and then a string that defines
the query and for a normal query, you now don't repeat query, you just start
right away with the curly braces as we did it in the graphiql interface earlier.


Now let me split this over multiple lines to make it easier to read. 

In that query here, I want to reach out to my login query, so to that query I
defined in that schema, login. 

I need to pass email and password here, so login actually gets curly braces here
and the email between double quotation marks will be the email I also extract
down there, auth data email in this case, the second argument separated with a
comma in this function-like call here is the password, also enclosed between
double quotation marks and there you inject auth password, auth data password. 

Now we can get back some data which we enclose between curly braces and the data
we get back, well there I'm interested in both the token and the user id, so I
specify both between these curly braces here. 

That is the query I want to execute and that is the data I pass to json
stringify on my request body here. 

Now as you learned, checking the response like this will not work, instead we
can grab the code we used for signing up, this code here and copy that over, in
the login handler we therefore remove these checks in the first then block, in
the second then block we now add the copied checks and here I just will say user
login failed because creation doesn't make much sense here. 

Thereafter we set the state and the way we retrieve data from the response will
not work, I can already say that. 

Now why will it not work? 

Well for that, let's first of all run the query in the graphiql interface. 

There let me get rid of that mutation, instead let's run a query, you can also
omit this by the way and in there, it only sees hello, I need to reload, it now
sees login. 

Let me specify the valid email which I did use for the user and the password and
now I want to get the token and the user id. 

If I now hit control enter, I do get my data here and I do get it on an object
which has a data field that is always added by graphql. 

In there, I have the name of my query which was login and in there I have my
response data. 

So this is my res data object in my react code though, so res data will be this
entire object. 

So if I want to get the token, I need to drill into it, into data login token. 

So in places where I just accessed res data token, I instead need to do res data
data login token and that is now the case for all the places where I retrieve
something from the response data, I need to add data login. 

With that in place, if I now save that frontend code and the backend should be
saved too of course, we can go back to our app and try logging in here and
indeed we then get an error for fetching the posts which makes sense because we
try to use a rest API url which does not exist but logging in actually
succeeded. 

So we got users sign up and login in place, we now need to add some routes for
or some endpoints for getting posts and for adding posts of course and we then
also want to use that token we do get to protect certain but not all graphql
endpoints. 

These will all be steps with which we continue. 

---