## 413. Synchronizing POST Additions

<strong><em>no description</em></strong>

Now that we have a way of sharing our io connections across multiple files,
let's go ahead and in feed.js, in our controller on the backend, there I want to
use that io or that socket.js file. 

So here maybe above my other imports, I'll add a new import and I'll name that
io, the name is up to you though and I will require dots going up one level and
then /socket, so this file we just created, I will require that object therefore
and there I can now call get io to get my existing io object which I do
initialize first in app.js, right, we initialize it here so this will be
initialized by the time we use it here. 

So now this is how I import it here in feed.js. 

Now inside of create post, I now want to use that and of course in create posts
I want to use it once I'm done creating the post essentially. 

So right before I sent my response back and that response will go back to the
user who created the post, we'll not change this, we have to send back a
response but now I want to inform all other users and for that, I can use io and
there I can call get io to get my established io object or connection we set up
in app.js and now there are a couple of helpful methods the io, the socket.io
package gives you and one of them is emit. 

There also would be broadcast, the difference is that emit will now send a
message to all connected users, broadcast sends it to all users except for the
one from which this request was sent. 

Now I'll actually go with all users with emit, then you define an event name and
that name is totally up to you, I'll name it posts and I'll define the data I
want to send. 

This is also up to you, typically it's a javascript object and here I'll send an
object with any data you want. 

I'll define an action key to inform the clients what happened, the channel you
could say is posts but the action now is create and that is just one way of
implementing this of course and then the post that was created will be stored in
let's say a post key and that is the post which we do save here. 

So I'm sending this post object in this data package on this posts channel you
could say. 

Now with that, we're sending this to all connected clients. 

In the next step we'll have to adjust our client side code to also react to such
incoming events and for that I'll go back to my client side code and here in
componentDidMount in the feed.js file, I want to set up the code to listen to
incoming data from socket.io because in my app, the events I broadcast or I emit
on the server happened to be related to post which I manage in the feed.js file
in the end, so here is where I'm interested in, well changes to that. 

So in componentDidMount ofter opening my socket, I will actually store something
which is returned by open socket and that is my socket, so the socket, the
connection which was opened, I'll store that in a constant named socket, the
name is up to you and now on that socket, we can use the on method to listen to
certain events and now here we want to use that same event name we used on the
backend. 

So there I used posts, if you use something different you now have to change
that in your frontend too, so I use posts and in the frontend I therefore listen
to the posts event and there we will get some data. 

Now I know that due to the set up I chose here, my object which I send on the
backend will have an action key that defines what happened to posts but that's
just the pattern I established here, that is not enforced by socket.io. 

You can send any data you want here, you don't have to have an action key, I
want that though because I'll actually send different events or different kinds
of operations on posts through the same channel eventually. 

So here I'll have my data object and I can check data action and see if that is
equal to create which in my case it will be for that event I'm emitting on the
backend and then I want to call this add post, so this function we created
before and I'll pass data post because again, I'm creating this whole set up and
I know that on the backend, that data package I'm sending through socket.io will
have a post key with the post that was created. 

So that is the post which I will send to add post which will be rendered by that
code then. 

And that is it for now, let's save that and also save all your backend code and
go back to the application and now to see that in action, I'll actually fake to
have a second client. 

So I will actually open a different browser, Firefox and this is essentially the
same as if it would run on a different PC now, so these two browsers are now
like two different machines and you can tell by the fact that I'm not logged in
here on Firefox, get a little display back here but we can ignore that for now. 

So let's use let's say the test2 user, create a different user if you don't have
one and now I'm logged in on Firefox on the left and on Chrome on the right. 

Now on Chrome, this is a test user and on the left, it's a test2@test.com user
named Max. 

Now let me create a new post here, I'll name that a duck and choose that duck
image here and click accept and you see it'll show up on the left too, you'll
also see it show up on the right two times simply because there, I also get
informed about this created post through my socket because I'm not filtering to
not send this to the client who sent the request and since I also have some code
for rendering the post in my finish edit handler in the feed.js file, if you
scroll down a little bit, here the post will show up there as well. 

To prevent this from happening, I can remove this else/if case. 

If I now save this, all the pages will automatically reload and now let's try
this again, a cup, let's choose that cup image, accept and you see it show up on
the left side too and that is the interesting thing. 

I never reloaded the page on left and still we see the new post show up there,
that is simply due to socket.io where we have an established connection on both
clients now and therefore it also updates on the left or add this item on the
left due to the code we added on our frontend. 

---