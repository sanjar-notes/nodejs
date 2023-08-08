## 432. Sending the "Create Post" Query

<strong><em>no description</em></strong>

On the frontend in the finish edit handler function, in the feed.js file, there
I'll ignore the image upload for now, I want to now reach my graphql endpoint
and create a new user. 

For that first of all I will get rid of this code because I will not send this
request to different urls anymore and I'll not use different methods, it's
always the same url and the same method, localhost8080 graphql and the method
simply is post. 

The body is also not my form data but here I'll create a new query with let
because this will change when we edit the post later and my query here is
graphql query, my query here is defined as before, query and then this is a
multi-line string with back ticks, it then actually is a mutation and the
mutation is create post. 

To that I need to send the data I did on my graphiql user interface, so actually
I can copy that here, move that over there and now replace these hardcoded
values with dynamic values. 

So here for the title I will pass post data title, for the content I will pass
post data content and for the image I'll keep that to some url for now until we
have a real image. 

I get back the ID and title, now let me first of all send this in a stringified
version, the graphql query and then let's do something with the response. 

Now again this way of handling it will not really work, so let's instead copy
the code we use an app.js where I check for errors on the extracted response
body and therefore I do it here, then I log my response data and you see I'm
interested in the ID title, content, creator and createdAt here, so I should
actually retrieve all of that. 

So in my query I get the ID, title, content, image url, creator and createdAt
date. 

By the way, the creator if you have a look at my schema is again a more complex
object, it's a user object. 

So for the creator, we need to be more specific and that is the cool thing about
graphql, we can really drill into the data and here let's say I'm only
interested in the name and indeed I am, I don't care about the ID or email. 

In this scenario here, I want the name so that I can render that onto the screen
next to my posts and this shows the power of graphql really well, we get exactly
the data we need. 

Well now with that, we send the post request. 

Here for extracting the data, we'll have some problems but first of all let's
focus on what we log to the console and see if that works. 

So back to our application, I am still logged in because I have a valid token
and I do still attach this token by the way here but we also need another
header, we need to add the content type and set that to application json, that
is required so make sure you add this and now back in the application, click new
post, add a duck, you have to choose the image here even though it's not
uploaded otherwise you can't submit and then I'll add my lovely duck. 

And here I get an error which was expected but I also see a console log which
actually doesn't look too bad. 

I do have all the data I entered and we can now have a look at mongodb compass
and there if I refresh this and look into my post collection, I indeed see a
post with the data I entered, with that creator ending with aa1 and if I have a
look at my users, I see that it's that user and there on the posts, I am
unfortunately missing my post. 

So that is one thing I will need to tweak but the rest is already working really
well. 

Now let's make sure we add that post here too and then of course let's make sure
we extract the data on the frontend correctly so that we also render that post. 

For that by the way, we'll also have to make sure we load all posts initially
though. 

---