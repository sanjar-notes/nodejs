## 417. Deleting Posts Across Clients

<strong><em>no description</em></strong>

We're now using socket.io to successfully update and create posts, now let's of
course also align the deletion of posts and for that, let's first of all go back
to the backend code, to the feed controller and find our delete post methods
here, there it is. 

Now just as before, I want to emit an event once we're done deleting. 

So I will do that right before I send my response here let's say. 

I will use io, get io to get that connection and then I will emit to the posts
channel and I will keep my pattern of defining what happened to my posts inside
of the data package I'm emitting. 

So in here, I'll add my action which I'll name delete or where I have a value of
delete I should say and then my post field here is just a post ID, whoops,
written like that which in this delete post function I am extracting up there,
so I'm passing that ID through that event I'm now emitting through socket.io,
that is what happens on the backend. 

Now let's move on to the frontend, to the react code of course and there just as
before, we want to do something when we deleted a post and I'll keep it simple,
I'll simply reload the page here. 

You could of course implement some code here that simply finds that post and
change it and just deletes it but I'll keep it relatively simple and just load
the entire page. 

If we scroll down a little bit to the delete post handler, here we can therefore
also comment out this code and instead just call this load posts to reload, not
the page but reload the posts. 

Essentially this will make sure that pagination also is considered correctly and
now if I scroll up again to componentDidMount where I have my other listeners
for socket.io, I'll check if the data action might be delete which is the latest
action we're emitting on the server and then I just call this load posts to
basically load all posts again. 

Now this is my frontend code and now if I go back to my application and I do
delete another doc here, it reloads and it also reloaded the posts on the page
as you see. 

So now we're also orchestrating deletion to happen across multiple clients
through socket.io. 

---