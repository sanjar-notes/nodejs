## 383. Updating Posts

<strong><em>no description</em></strong>

We're making very good progress, we're able to create posts, view posts, view a
single post, upload files, validate content, all great. 

Now what is missing? 

We want to be able to edit posts, we want to be able to delete posts and
authentication and users and connecting posts to users, this is all missing, now
let's continue with editing and deleting posts before we dive into the
authentication and user related things. 

So for that, let's go to our feed routes in our node rest API project and there,
I'll add a new route, I want to be able to edit posts now and for that I will
use a new http method which we haven't used before. 

Editing a post essentially is like replacing it, replacing the old post with a
new one, we'll keep the old ID but that is it. 

Since we'll replace a resource, I'll use the put method here and the put method
is one you learned about in the last module but which we haven't used before
because with normal browser forms, you're not able to send it, through
asynchronous requests triggered by javascript you are however. 

Now we need a url here and the url will be /post and then also the ID of the
post encoded in the url, so colon post ID. 

Now we also need a controller action to handle that, the important thing about
put requests and the same is true for patch requests by the way is that they
also have a request body, just like post requests but you can also have
parameters in the url, well that would have been the case for post requests too
by the way but the important thing is we have a body for these request, we can
add a request body and that will hold the actual post data that I want to well
use and that I want to use to replace my existing post, so let's work on the
controller now. 

In the feed controller at the bottom, I'll add a new action and I'll name it
update host, the name is up to you but this is what we'll do, we'll update the
post in there, this is the function and in here, in this function, I can first
of all retrieve my post ID from my request params because we just added it
there, right. 

In my route, host ID is a parameter which of course I can extract. 

Now when updating a post I also will extract my title, so request body title, I
will extract my content, request body content and I want to extract my file, my
image url, however for that url we have two options when updating. 

The first option is and that will be my default, that image url is part of the
incoming request and it's just some text in the request body. 

That would be the case if no new file was added, if no new file was picked, then
my frontend code has all the logic to take the existing url and keep that but we
might have picked a file and in this case request file will be set and I can now
set image url equal to request file path, this is the alternative. 

After all of this, at least one of the two should be set, so if image url is not
set at this point because we were not able to extract it from there and we did
not make it into this if statement, then we should throw an error so here I will
prepare a new error, no file picked, I'll set my status code to 422 and I will
throw that error here. 

So that's my first little piece of validation, we'll add more validation of
course, normally we should have an image url however. 

Now I have one little mistake here by the way, this should be image here, what I
retrieve from the frontend and we need to tweak our frontend a little bit too. 

There in feed.js, in source pages feed, feed.js, when we load all posts, so in
load posts, that is when we basically load to post data from the server
including our image url. 

Now we then store the post here in the frontend so that the rest of the react
application, the rest of the code I prepared can handle that, we need to tweak
this line a little bit. 

There you should access res data posts but we have to map this, which is a
default javascript method into a different kind of array or every element has to
be changed a little bit. 

Map takes a function that executes on every element in the array and it gets the
element which in our case is a post as an argument and then we return,  well the
updated version of that object, so I return a new object here where I will use
the spread operator to get all the properties of my post object and then I'll
add an image path key here which is post.imageurl . 

Now image url here is referring to the property I am storing on my server side,
there we are restoring a path to an image in the image url key, you could have
name this differently, if you named it differently here, you would have to name
it differently here. 

Now I'm storing the original path here because when I'm viewing a single post
for example, I do extract that image url and I append my url to the domain. 

Now the path should be well just a path without a domain because I'm keeping
that here and this will get reused later when we edit this through this edit
modal, behind the scenes this path will be stored and if I don't choose a new
file here, this path will be submitted with my edited post and there, the path
will be stored in a property named image, you can see that in the components,
the feed edit component under feed, feed edit, there you could see all the
internals, if you know a little bit of react you can see the internals and see
that I'm extracting my image path and I'm storing it in an image key ultimately.


I don't want to dive too deep into react but this is what I'm doing on the
frontend and this was one adjustment that was required and on the server side,
we can now extract our image here from the body and either this is set or we
selected a new file in which case a file will be found. 

So now we can continue working on update post and we can continue working by
first of all adding more validation which we do in our routes of course. 

