## 394. Connecting Posts & Users

<strong><em>no description</em></strong>

Let's connect posts and users. 

For this in my backend code, first of all I'll go to my post model and there we
have that creator object, right. 

Well that was like an intermediate solution, now that we know users in our
application, creator will no longer be of type object type schema types object
ID because I will store a reference to a user, so this will now be a reference
to a user here, this will also be require true and not required string, what I
had before, this was a mistake of course. 

So now we have a relation between posts and users, we store the creator of a
post in every post we create and on the user model, we add the post to the list
of posts for that user. 

That of course means we now need to adjust our feed controller in the place
where we do create new posts. 

There in create post, the validation which we do at the beginning still is all
right but then before I create the post, I should get my user ID. 

Now I remember in my isAuth middleware, I do actually store that in the request
object, I get it from the decoded token, so we have that user ID available here.


Now with that information, I'll set creator equal to request user ID, that will
be a string not an object ID but mongoose will take care about that and convert
it, so now we create a new post assigned to that user. 

Now once I save the post, I'll not immediately send the response though, instead
I now also want to add that post to the list of posts for the given user. 

Therefore I'll import my user model into that feed.js . 

file by requiring it from the models folder of course and in create post once we
did save the post, I'll use that user model to find the user by ID for the
request user ID, so for that user id I extracted from the token. 

Then I'll return this and close this then block and add a new then block where I
now get that user that was created. 

Now in this second then block here, I now have a user, so not the user which was
created but the user which was found, I have that user which is the currently
logged in user and now I can take that user object which is a mongoose model
here in the end and I can access the post of this user, keep in mind the user
model has a posts property. 

I can access this post and I can push the newly created post, so this post here,
I can push that posts object to that user and mongoose will do all the heavy
lifting of pulling out the post ID and adding that to the user actually. 

Now I'll also add a new variable at the top which I'll name creator which is
uninitialized and once I found a user, I'll store the user in that creator
variable. 

Now what do I need that for? 

Well I do update my user here, that means that here I will also call user save
and I will return that and hence we need another then block where I get the
result of this operation. 

Now in this next block, I'll send my response and there I will not just send the
post but I also want to send information about the creator, so here I'll add a
creator key and that will be let's say some object with an ID _id of creator _id
and name which is creator name. 

So I'm just passing this extra information with the response and if I want to do
that, I have to do it through a variable. 

So now posts get saved and get connected to users in both directions, let's try
that out. 

Let's save this code, go back to the frontend and there let's create a new post.


Good old duck again, let's add a duck image, a duck, how lovely, click accept
here and I get an error. 

Let's see what's going wrong, I do get back a response with a post and the
problem is that post holds my user data actually which is a mistake on my side
of course. 

The post I am sending back here is not the result, the result here is the user
which I updated. 

Here post should be the post model, the post object I created up there, so
that's my mistake. 

I do create a post there, I store it in a constant, I can reuse that constant
down there to send data about that create post back to the client. 

So let me save that, now still what we'll see is in the database, if I go to the
post collection, it was created though because it only failed when it came to
sending back the correct data and there we see that it's also connected to a
user which ends with ABC. 

If you have a look at the users, this is this user and there in posts, we also
find the ID of the post which ends with 6E5, yes that is correct. 

So this worked, now only a minor mistake here regarding the data I send back. 

Let's simply give this a try again, here's our post, let's add a cup like this,
superhot and now this works without an error. 

So now we are able to connect posts and users, let's now take it a step further
and make sure that editing and deleting is only possible for posts that belong
to the currently logged in user. 

---