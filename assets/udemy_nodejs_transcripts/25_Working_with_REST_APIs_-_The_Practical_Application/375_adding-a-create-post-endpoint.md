## 375. Adding a Create Post Endpoint

<strong><em>no description</em></strong>

Let's make sure we can create new posts so that this new post button does not
only open the modal but we can actually add a new post, for now without the
image upload. 

So let me go back to my rest API and there we already have a create post route
of course so we can continue working on that. 

We expect the title and a content there and for now this is the only data which
I will really need to worry about because well as I just said, we'll not worry
about the image for now. 

You can pick an image here but ultimately even though it's previewed here, it
will not be uploaded. 

But it does not matter, we can implement this in a way that at least the title
and the content is uploaded. 

For this we already got our route in place, a post route to feed post and there,
we then extract our title and content and we, well for now basically echo back
that message. 

Let's try that and let's go to our frontend application so to the react code and
in there, let's simply go to the feed.js file and there you should find a finish
edit handler function. 

This is the function which is responsible for handling the case that we clicked
on except here once we entered a valid title and content, by the way here I also
got validation in place, frontend validation which is not the matter of course
because it's not related to node at all, it's just a user experience thing that
we use browser side javascript to validate the input right away, you can learn
more about that in my react course if you want. 

Still worth noting that we have some validation in place here, not validation on
the server though. 

So if I now click accept, I want to reach my /feed/postroute, for that here we
have to edit this url. 

This url here will actually be required later when we start editing posts, for
now we want to create a new one, so here the url will be http localhost 8080, so
our backend url /feed/post, this is the route we set up on the backend. 

Here we send a fetch request to that url and we need to configure that request
because it will be a post request. 

So the method here can be post but actually I'll write this in a more flexible
way too because when we later edit this, we'll use a different method, so here I
will create a new variable method which I'll set to post which we then later
could override in here. 

So here I'll not hardcode posts down there but instead use my method variable. 

I will also need to add a body, the data which I want to set and that has to be
json data so I will use json stringify to convert a javascript object to json
and then I pass a javascript object here and this javascript object in the end
should hold the code which I want to, well send to my backend. 

In this object for now, I simply want to set my title and that can be extracted
from post data, an argument I receive in this function, so post data will hold
the data the user entered, post data title and then here also the content to
post data content, so this is again what we add in the react application. 

Last but not least to send this request in a way that the server understands it,
we need to add some headers here where we set the right content type, so here
I'll set content type to application json to inform the server that I do indeed
send some json data. 

So with that, I'm targeting the right url and I'm sending json data and I'm
sending a title and a content and this should be everything I need on the
server. 

So let's save this and it should reload automatically as long as you keep npm
start running here and therefore, well it reloaded the app here and let's create
a new post, the title has to be at least five characters long such so as the
content, choose a file otherwise you're not allowed to submit this even though
the file is not getting uploaded right now and click accept. 

Now you will run into an error here which is related to the frontend missing
some crucial data it needs to update everything correctly. 

However let's go back one step and let's actually console log res data here,
still in that finish edit handler, just in the then block after fetching and
save again. 

The app will reload and you can enter something into that new post model again,
testing again and hit accept again and you'll get that same error but before
that error, you'll see a log which actually proves that on the rest API,
everything worked correctly. 

You get back that post created successfully message and the post with the data
you entered. 

The error is simply stemming from the fact that on the server, we're not doing
everything we expect it to do because we're not creating or we're not attaching
a user, we're not creating a date and so on. 

These are all things we can fix though by going back to our controller on the
server and there when we create a new post or when we echo back that post, first
of all it should have an _id not an ID, it should also have a creator field
which is again a javascript object with a name of your choice and later this
will not be dummy data anymore but real data, so we add this creator and we
should add a created add field and that created add field is simply a new date. 

And now with that being echoed back, if we save that server side code and we
reload the frontend application, we can test this one more time, click accept
and now we don't get an error instead we see our post there. 

So now we indeed do create our data on the server or at least we fake to do so
and we return that back to the client where we can now render it. 

Now editing will not work though we can select it for editing at least, deleting
will also not work and viewing will neither but we got our basic flow set up. 

Now since we're creating a new post here, what is missing on the server though,
at least two things are missing and what is missing? 

Well validation, server side validation, we only got client side validation but
that can always be tricked because users can see your browser side javascript
code, they could disable it, they could basically find ways around that so it's
not a safe mechanism, it's only meant to improve user experience. 

So we need to validate on the server and of course we want to store the data in
a real database, so we should add mongodb or SQL solution again and that is what
we'll do over the next lectures. 

---