Well there I will copy that array from my post route and I will add it here, so
for my put route I also want to validate the title, by the way we should switch
that back to 5 characters of length for both posting and putting. 

So I will validate these two things, I'll not validate my image because that is
done directly in the controller action and I don't need to do any other
validations for now. 

So with that added, let's go back to the controller and let's copy the
validation logic from the post route where I gather all my errors and then I
check for errors not being empty and then I would throw an error. 

So before I extract anything else, I'll check these things in update post,
whether I have any errors and if I have, I'll throw an error. 

If I don't have errors, I continue, check the file and if we make it down here,
so after all these if statements, then I know I have valid data and now we can
update it in the database. 

To update it in the database, I will find my post by ID for the post ID which I
extracted from the url, then I can do something or we might have an error, if we
have an error, I'll reuse that error handling logic you find in other places, in
other actions, so I'll add my status code in the next, the error. 

If I am successful, I know we have no database error, I still need to check if
post is undefined which means we didn't find a post, in which case I will also
throw an error just as we did it for getting a single post, I can copy that
logic and again if you are copying a lot of code, you might of course also
refactor that, I like the more verbose approach to make sure we all understand
each step we take in each action creator and if we make it past this if check
inside of the then block, then we found a post and then I want to update the
post of course. 

So here I'll set my post title equal to the title I extracted, I'll set my post
image url equal to the image url I extracted and I'll set my post content equal
to the content I extracted and then I can return post save here to save that
updated post back to the database, overriding the old post but keeping the old
ID and then here we get the result of that save operation and here I want to
return a response with a status code of 200. 

We didn't create a new resource so it's not 201, with some json code or some
json data where I say post updated maybe and where I return that updated post
which is stored in the result in the end. 

So this is now the updating logic here, there is one more thing we can add and
that is some logic to delete the image. 

For that I'll add a little helper function down there, clear image which is a
function that accepts a file path as an argument and then I will use the file
system package nodejs offers, so I'll import it at the top by requiring fs and
with that imported in that clear image function here, I'll first of all
construct my file path for which I'll also import the path package by the way so
let's import that at the top too and now the file path can be constructed by
joining dir name, then going up one folder because we're running this inside of
the controllers folder which is not where we will find images, so we should go
up one folder to be in the root folder and then we look for whatever file path
we got here. 

So images and then the image name would be the case in our application and I can
then use the unlink function to delete that file by passing the file path to it
and we can also log any error message and I want to trigger that clear image
function when ever I uploaded a new image. 

So inside of my update post action creator, right before I save my updated post
maybe, I'll check if my image url which is the path to the image, if that is not
equal to post image url. 

So to the image url I stored in my post before, if they're not equal it
obviously changed, so I uploaded a new file and that is where I will execute
clear image and pass the old image url, so the old path as an argument. 

Now with that, we got all in place here in the controller, now we can go to the
route and there we still need to register that controller action on the put
route, so on the feed controller I access update post here, that's one important
step and on the frontend so in the react code, we also need to do something. 

There in source feed, feed.js in the finish edit handler function there, we need
to adjust our code now. 

There we set up our form data which is correct for updating as well but if we
are in edit mode which will be the case if we make it inside this if statement
due to the logic I configured on the frontend, we want to send a request to
localhost 8080 /feed/post/ and now we need the post ID which we get from this
state edit post._id, that is where it will be stored in my react app and I'll
set the method to put because we created a put route. 

Now with that, we can save all that and try that out and hopefully not get an
error. 

Let's edit the second doc here and add a couple of exclamation marks in both
title and content. 

Let's not choose a new file, it's looking good, I see my exclamation marks
there, I see them in the content as well. 

Here I get a confirmation message that should looks good and on the backend, I
still only have one image, well that makes sense because I didn't replace it
anyways. 

Let's now replace it by editing that same doc again, let's not change title and
content but choose a different file, maybe that coffee mug, click accept, post
updated is looking good, it's not a doc any more so the title is not correct but
on the backend, we only have the coffee mug now, so updating seems to work and
of course we can confirm this by viewing that image as well, there we also see
all the updated data. 

So that is working and with that, only deleting is missing before we can finally
start working on authentication. 

---