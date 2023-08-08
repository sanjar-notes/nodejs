## 415. Updating Posts On All Connected Clients

<strong><em>no description</em></strong>

Now we worked on code that allows us to emit the event when we create a new
post. 

Now obviously we're not just creating posts, we're also updating or deleting
posts, we want to be able to handle that too. 

Now let's do that together and let's continue with updating posts, so on the
backend in the feed controller, I'll scroll down to the update post method and
in there, we want to emit an event once we're done updating, so towards the end,
once we got our result we save the post and we're sending a response. 

Here I'll again use io, get io to get access to our established io connection
you could say and I'll again emit on this posts channel and I'll emit my data
just as before. 

Now I will keep my pattern of having an action where I this time write update
because this is the action we performed and my post is then my result here
because result turns out to be the result of my saving operation. 

Now just as before, I want to be sure that I also have some user data in there,
so we'll actually scroll up or we find that post and I will populate it with my
creator data, this again will take that creator ID which we stored in the post
object, reach out to the users database or the users collection, fetch the data
for that specific user and add it here in our post. 

Now I do emit this event where I send my created post and let's now go back to
our frontend application here and also establish some code here to update our
posts. 

For this, after this add post function, I'll add a new function which I'll name
update post where I again get my post data and then I do something with that in
the arrow function and as before, I prepared some code which we just copy in
there which we'll add or which we'll update to post in our list of posts. 

Now also scroll down in your react code here in the same file to the finish edit
handler because there where I also have some logic to edit the post, here I will
get rid of that, I will actually get rid of this entire part here and also of my
update post assignment in this return statement in set state call because I now
no longer update it here but I do emit the event to all connected clients
including the client who did, well send that update and therefore I can also set
up my listener and use that with this new update post function I copied in up
there. 

So let me now go up and here where I have my established listener for the post
event, I'll add an else/if block to see if the action maybe is updated if it's
not create in which case I'll call this update post and pass data.post to that. 

Now before this will work, let me go back to the server side code and there
since I do populate my creator when finding that post in the update post
function here, this check here will actually fail where I do check if the ID
which is now not the ID anymore but the full creator object is equal to the
request user ID. 

So here I actually want to access creator._id to string right because we're
populating the creator field with the full user data, it's not just the ID
anymore. 

So we would fail editing this post if we don't make this change. 

And now if we save both and we go back and reload both pages, I deleted one post
in the meantime so I only got two anymore and let me now edit this a cup post
here, add a couple of exclamation marks maybe and click accept and you'll see it
added or being changed on both clients. 

So this is now also working. 

---