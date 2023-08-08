## 380. Fetching a Single Post

<strong><em>no description</em></strong>

So time to add a new route in the feed.js file in the routes folder. 

There I will add a new get route and that will be a route for a single post. 

So the route is get/post and then we need a dynamic parameter, /postID for
example because we'll encode the ID of the post we want to fetch in the url. 

So this is my path, now we need a fitting controller action, so let's go to the
feed controller and in there, I'll export by get post controller action with
request response next and here first of all, let's extract the post ID from the
incoming request params. 

So there I can get my post ID, post ID here, this property I'm trying to access
has to match exactly the name I assign in my route, so post ID here after the
colon. 

So now I'm extracting, whoops, I'm extracting that post ID here, now we have to
find a post with that ID in the database. 

So let's use our post model and use the find by id method to find a post with
this post ID. 

We then have a then block or a catch block depending on whether this fails or
not. 

In the catch block, I'll use that same logic as I used for creating a post, I
check if we have an error status code, if not I add it and otherwise I just next
my error and yes you could refactor into a single function which you then always
use. 

So here I have this error handling code, in the then block here, I will get my
post and first of all I'll check if this is undefined, so if this is not a
true-ish value. 

If it is, I know that no post was found and then I'll actually throw a new
error, so I'll create a new error object, could not find post, I'll set the
status code to 404 because that is a not found error and now I'll throw the
error. 

This can be confusing because I'm inside of then and you learned that you should
use next in there but if you throw an error inside of a then block, the next
catch block will be reached and that error will be passed as an error to the
catch block. 

So all I do with throwing is I end up in this function and there I do indeed
next the error, so I just always use that function, that's all I'm doing, I
still throw an error if I can't find the post. 

If I do find it, I will return a response with a status code of 200 which shows
that it was a success or I do return some json data with some message, you don't
have to set the message by the way, this is purely optional of course, where I
say post fetched and of course my post like this, so I'm returning the post I'm
fetching here as a property post in that object. 

So now we have that controller action in place, now if I go back to my routes I
can assign that controller to that route here, so feed controller get post is
the action I want to use and this will not work however because in my frontend,
I fetch the wrong post, so I fetch some dummy data because in my feed controller
get post, I'm not using the database, I'm instead just returning dummy data. 

Now since we are using a database now, since we have added a database, we should
of course fetch data from there as well. 

So for that, let me use post find to find all posts and then I have an error or
a success case, if I have an error, I'll use that same logic I use down there to
add a status code if it does not exist and then next the error, if I succeed I
get some posts here however. 

And now I want to return these posts, so I will send a response with a status
code of 200 where I send some json data and that json data will be an object
where again I will add a message which you don't have to, fetched posts
successfully and most importantly I'll add my posts of course and the posts I
add here are the posts I fetched with posts find, so these posts. 

Now we can get rid of that response down there with our dummy response,
re-format this and now we have this logic in place to fetch the actual posts we
have in the database. 

If we now save that and we go back to the frontend and reload, it should load
that post. 

Does that work? 

Now of course we will now want to be able to click on view and see that single
post for which we already added the route. 

We just need to adjust our frontend code, so the react code to load that single
post and you do that in the source pages feed single post folder in the
singlepost.js file, in there you have componentDidMount which executes when this
page loads essentially where we extract the post ID from the url in the frontend
and now we just need to target the right url here which is of course http
localhost 8080 /feed /post/ and then that post ID. 

With that we have a get request that should get us our post. 

If you now save that and you click on view, you should load your post here,
however the image is not displayed. 

The reason for that is that we're looking for the wrong url or that we're not
using the image at all to be precise. 

In the frontend, in the same componentDidMount function you just worked in, in
this set state block here, you should add an image key and it has to be named
image because that is a key I'm looking for in that frontend application in the
other code which I prepared and there you want to also define that url to your
server, so localhost8080/ and then use res data. 

post, accessing the response data, there the post property which we do use to
store our post in, in get post we have that post property here which holds our
post. 

So this is what I am accessing now in the frontend and there, image url, that is
the key name, how it is stored in the database, add a comma thereafter and save
that. 

And now this page should automatically reload and you should see that duck. 

Of course we didn't upload that, I prepared it but at least you see it. 

Now you can go back to the feed and see your posts here, we'll get off that
error message later too by the way. 

So with that, we got this in place, let's now work on image upload next. 

---