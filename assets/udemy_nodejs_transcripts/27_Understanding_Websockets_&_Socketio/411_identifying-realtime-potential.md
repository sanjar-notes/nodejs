## 411. Identifying Realtime Potential

<strong><em>no description</em></strong>

If we have a look at our application here, what could we do in real time? 

Well what would be interesting is that if we create a new post with user a, that
we can instantly see it with user b too. 

And for that, we need to add some code in our client and then also on our
backend. 

Now let's actually start with the client, let's say we want to react to a new
post being created and we then want to render it in the client instantly. 

For this in my react app after this componentDidMount function, before load
posts let's say, I'll add a new function, add post with this syntax, I expect to
get the data about the post as an argument, so I'm using a normal arrow function
here and in here, I want to render that post to the screen. 

Now for that, since this is not a react course, I prepared some code which you
find attached to this video, just copy it here. 

In this code snippet, we're using some react functionality, set state to
basically update our existing data we used in this react application with this
new post we received here and I will also take care about pagination to insert
this post in the right place. 

That is the end what I'm doing here, the important thing is that I'm using some
react functionality here so that we don't have to reload the browser page, I
simply change the existing dom. 

This is what react will do for me with this code snippet and as mentioned before
if you want to learn more about react, dive into some dedicated react resources
of course. 

Now we got add post but we're never calling it. 

My idea is that I want to call it whenever we do create a new post on some other
client, now how do we do that? 

Well for that, let's go back to the node code. 

We have to go to the place that runs or to the code that runs when new post is
created and that would be in the feed controller to create post function of
course. 

There we want to use socket.io, the existing connection we have set up to
basically inform all connected clients about the new post, that is the idea. 

Now for that however, we need to share that connection which we currently set up
in app.js. 

How do we get that connection out of app.js into feed.js now? 

Let's do that and continue with the set up in the next lectures. 

---