## 396. Clearing Post-User Relations

<strong><em>no description</em></strong>

Now talking about deleting, there's one more thing we should do in case we do
succeed. 

We should clear the relation of posts and users. 

If we refresh the post collection, we only have one item there but if I have a
look at my users there now, the first user has a couple of posts and the second
user has so too because right now we have no logic to clear posts when I delete
them, to clear relations and we should of course do that. 

Now how can we get rid of a relation? 

Well we delete the post anyways, so there's nothing we need to do there but on
the user, we need to pull our reference. 

To do that we should find the user after we deleted a post let's say, so here
I'll find a user by ID and I can use my request user ID here and I will return
that user object in there. 

Well let's grab that code and add another then block where I will have that user
mongoose model fetched from my database. 

Now in there, I will use my user model and there, the posts array and then there
is a pull method mongoose gives me,  there I need to pass the ID of the post I
want to remove. 

Now I deleted the post already here but the post ID is still available of
course, so I can pass post ID here. 

Now I can call save here to save that updated user and return that, grab the
response one more time and add another then block with the result of that
operation and here, I'm done with clearing the relation. 

Now to see that in action, let me actually get rid of all users manually by
using mongodb compass, also get rid of all posts and logout here and let's
create a brand new user because we cleared all users, like this. 

Let's login with that user and let's create a new post, a duck, use that duck
image, it ducks around for sure and click accept and before we do anything,
let's go back to mongoose, to mongodb compass I mean, there we can see that this
post has this creator and this user more importantly has this post in his posts
array. 

Now I'm logged in with the right user, let's click delete. 

This worked and now if I refresh posts, we got no posts in there because I
deleted the only post we had and in users, this array is now also empty, so now
we're clearing this as well. 

---