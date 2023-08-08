## 443. Managing the User Status

<strong><em>no description</em></strong>

We're almost done, let's now make sure we can view our user status and delete it
and as I already mentioned at the end of the last lecture, this again is a great
practice for you so definitely feel free to try this on your own first, pause
the video now and implement these two functionalities. 

Of course we'll also do it together after a short pause. 

So did you succeed? 

Well let's try it together and I'll do both in one go. 

I need to add two things, one query and one mutation. 

The query is for getting the status and actually since we're not using the
approach I mentioned earlier where we add a new endpoint for everything, we have
to remember that with graphql, we can control which data we get back. 

So I will add a general user query without any arguments, always for the
currently logged in user and I will return a user object here. 

Now in my mutations, I will add my update status mutation, I could add an update
user mutation if I generally would be fine with the user changing, since I have
no such functionality planned in my app, I will only add a special mutation for
just the status otherwise we could of course go with a more generic approach
here too. 

There I expect to get the status as a string and I will return the updated user.


With that, we can move on to our resolvers, let me add the code for returning a
user, so for this user query. 

There I get no arguments, so I get that object but I will not retrieve anything
from there and again I will write this as a async function to be able to use the
await keyword. 

I'll then check if the user is authenticated, if he's not, then well we have a
problem and I will not continue otherwise I will get my user by awaiting for
user find by ID and I can use the user ID stored in the request and on that user
here, I'm interested in the status right, that's the status I want to return. 

So if I find no user for that ID somehow, then I will basically do the same I
did when I found no post, I'll return error, no user found. 

If I do have a user though, then I will simply return a response and that is my
whole user data, I just will make sure to replace the ID with user_id toString. 

So I can now theoretically fetch all the data about a user I'm interested in but
obviously I'll implement that in a way that I only fetch the status and that is
something I do here in my feed.js file of my frontend application. 

There in componentDidMount, I send a request to an endpoint which does not exist
anymore, instead we're now of course targeting graphql, the method here will now
be post. 

I will send the token but I'll also set the content type to application json and
I'll set the body to my query and that query is something I need to create up
there, graphql query is a constant I'll create here. 

That is an object with the query key which again is surrounded by double back
ticks or single back ticks but I need two, opening and closing and here I'll
send my request to my user query or I'll use the user query and of the data I
get back, I'm not interested in the name or the email, I'm only interested in
the status. 

That is my graphql query and that is what I'll send in stringified version to
that endpoint. 

Again handling errors like this will not work, let's instead grab the code we
have below, here where I just check for the existence of the errors object after
parsing the request body, so here fetching status failed would be my error
message and when I extract the data, I need to drill into the data field and
then the status field. 

Now if I save that and I reload, I got an internal error here, cannot return
null, let's quickly check our resolver, the user resolver, I return my user
object here but I did not save it I guess, this now looks better but I'm not
seeing the status here and I got an error about which I'll take care in a
second. 

My status here is not found in data, I have to drill into the user field as
well. 

We can see that if we go to the network tab and have a look at that request
where we get that data, we get data and in there, user which is the name of our
query of course and I forgot that but obviously query name is always where the
data is stored in and that then has the status field. 

So this is a change that is required and now with that, we see the status and
this error message also is gone, like that. 

So this is it, now let's also make sure we can update a status and for that,
let's first of all make sure we do something for this schema we added, for the
update status schema in our resolvers file. 

So this is the last resolver function I'll add here, update status. 

I'll get my status argument and the request of course and I will as before use
my async function syntax and in here, I first of all will check whether the user
is authenticated, if that's not the case, we throw an error and then I'll get my
user by awaiting for user find by ID for the request user ID, so for the logged
in user. 

If I have no user then, we get a problem so I will copy that code from above and
throw an error if that's the case otherwise I'll set the user status to the new
status I'm getting as an argument and then I will await user save to save the
updated user. 

I can then return an object where I take my user.data and where I replace the
ID, so user ID with the stringified version of it and this is my update status
mutation. 

Now last but not least, I also need to edit this on the frontend, so in my react
app and there, we simply search for the status update handler here where we of
course send a request to graphql and that should be a post request. 

The headers are all right and I will define my graphql query here, is an object
with the query key, my back ticks of course and the query now is a mutation with
the name update status or whatever you defined in your graphql schema file and
there I need to pass in the status which is a string, so we need double
quotation marks around the value which I'll now inject here and the value is
this state status, this is where the status is stored which the user enters into
the input field and of the data I get back, I'm only interested in the status. 

Then we want to send this here in a stringified version and again we don't
handle errors here, we handled them as we do up there checking for the existence
of the errors object in our parsed response data and that is already it. 

Now if I save that and save the backend as well, if I add a couple of
exclamation marks and I click update, seems to succeed and we can validate this
by reloading. 

If I now login with a different user, there of course we should not see that
updated status, there we see the status of that user. 

And with that, we moved our entire rest API over to graphql and I hope you see
the power graphql gives you by being more flexible regarding the data you fetch
from the backend and therefore, your frontend development can move faster
because your backend gives you the entire bandwidth of data you might be
interested in. 

---