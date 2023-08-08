## 441. Deleting Posts

<strong><em>no description</em></strong>

Let's finish the post functionality by making sure we can delete posts and as
always, feel free to do that on your own as a practice. 

Create the appropriate query or mutation and the respective resolver
functionality on your own and feel free to edit the frontend too. 

After a short pause which you can use to pause the video and try it on your own,
we'll do it together. 

Were you successful? 

Well again we start in the schema of our backend and I'll add that delete post
mutation here and I expect to get the ID of the post which should be deleted, I
will then only return a boolean that indicates whether that succeeded or not. 

This is my mutation, more interesting is the resolver for that. 

Let's go to the resolvers file here and there, I'll add delete post, I'll
retrieve the ID from the incoming data package so to say, from the arguments
object and I'll write this in the async function syntax again so that I can use
async await and again I'll start by checking the login status. 

Now obviously you could refactor this into a common function, I deliberately
have the more verbose setup here to make it really clear that we have this check
in every of these resolver functions. 

After knowing that the user is signed in, let's fetch the post we want to remove
so that we can check whether the creator of the post is the user who tries to
delete it. 

So we get the post by awaiting for post find by ID with the chosen post ID. 

Now here we can check if we don't have a post and again, this is some logic we
can copy from before and the same is true for our authorization check regarding
the quality of the creator and the logged in user. 

So I'll copy these two if statements in here to check if the post exists and
then I want to compare the creator with the logged in user. 

Now important, since I don't populate my creator field here, the creator here is
not an object with _id but creator itself is already the ID because that is how
it's stored in a post and we need to call populate to change that in the result,
we're not doing that here so we only access creator to directly get the ID of
the user who created the post. 

Now we got all the checks in place we need and after this, we want to delete the
image that belongs to that post. 

Now for that, I have that functionality in app.js here, now I will copy that and
put it into a separate folder, util where I will add a file, js file and in
there, I will just import path by requiring path and I will import the file
system by requiring that core node module. 

Now in here, I can export clear image so that we can use it in other files and I
want to use it in app.js where I already did use it in the past, there I don't
need the file system import anymore but I will add an import to my own clear
file functionality by requiring util file and then here, I use destructuring to
get that clear image function. 

So this is now using that restructured code where I moved that function into a
seperate file and in the resolver, I can now also import that, so here I also
want to import clear image by requiring and here I need to go up one level, then
util folder and then the file file. 

So now I have clear image available and now at the bottom of my resolvers in
that delete post resolver here, I will call clear image and pass my post image
url in there because that is the path of the image on my server. 

Now after this was done, I will await the result of post find by id and remove
and I'll do that for my post with that ID. 

Once this is done, I just need to make sure I remove that post from my user as
well, so for that I first of all need to get my user by awaiting user find by ID
for the user ID stored in my request object due to the auth middleware we added
earlier and on that user, I can then access the posts and pull my ID, so the ID
of the post which I just deleted and thereafter, I will await the result of user
save to save that updated user back to the database and then I will return true
because remember in my schema, I defined that I want to return a boolean. 

I could wrap this all with try catch, this part to also then return false if it
fails and that is generally something we can do on all these resolvers, I will
not do it here to keep this code a little bit more simple but in the end, that
is something you could add, important is that you here return true. 

That is the backend, let's now work on the frontend as well and let's make sure
we can trigger the deletion of the posts there. 

For that in the feed.js file, you want to go to the delete post handler and
there again, define your graphql query which has the shape you already know and
love. 

In that query here, I'll run a mutation, the delete post mutation, the ID here
is injected between double quotation marks, it's the post ID I am getting as an
argument and we have no nested object here so we couldn't even get any nested or
detailed data, we only get true or false. 

That is my query and then here, again I'll send this request
localhost8080/graphql, the method as always will be a post request, we add our
token, we also set the content type to application json and of course we need to
add our query expression as a body by using json stringify and passing our
graphql query in there. 

We don't handle errors like that as you learned, instead we do it on the parsed
response because there that is where we would have an errors object if there are
any errors, so I'll copy that code from above and then move that in here to
check if there is an errors object which means something did go wrong and then
deleting the post would fail and that is it. 

Now let's save that as well as the backend code and let's click on delete here
and that is looking good and I can carefully delete all my data until there is
only one doc left and if I now refresh my posts, only one doc is there and in
users, that user still has two docs or two posts but that is probably related to
something I deleted earlier behind the scenes which is also the reason why I
have two images here. 

To validate that everything does work, let's delete that and on that user, let's
manually delete the two array elements, clear all the posts as I mentioned,
clear all the images here and now reload, we have no posts now. 

Let's create a duck and let's give it that duck image and some content. 

Let's also create another item, a cup and give that the cup image here, you can
now view the cup, we see it, we also see the duck here. 

Now let me delete the duck, the cup is still there, only one image, this is
looking good. 

If I inspect my users, only one item, the cup, so that now makes perfect sense. 

And now let me also try logging in with a different user who didn't create that
and there deleting indeed does not work. 

So we have all that in place, let's now finish this all up by making sure we can
view and edit our user status and again this is a great challenge for you. 

---