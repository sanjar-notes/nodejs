## 437. Uploading Images

<strong><em>no description</em></strong>

How does uploading data work now? 

The thing is graphql only works with json data, you can find a couple of
articles, third party packages that help you with getting data through graphql
but in the end, one of the cleanest solutions is to use a classic endpoint like
a rest endpoint where you send your image to and then let that endpoint store
the image and return the path to the image and then send another request with
that path to the image and your other data to your graphql endpoint and this is
the solution I'll implement here. 

I'll implement it in app.js because you could outsource this into a separate
file but it'll be the only other route we add here and there, I'll register a
new route on my app for incoming put requests because I plan to send that image
with a put request to slash let's say post image, you can name this path however
you want. 

There we have our traditional middleware function, I hope you still know that
even though we haven't used it in the last lectures and there I'll first of all
check if we don't have a file. 

Now how can I check that? 

Well I still have multer in place, we added that in the rest API module and
multer is the package which takes our multipart form data requests and extracts
a file and stores it in the image folder and I still have that in place. 

So all my files still will be extracted and multer then populates the file
object with information about the extracted file. 

Now if this is not set, then I'll just return a response here with a status of
200 and a message where I say no file provided. 

You could set an error code here but actually this scenario is fine for me as
you will see when we later edit a post because there we might or might not add a
new image, maybe we stick to the old one, maybe we did choose a new one and then
this is one way of handling both cases. 

If we do have a request file, we can get some data from it though and of course
we want a clear and existing image if there is one. 

For that, I'll create a new function here or actually I have that function in
the feed.js controller already, I can copy that from there, the clear image
function at the bottom of the feed.js file. 

I'll move that into app.js, this depends on the fs package, on the path package,
the path module, path is already imported, now I'll also import fs here and now
with that all imported, back in our put request here, I'll check for the
existence of a body field which is named old path which simply means that an old
path was passed with the incoming request in which case I want to clear my old
image and I'll pass in the old path because then we added a new image. 

We can be certain about that after this if check and then we should also have an
old path which we delete so that we don't keep the old image and the new image,
instead we delete the old image here and then only keep the new image which was
stored by multer. 

And then at the end here, I will return a response with a status code of 201 and
that differentiates it from this response and here I will add some json data,
let's say a message, file stored but more importantly, I'll add a file path or
however you want to name it which is request file path and this is the path
where multer stored the image and this is the path we can then use in the
frontend. 

With this added on the backend, we can now work on the frontend to use this rest
API endpoint and this also shows you that you can use rest and graphql concepts
together, it's not like a hard decision you have to make, you can use the best
for a given problem. 

So now we can use that on the frontend and we want to use it in this finish edit
handler, so in the feed.js file of the react app, in the finish edit handler,
there I'm preparing some form data and this form data does not get a title and
content anymore but it would still get the image. 

Additionally though, I also want to check if we are in edit mode, so if this
state edit post if that is true and then I will append the old path field which
is this state edit post which is the post we're currently editing, image path. 

This is a field we're setting when we're loading all posts, there when we load
all posts, we also set the image path and this is a field which we therefore
also should set when we edit our posts. 

So there when I create a new post, I should also add image path here and get
that from create post, that should be my image url which I get there and that is
also something I need to request therefore, image url is something I do request
here so I do have it available. 

So I'm setting this image path, I have that available, this will be the path of
the well the old image on the server and now with that, I have my form data
setup. 

Now before I send my graphql query, I will therefore send another query to http
localhost 8080 but there to /postimage, so to this new endpoint I defined and
the method here will be put because on my backend here, I simply defined this to
handle put requests, you could of course also argue to use post but since I'll
replace the old image, put makes a lot of sense, I'll then add my headers. 

Now regarding authorization here, we want to make sure that our auth middleware
actually runs first on the server so that we know if the user is authenticated
and if isAuth is false, then we can certainly throw a new error here, not
authenticated so that we protect this route as well. 

So now on the frontend, we need to add our authorization header and now we'll
just copy the headers from my graphql request because the headers actually are
the same and the body is now here, my form data. 

This fetch request will be made first, then after it has been made, I'll get
back a response, some response data where I'll parse the body and thereafter
I'll have my file response data, you can name this however you want and in here,
I now can extract the image url by accessing file response data and there, file
path because in my endpoint, I am setting this file path key here and I can now
use that in the graphql query. 

So now let me grab all that graphql code here, this code up to the then block,
cut it and move it into this then block and then remove this semi-colon and
chain this then block here, I just need to return this fetch call so that the
next then block refers to the result of this fetch block here. 

So now I do have my image url, now I just need to pass it here for my graphql
query image url and now we should have a setup where we are able for now to at
least create new posts, editing is something we'll work on later. 

So let's try that out, let's try creating a new post and first of all on the
server, I'll clear all the images in the images folder so that we can tell
whether this works or not, so back here I need to login again, let's quickly do
that and let's create a new duck, a new post but it can be a duck, a duck with
an image hopefully. 

Let's choose our duck.jpg, this is a lovely duck again, accept and I get this
error regarding payload too large and this is actually coming from an error on
my side that fetch request here where I send the post image, I should not set
the content type to application json otherwise it will be parsed as json data
and that does not work for my binary data here. 

So after removing this header, let's try this again with another duck here, add
that image, so lovely, accept this and now it uploads this first and we can
prove that by looking into images, here is our duck image. 

So this works and it still creates that post which we can see here. 

Next challenge is to make sure that we can click that view button and view the
detail page for one post and this again is a challenge for you. 

Implement something, some schema or a query in the schema of your graphql API
and add a resolver that takes the ID of a post and loads that post. 

You can then work on the frontend too if you feel bold otherwise focus on the
backend. 

We'll do it together in the next lecture. 

---