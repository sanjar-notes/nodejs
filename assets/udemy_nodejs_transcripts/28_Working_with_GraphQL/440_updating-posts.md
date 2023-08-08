## 440. Updating Posts

<strong><em>no description</em></strong>

Now that we can load a single post, let's make sure we can also edit a post and
as always, that journey starts on the backend. 

There in the schema, we want to add a new mutation because obviously editing a
post is a mutation, I'll name it update post and I expect to get the ID of the
post I want to edit and then some post input which is my post input data, so the
exact same data I expected to get for creating a new post. 

As a result I will return the updated post. 

So this is my schema, now onto the resolvers where I will add update post as an
async function again where I get my arguments, I will have the ID and the post
input and the request object. 

So this is my update post resolver, in there I first of all want to check the
authentication status and throw an error if the user has not authenticated hence
we can copy the code from our other resolver functions where we had a similar
check and then I'll first of all get my post by using await and post find by id
and using that ID I extract as an argument. 

I'll also populate that with the creator so that we have the full user data when
we return the update post, then I'll check if we don't find a post and I can
copy that check from up there to return an error in that case and if we do have
a post, well then I want to check if the user who tries to edit it is the user
who created it and for that, I'll check if post creator_id toString, if that is
equal to request user ID and that also convert it to a string. 

If these two match, then I know this user is the creator, if they don't match,
so if I add an exclamation mark here, then know someone tries to edit the post
who is not authorized to do so. 

And in this case, I'll again create an error, not authorized, could be the error
message we throw, I'll add a code of 403 and I'll throw that error and then we
can continue. 

If we are the right user however, we can now edit the post and set the title
equal to post input title, we could now also add validation by the way and we
should, so I can scroll up to my create post function and grab that validation
logic, all the logic beginning from the empty array being set up to the errors
being checked and that is something I also want to do before I start editing my
post title and so on but now here I know that the input is valid. 

So now I will edit my title, I will edit my content and I will now also edit my
image url if it changed and that is not guaranteed because the user did not
select a new image, the image will not have changed. 

So I'll check if post image image url is unequal to undefined and now this has
to be checked against a text because it will be converted to text, by the way
I'm sending it on the frontend. 

So if this is undefined, then I will continue but if it is not undefined, then
I'll also override the image url with the new image url of course, otherwise I
will not touch the image url and then I'll have my updated post by awaiting for
post save and I will then return my updated post here or some data. 

I will return my updated post doc data and again replace the ID with updated
post ID toString and the same for the dates, createdAt will be replaced with
updated post createdAt to ISO string and updatedAt will be replaced with updated
post updatedAt to ISO string, so this is the response I want to send back to my
client here. 

With that we get a resolver in place, we hopefully get everything in place we
need, let's now go on to our react application and there in feed.js, we need to
find finish edit handler. 

So if we scroll down, in this function, in the finish edit handler function, we
will always send our image to that endpoint, though of course it could be the
case that there is no image to append if no new image was chosen but that will
be fine, we do handle that scenario in our endpoint right, in post image, we
check for the existence of a file and we send a response if no file was
provided. 

So thereafter here we continue and we'll have a file path though that file path
might very well be undefined and that is why in my graphql API, I check for it
being undefined. 

We could handle this in different ways of course, we could alternatively simply
keep the old file path here then if this is undefined but I will go with this
approach and then we send the graphql query. 

Now of course it will not always go to create post though, it might also be that
we edit a post. 

So I'll check if this state edit post is true-ish which means we are editing and
then I'll set graphql query to a different query, so to an object where my query
then looks differently. 

I will copy this query in general so I'll copy all the code between my opening
and closing back ticks, like this but of course I'm targeting update post here
and not create post, so I'm targeting this mutation here and there, I also need
to pass in different data. 

I need to pass in my ID which I get from this state edit post_id, I still pass
in the post input as before, that did not change and I still want to get the
same data back, so that also does not change. 

Then we send that request and in the handler of the request, I already have some
logic that should handle this correctly if we are updating. 

So let's save that all and let's give it a try, let's reload and let's edit
another duck and add a couple of exclamation marks without adding a new image
and I get an error here. 

In general though, it looks like it worked, I have my exclamation marks here and
the image, the old one is also still there, I can also still view that and here
I see the change too. 

Now regarding that error, well that is related to how we extract data from the
response, we access create post but of course if we send an update post request,
then this field in which our response data is stored will be named update post
and not create post. 

Therefore here and we can by the way validate this here, it's stored in update
post. 

Therefore what we can do is we can add a new variable, response data field or
whatever you want to name it and by default that should be create post because
creating a post also is our default query up there. 

But then I'll add an if check and I'll see if this state edit post is true-ish
in which case the data field where I want to extract the data will be update
post and now we just need to use that variable here to dynamically retrieve our
data and we can do that by selecting all these create post instances here with
the first dot and replace them with square brackets where we pass in res data
field and this will now use the value inside of res data field to access, well
property with the name of that value on our data object. 

And now if we reload, we should be able to remove the exclamation marks and try
out choosing a cup as an image here, accept, no error and we see the cup here
too. 

So this all seems to work, the status and deleting of posts are the remaining
things that don't work. 

---