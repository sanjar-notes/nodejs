## 433. Fixing a Bug & Adding New Posts Correctly

<strong><em>no description</em></strong>

Now let's first of all fix the fact that our user does not have the post added
to his posts array, the reason for that is that I do push the post here but of
course I forgot one important thing, I never saved that change. 

I need to call users save here and I'm not interested in the result but I
certainly want to await it nonetheless so that I only return after this has been
done. 

So this is one important change and this is only one change we need though, we
can quickly validate whether it works however by going to posts, let's delete
that post which we added here and now let's go back to our frontend, add a new
post, another duck, choose an image even though it's not getting used. 

Let's add some content and click accept, we still get that error but if we go
back to compass, we have a look at our users, for the first user, we now also
see that post here. 

So that is now working and now let's make sure we also extract the data
correctly on the frontend and that we then also load all posts so that we really
can see them there. 

Now for the data extraction, we see that this is the data in the format we get
it back, an object with a data field, then the name of our query and then in
another nested object, the fields for that query and this is exactly how we have
to retrieve our data. 

So in our react code in feed.js here, when I create my post there and I try to
access response data post and this will not work, I have to access res data data
create post, so here its res data data create post ID and that is the case for
all these places, whoops, where I do access fields on my created post. 

Now with that, we should not get an error message anymore when I create a new
post at least, so let's try that out, a cup, let's choose the cup image though
it does not matter, we're not uploading it, it accept and I don't get that error
anymore. 

So extracting the data works, now let's focus on adding a query that allows us
to get our posts so that we can also render them here. 

This is also a great practice for you, we'll do together in the next lecture,
try fetching your posts on your own, try creating that query on the backend on
your own. 

You don't need to tweak the frontend code, if you can do that, perfect, we'll do
it together otherwise but add your graphql query and test it with the graphiql
interface. 

---