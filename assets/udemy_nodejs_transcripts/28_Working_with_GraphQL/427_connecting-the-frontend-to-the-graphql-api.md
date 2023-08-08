## 427. Connecting the Frontend to the GraphQL API

<strong><em>no description</em></strong>

Now it's finally time to work on that react application we have as a frontend
here which you also find attached to this lecture again in case you skipped the
other modules, so react application will not work on the code here too much
because this is no react course and now I'm interested in signing users up. 

This is done in the app.js file there and there in the sign up handler. 

Here we send the request for creating a new user but this is of course a request
from the rest API world. 

You learned that from now on, there only is /graphql for all our API requests
and then here this has to be a post request. 

The type is still application json and this needs to be set but the body will
now be in the graphql query language and for this, I'll create a new constant
which I'll name graphql query, the name is up to you though and this will be a
javascript object where you need to have a query key, that is required even for
mutations. 

The value here then is a string which you create with double back ticks, back
ticks so that you can write multiline string, single quotation marks will not do
it and here you add mutation to define that you're running a mutation now, curly
braces and now the name of the mutation and the name of the mutation you want to
execute is create user. 

Essentially you could just copy this query here now, this is what you could copy
and what you could move into your query here. 

Now of course we need to replace these values with the values we fetch from the
user input though and we can do that by using dollar sign curly braces in this
back tick enclosed string because this is a template literal and this allows us
to inject values. 

Now just make sure you keep the double quotation marks around and the injected
values otherwise this will fail because this query language here needs to
enclose strings in double quotation marks. 

Now the email can be retrieved just as we retrieve it down there, so we can copy
that code up there and the same of course also for the name and the password, so
for the name, we also inject the value of dollar sign curly braces and we use
that syntax from below and the same for the password. 

Let's copy that and replace this with the injected password code. 

Now here I am retrieving ID and email, it's up to you, we don't need any of the
data, I'll leave it like this and now this is the object I want to stringify, so
my graphql query object. 

Now I don't need to check the status code here because that will not be set,
it's either 200 or 500, I'll cut it here and I'll remove that and in the
response data then block here, where I have the parsed request, response body,
there I can now check if response data has errors and there on the first error,
I could check for the status field. 

So here I will check if response data has errors, if that's the case I'll check
if response state errors and there the first element has a status field just as
I explained, accessing this field and if that is equal to 422 and then I can
throw my validation failed error. 

Maybe we have other kinds of errors so I'll check another of thing here in case
we don't throw that first error, I'll check just for the existence of errors and
there I would throw another new error where I just throw user creation failed,
like this. 

Now after these error checks, I'm printing my response data here and actually we
should have all we need to sign users up now. 

So let's run our frontend server with npm start, it runs on localhost 3000 so
let's open that here and there, let's navigate to the sign up page and create a
new user. 

Now this is an email address which is already taken and actually therefore, I
should fail doing that. 

Let me click sign up and indeed I get an error but this is a different error
than you might expect. 

It's an error here where my method is not allowed and this can be a tricky thing
to fix if you're brand new to graphql. 

Well the reason for this error is we get this error actually as a response to
our options request here, not to our post request. 

Now you might remember that I explained that the browser sends an options
request before it sends the post, patch, put, delete or so on request. 

The problem is express graphql automatically declines anything which is not a
post or get request, so the options request is denied. 

The solution is to go to that middleware where I setup my cors headers and
there, I check if my request method is equal to options and if it is an options
request, then here I'll return res send status 200, so I'll simply send an empty
response with a status code of 200. 

I return so that this code is not executed and therefore options requests never
make it to the graphql endpoint but still get a valid response. 

And with that if I now go back to my frontend, I clear my errors and sign up
again, now the user creation fails but now it simply fails because if you look
into our data, we see that the user exists already and that is what we expected
and now if we take a valid email address which is not taken yet, it actually
succeeds and here is the response I get back from graphql, my data that is
provided automatically for the create user query, the to data fields I
requested. 

And this is how we connect the frontend to our backend by simply sending a post
request with a valid graphql query expression. 

---