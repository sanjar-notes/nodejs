## 414. Fixing a Bug - The Missing Username

<strong><em>no description</em></strong>

By the way if you're wondering why there is no name being displayed, I have it
back on my backend code here in get posts, we should add populate creator to not
just fetch the creator ID but the full object for that creator and on create
post, well there we have the issue that the post I am sending through socket.io
is just a post object where I did add my creator ID but not all the creator
data. 

Now how can we fix that or how can we add more data? 

Well we can send the entire post _doc data, so all the data about the post but
set the creator equal to an object where we do have the _id, that will be our
request user ID but where I also then add my name field which will be user.name
and user.name can be used because of fetching the user here and that will be an
object which also has a name. 

So that's just a little tweak we want to add here to send all the data with a
created post that we need on the frontend. 

If we now save that and we reload, we get the data up because of that change in
get posts and if I now add a new post, another duck, choose a duck, add some
content and click acccept, we also see the name there. 

Now both users are named Max but still keep in mind, the left user we logged in
with is a different user than on the right and still we get the updates here due
to socket.io. 

---