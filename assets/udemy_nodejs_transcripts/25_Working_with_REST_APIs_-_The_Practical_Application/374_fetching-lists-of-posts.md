## 374. Fetching Lists of Posts

<strong><em>no description</em></strong>

So let's start working on the rest API again and for that I'll run npm start in
my rest API nodejs project too and that is also the reason why I'm using
different ports by the way. 

Here I'm starting the application on port 8080, my frontend application
automatically takes port 3000 and this simulates that these two ends of my
application are served by different servers in the end which is a pretty common
scenario since frontend only applications like react can be served on so-called
static hosts which are optimized for applications that only consist of html,
javascript and css and hence you might indeed have two different servers even if
you created both the backend and the frontend. 

So we have different ports and therefore we have different domains and therefore
we definitely need our course headers otherwise nothing would work and with
that, we can now start working on our feed routes. 

We actually got two routes already, /posts and /post for creating a new post and
for getting existing posts and now let's add some logic so to our controller
actions to actually return something useful and to enable the user to create new
posts. 

Let's maybe start with getting posts because that would allow us see at least
some dummy data, so that is something useful. 

For that in get posts, we actually already return a list of dummy data posts,
each post has a title and some content. 

Now it's of course always up to you how you want your data to look like in an
application. 

In this application because my frontend also expects it, I want to have a post
which in the end consists of a title which has a user attached to it, a creator
or an author which has a creation date which has an image and which has some
content. 

This is what I want to output in my frontend so the data we store on the server
should have all these fields in the end. 

Now we don't have to start with the full package though, I already have a title
and content here, now let's maybe add some image url here and for that I'll
create a new images folder and for the moment I will just copy an image into
that folder, later we'll of course add image upload. 

I'll copy in my good old duck image which I used before in the course and here
it is, the lovely duck.jpg and I want to serve that duck. 

So here in image url I will actually provide images/duck.jpg as a path because
that is my local path on the server here. 

It's missing my domain and so on, we'll have to attach this on the frontend but
this is now a post as I could serve it. 

If I now save this, we can actually fetch that data with a get request to
localhost 8080/feed because that is what we have as a filter to reach the feed
routes, so /feed/posts. 

Now let's try that out in our frontend application, there we fetch our posts in
a feed.js file in the source pages feed folder, in there you should find a load
posts function. 

Load posts is a function that is called by the react code and so on in the end
and what we do here is I also support pagination which we'll add later, for now
I just want to reach out to my url which is http localhost 8080, written like
this and then /feed/posts like this. 

So this route I just talked about in the rest API. 

This should fetch all these posts, then here I just check if the status code is
not equal to 200 which would mean that something went wrong and then I throw a
new error which is handled in your react application otherwise I extract my body
and then here, I have my body and I use some react logic to load that body in
the end and to hopefully display it. 

If I save that and I go back to my application, I'll get an error regarding the
name, the author name which is missing, I'm not supporting users yet so this
will be a problem for the moment and we'll also get an error regarding the date
eventually. 

So to avoid this, we should go back to our controller and add some dummy data
for this too. 

Let's add a creator object because that is what I'll be looking for in my react
code which should be an object with a name where you can enter any name you
want, later we'll of course connect this to a real user in the database and
let's also add a date and here you can simply create a new date with, well new
date like this. 

Last but not least, you also want to add some ID and that should be _id because
I'll be looking for _id in the frontend code in the react application because
later we'll use mongoose again here and that of course or mongodb in general and
that of course simply adds IDs with _id, so here you can enter any ID you want. 

Now if you save that updated controller code and the server therefore restarts,
you can reload and you'll still get that error which is related to our status,
our user status which we still can't fetch but if you simply click that away,
you see that first post here and that is looking better than before. 

The invalid date is a problem because actually the field should be named
createdAt, not date, there was a tiny mistake on my side, on the server it
should be createdAt. 

With that if you reload, you'll see this post. 

So fetching posts works, of course it's just dummy data though. 

To work with real data, I want to be able to create new posts by clicking new
post, so that is something we can add as a next step. 

---