## 416. Sorting Correctly

<strong><em>no description</em></strong>

So now we also manage updating via socket.io, there's one tiny thing you might
be wondering about. 

If we create a new post, like a duck again where I add the image and some
content, it does show up at the top but once I reload, it's actually at the
bottom of the list. 

Well this is simply due to how I sort on the backend when I get all posts here
in our feed.js controller get posts, there we simply have to sort by createdAt
date in a descending way. 

And now by doing that, if I reload on the frontend, our latest posts come first
there too. 

So that's just some tiny cosmetics which better align with the rest of our
application of course, it doesn't affect the way we use socket.io though of
course. 

---