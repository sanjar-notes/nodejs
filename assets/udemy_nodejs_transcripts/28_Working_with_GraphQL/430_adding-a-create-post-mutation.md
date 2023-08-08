## 430. Adding a Create Post Mutation

<strong><em>no description</em></strong>

Now that we have users in place, let's work on posts and for now I will add
posts without a real image because the image upload is something I'll manage
differently, for a post with just title, content, some dummy text for the image
url and an attached user, you can definitely try this on your own though that
will be challenging of course but give it a try, go as far as you can and then
try to solve it together with me, I will of course now also do it with you. 

So I will start in my backend, in my schema here and I will add a new mutation,
create. 

There I expect to get some data that describes the post, we could get it all as
separate arguments or again we define an input type which I will do here and
that will be my post input data and in my post input data here, I will require
everything I need to, well create a new post and I expect that to be a title
which is a string, the content which is a string and also the image url. 

The user is something I can retrieve from the token which has to be attached at
some point anyways and the image upload is something we'll handle differently
later. 

So the post input data is in the end what I get here, so post input will be of
type post input data and I will return the created post here, remember that we
did create the post type earlier already. 

And now with that, we can actually already move on to the resolvers and add a
new resolver which I'll name create post. 

In there, I can use destructuring to extract by post input argument which I just
defined in my schema here and I do get the request as the second argument, we'll
need that later to get the user data. 

Now for now, let's simply create a dummy post with the dummy data we are able to
use right now and of course let's also validate the input. 

For validation I'll use the same approach as when we created or logged the users
in, I'll create an empty array, an empty errors array and then I'll add a couple
of if statements. 

Here I'll check if validator is empty, whoops, is empty, so if the input is
empty and I'll check that for my title. 

If that is the case or if it don't meet a minimum length requirement with
isLength for the post input title and then I configure this length with the
second argument to be a minimum of five characters long, if we have either of
these two cases, then I'll push a new object onto my errors array with a message
of title is invalid. 

Obviously again, you could be more detailed here. 

So that is my title validation, I'll then add another if check where I check the
content for exactly the same two things and that is it for now. 

Now with that in place, I'll keep my code I have up there where I have a look at
my errors length and I will copy that down here too to throw an error if we have
any validation errors. 

If we make it past this if block here, I know my input is valid and we can now
create a new post. 

For that, we'll eventually also need a user but for now, I'll ignore the user
and instead here up there, I'll import my post mongoose model from the models
folder and now we can use that to create new posts which you of course do,
whoops, not user, post by using our constructor mongoose gives us. 

Now I want to use async await again, so I'll tweak that to use this syntax here
and now down there where I create my, whoops, not user, my new post, I pass in
the title which I get from post input title, I of course also add the content
here, so post input content, the image url post input image url and for now I
won't add a creator here because I'm not able to retrieve the user yet. 

So that is my post, I can now store the created post in a new constant and I get
that by awaiting for post save to finish, here I'll then also need to add posts
to users post, later once I do also retrieve the user, for now I can just return
my response here so to say by getting all the data from the created post doc and
then I'll overwrite the ID because I can't return the mongodb object id I need
to return a string and I will overwrite createdAt and updatedAt because these
will be stored as date types, graphql does not understand that so I need to
convert that to a string too. 

So I get that from my created post, there createdAt and I need to call to ISO
string here. 

The same for updatedAt, updatedAt will be created post updatedAt to ISO string
and now with that, this is the data I want to return when a new post was added. 

Now for now I'm not checking if the user is authenticated and so on, I'll just
have this resolver added, this create post resolver for the respective mutation.


Let's try that out in graphiql first of all, so here if I reload that so that it
loads my latest definition, I can add a mutation here and that is now create
post. 

There I have my post input which is an object where I have a title, test where I
have a content, test and where I have an image url, some url and where I then
once it is created can get back the ID and the title, let's say. 

Let me click on prettify to make this a bit easier to read and now if I hit the
play button, I get invalid input which makes sense because title and content are
too short so let's make them five characters long and now I simply get an error
from the database that the creator is missing, which makes sense. 

But the general mutation is working, let's now make sure we also validate that
token which we need to send anyways and that we extract the user id and the user
therefore so that we can connect posts and users and thereafter, we'll of course
also connect to our frontend. 

---