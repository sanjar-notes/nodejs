## 384. Deleting Posts

<strong><em>no description</em></strong>

To ensure that we can also delete posts, let's start in our node rest project
and add a new route. 

This will be a delete route using the delete http method, we register such a
route by using router.delete. 

Now here, the path will be /post/:postid, for delete routes you can't send a
body but as with all routes, you can of course encode data into the urls and
that is what I'm doing here. 

Now the route is one thing, obviously we also need a controller action, so let's
go back to our feed controller and before clear image, I'll export my new action
which I'll add which will be my delete action. 

So I'll name it delete post here, it will be my standard middleware with these
three arguments being passed to the function and in there, I first of all
extract the post ID from my request params as we did it multiple times
throughout the course. 

Then we can use the post model to find a post by ID and that will be my post
with this ID of course. 

Now why would I find it by ID first? 

I can of course also use post, find by id and remove. 

Well I will use this eventually but later once we edit a user, I want to verify
whether that user created the post before I delete it, so I'll first of all find
the post with success or not and if I have an error, I'll use that old error
handling code I had before and in the then block, I'll have my post where I will
check whether the creator is the currently logged in user, so check logged in
user, this is something I can't do yet because we have no logged in user
obviously. 

For now there is one thing I can do though, I can use clear image to access the
post I retrieved and delete the image for the image url that is stored there. 

There is one other thing I actually should do and that is I should check whether
that post exists. 

So I can copy that logic from up there where I see whether post is undefined and
if it is undefined, I throw an error. 

Now if that succeeded, I delete the post image and then I return post find by ID
and remove because now I will remove it and here, I pass my posts ID again, I
can add one more then block with the result of that operation and in here, I'll
know whether that succeeded and most importantly, I'll return with a status code
of 200 which means yes we were successful and a json data package where I will
just say deleted post in a message, of course you could send any data you want. 

So with that, my delete post action is configured here in the controller, back
in my route, I can now use my feed controller delete post and assign it to that
delete route and now we just need to work on the frontend and hook up this
route. 

So there in the feed.js file which we worked in a lot already, you'll find the
delete post handler and there, you simply need to update that url you see in
there. 

So let's replace url with http localhost 8080 /feed/post/ and then post ID which
is an argument we'll get in this function. 

Now important, we want to send a delete request so we need to pass a second
argument to fetch here and set the method to delete and that is it for now, this
should now send such a request when we click the delete button. 

So make sure you save this and you're back in the code and thereafter, let's go
back to the feed and let's click delete, maybe on the first item. 

Now after reloading, it's gone here and the duck image was deleted as well. 

If I reload this app, we also should not fetch it again so it really seems to be
gone. 

So now deleting also works. 

---