## 325. Storing File Data in the Database

<strong><em>no description</em></strong>

So I'll just quickly clean up all my products here because there I'll store it
in an incorrect way due to, well how I worked with the files in the past so let
me remove all these products and now let me go back and here in my application
in post add products, in my admin controller, there I now want to handle that
file correctly. 

So first of all image here will be an object of this format with information
about the file and where it was stored, so where the physical file can be found
and now I want to save that. 

First of all, I will check if image is set because if it's undefined, then that
means that multer declined the incoming file. 

So if this is not set, if it is undefined, well then I want to return a response
with status 422 because I then have an invalid input, so I want to return that
response, add product, editing false has error is true where I pass in my old
data, not the file however, only title, price and description and the error
message is attached file is not an image, let's say and validation errors can be
an empty array, I won't mark anything as read. 

With this change in place, we can already validate this. 

If I now try to upload an image, I succeed, so I don't get my same form again. 

If I choose a PDF though, then I get attached file is not an image. 

So this is working and let's now also work on the case that we do have an image
and that we want to store it. 

Now the file already gets stored on our file system and this is how you should
store it, you should not store data like this in the database, files should not
be stored in a database, they are too big, it's too inefficient to store them in
a database and query them from there. 

Store files on a file system as we are doing it here but of course you need to
store something in a database, you need to store the path to the file, right and
that is something you can construct here with the information given to you in
the file object and you can then simply pass that data to the database. 

So if we made it after our entire validation here, I know that I have a valid
file and valid input data and then I'll create my image url again and in that
image url, I will use my image data which is that file object we get from multer
and there we have information like the file path and it's this path that is
interesting to me of course because this is the path that a file on my operating
system, it is the path I therefore want to use later on when fetching that
image. 

So this path is what I'll store here in the image url and therefore I can store
image url in the database again. 

So if we now save all of that and I do select a valid image here and I hit add
product, this now works again, displaying it does not work we'll work on this in
a second but saving does work and if I have a look into my database for the
products, you see this is the part that was stored. 

Now this is looking good but of course here if we inspect this, we see the image
is not really rendered because it can't find this, it fails to fetch images and
then well this name and in the network tab we indeed find a 404 error when the
browser sends the request for this image. 

So now that we are able to store data, let's also learn how we can serve data,
well almost before we serve it, let's work on editing this because this is
another path which won't work correctly right now. 

Right now when we load the added page, what we do is we load the page and we
send back the data we need for displaying it of course. 

So that means we render the added product page with product data that includes
our image url which is of course fine but ultimately, here we don't see the url
and we don't want to change the url when editing the product, instead here we
have a new file picker. 

Now you can of course configure this to work in any way you want but here I want
to have a behavior where if we choose no file here, we simply keep the old one
and we only overwrite it with a new file if I do choose a new one here. 

So to do that, I'll go to post edit product which is where we do handle the
incoming data and of course here we again can retrieve request file and store
that in image constant, just as I'm doing it here when we add the product, there
I'm also retrieving this file extracted by multer. 

Multer will do the same for post edit product, so I can extract it there too,
store it in an image and now this image is the thing I need to check. 

If it is undefined, then I know no file was saved and in this case this means I
want to keep the old file, by the way the same will be true if I upload a PDF, I
will simply keep the old image in that case. 

So we don't need to throw an error or return an error message, though you could
of course do that if you want, if you always want to force a new image but here
what I'll do is instead I'll first of all edit my validation page which I return
and I'll not return the image url here, we don't need that just as in post add
product, there we also don't need to return that because there is no image url
we render in our edit page any more but if we make it past our validation here,
when we store the product or when we update the product I should say, this image
url does not exist anymore. 

Instead here I want to see if I really need to set that, so I'll check if image
is there, if it's not undefined, in which case I'll set product image url to
image path. 

So the same logic as I do have it in post add product, there I also set image
url to image path but in post edit product, I do it conditionally and if the
image is undefined, so if no new image was passed, I simply don't set it on the
object which I then update and since I update it and if I don't set this, I will
simply well not update this field and I can prove this to you. 

If I update this product here now, I get an invalid value because I forgot to
adjust my validation middleware in the routes folder, for editing the product
I'm still checking for image url to be a url but this field does not exist
anymore so we should remove that from the edit product route validation logic
and now if I submit this again, it just works. 

If I now choose a different image though and before I select this, let me
quickly show you, if I update my database here, you'll see that image url did
not change. 

If I select both too now which is the same image but a different file name and
technically, a different file therefore, I update this and now if we go to that
database and we refresh, we see it set both too. 

So now we got that editing option in place too and now we do handle the file
uploads in the way we need to handle them. 

But of course handling file uploads is only one thing, we also want to be able
to see that image, so to download it kind of and that is what I focus on in the
next lectures. 

---