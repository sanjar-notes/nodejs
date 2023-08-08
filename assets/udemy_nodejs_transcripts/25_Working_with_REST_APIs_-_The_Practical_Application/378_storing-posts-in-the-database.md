## 378. Storing Posts in the Database

<strong><em>no description</em></strong>

Well speaking of that, let's now use that model. 

We're exporting it here, let's now use it in the feed controller. 

There we first of all need to import it, so here I'll import post by requiring
it from my models folder from the post file and now we can use that post model
in create post after we validated the input here. 

There I will create a new post with my post model as a constructor, we pass a
javascript object and there we define basically what we do down there, so we can
cut that and move it up here, I don't need to set createdAt because mongoose
will do that for me thanks to that timestamps option we set here and of course I
don't need to set _id because mongoose will create that for me as well. 

Title and content should be passed and the creator as well for the moment. 

So now you'll learn that we can just call save on the model to save it to the
database and this will give us a promise or a promise-like object where we can
catch any errors and here I will log the error for now, we'll later add real
error handling of course and I get a result which I also want to log here and I
will also send my response, whoops, in here, in the then block I'll send a
response, 201 is the status code, the post object here however will be the
result object I get back here because that should be my created post. 

If we now save that server side code and we go back to our frontend application,
we should need to change anything in our react code instead we can just try
this, does this work? 

Let's choose an image, upload still does not work, we'll do this later, checking
it and this seems to fail. 

If we go back, I see path image url is required which makes sense because in my
model, I set image url as a required property, so in my feed controller when I
create a new post, I should also add an image url here and for now that can
point to images duck.jpg, we'll later add file upload as I mentioned. 

So my mistake, we should add this on the server side, make sure we store an
image url so that we meet the requirements of our model and now let's try this
again. 

Does that work? 

Take the duck, enter some content, click accept, this looks good post created
successfully and there we see indeed this is the data or the post which was
stored with the creator, the content, this automatically generated createdAt and
updatedAt timestamp thanks to the timestamps option and the automatically
generated ID. 

So that is working and on the server side, I'll also get no error, I only see
that created object being printed thanks to that console log. 

So that is working fine and now as a next step we can work on serving that image
and on accepting image uploads and on handling that error. 

---