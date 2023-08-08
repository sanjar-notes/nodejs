## 321. Handling Multipart Form Data

<strong><em>no description</em></strong>

So now that we added our file picker, let's work on the backend and for that
I'll go to my admin controller which is where I do handle the creation of
products, also the editing of products which we'll work on later but for now,
let's focus on adding a product and here we are extracting data from the
incoming requests. 

Now I renamed my file picker here to image, so the input name is now just image
and this means that here when I try to retrieve it from the body, I should also
target the image like this or we can keep this name because it will fail
anyways. 

If I now submit this like that and I click add product, I get invalid value here
and the image url does fail because I do have in my routes, in the admin routes,
I do have some validation in place where I say the image url should be a url and
clearly it is not. 

So let's remove that validator here for the post add product route and let's try
this again and now we simply get an error, so the error handling is working and
the error we're getting is simply stemming from the fact that we're not able to
extract our image correctly. 

I can show this to you, if I console log image url here in post add product, in
this controller action and I try to submit this, then you don't see anything
here. 

It fails to log anything there because we failed to extract an image from the
request body and why is that? 

Because keep in mind you learned this a little bit earlier in this course, for
extracting the content of our incoming requests,  we set up a middleware in
app.js, we're using a special middleware, this body parser middleware and this
middleware uses or exposes a couple of different parsers and we're using the url
encoded parser, now url encoded data is basically text data. 

So if a form is submitted without a file, so just with text fields no matter if
that text field then stores a number, a url or plaintext but it's all encoded in
text when it is submitted. 

This format is then called url encoded and actually we can see that. 

If we open the developer tools and go to the network tab in there, if I do click
submit here, this failing request, this add product request, if we have a look
at our request headers, we can see that the content type is application and then
xwww form url encoded and this basically means it tries to put all the data as
text into its form body. 

We can see that down there, just form data, title, price and so on and just
image, this is invalid, this is basically an empty text because it can't extract
our file as text because a file is binary data. 

Now because of that, because of that failing extraction, we need to work with
this differently, we need to parse our data differently and the body parser that
we're using here does not give us any parser, it does not include any parser
that could handle file data as well. 

We need a new package for that, so let me quit that server and let's install a
new package with npm install --save and the name of that package is multer. 

Multer is another third party package that parses incoming requests but this
package parses incoming requests for files, so it is able to handle file
requests as well or requests with mixed data, with text and file data. 

We'll still keep body parser because we still have like for example, our sign up
form where we only submit url encoded data but now we'll have to use a different
encoding and that starts with our form. 

So back in the view, the edit product view, there I'll change my form here a
little bit, besides the class and action, here I'll also add a new field and
that's the enctype field which I'll set to multipart form data. 

Application xwww form url encoded as the default but now we'll switch to
multipart form data which is simply the content type telling the server that
this submission, that this request will not contain plaintext but will contain
mixed data, text and binary data and multer, the package we just installed will
be looking for incoming requests with this type of data and will then be able to
parse both the text and our file. 

So this is what we get there or what we will need and now with all that
prepared, let's use multer in the next lecture. 

---