## 382. Uploading Images

<strong><em>no description</em></strong>

If you remember that slide from earlier, file uploads require no changes on the
server side, only on the client side. 

So what do you learn now is not that important to you if you're not working on
the client side yourself, on the server side the logic is exactly the same or
pretty much the same we used before, let's still implement it again. 

Here I'm back in the node application and I want to accept uploaded files. 

Now in the past we did this with a special body parser, a special middleware and
that was multer. 

So let's install that again with npm install --save multer in the node rest API
project, not in the react project. 

So there we install multer just as we did it earlier in the course and with it
installed, let's go to the app.js file and I will implement exactly the same
logic as I did before. 

So I'll go through that really quickly, you should check out that file upload
download module if you want to learn all the details. 

I will first of all import multer into my app.js file and with it imported, I
will configure some things for it, maybe here. 

I will configure the file storage with multer disk storage to control where the
files get stored and there, we have a destination key which is a function in the
end, an arrow function where I get request object, information about the file
multer detected and a callback I should call once I'm done defining the
destination. 

I'm done immediately here, got no error and the destination is images pointing
at that images folder here. 

So that's the first thing here, we add another function to the disks storage
object and that's the file name function which defines how the file should be
named, get the same arguments as in the destination function and I call that
callback with null as an error and the filename will be a combination of the
date which I convert to a string and then a dash and then the original filename,
really simple, exactly the same logic I used before. 

I'll also define a file filter where I also have or which also is a function
which gets request, information about the file and a callback and in here, I'll
check for a couple of mime types. 

I'll see if my file mime type is equal to image/png or if file mime type is
equal to image/jpg or if file mime type is equal to image/jpeg with an e, that
is my if condition. 

If anything of that is true, then it is a valid file and therefore I return no
error and true as a second argument in the callback otherwise it would be
invalid and I still have no error but I return false here and this is again
something you learned in the file upload module. 

Last but not least, I need to register multer and I will use it here, maybe
after the json body parser. 

I will use multer as a function, pass an object to configure it, assign a
storage to my own file storage constant we just created and add a file filter
which points at that file filter constant we just created. 

On that multer function, I'll then also call single image to inform multer that
I'll extract a single file stored in some field named image in the incoming
requests. 

Now every incoming request is parsed for that file or for such files. 

With that, multer is registered and now we can use the file in our controller
where we create a new post. 

For that in create post, I can first of all check if request file, if that is
not set because if it is not set, then I'm missing a file so I will create a new
error here, no image provided maybe, I will set my status code to 422 because
it's also kind of a validation error and I will throw that error, that's the
first check. 

Now if I do find a file then everything is good, multer was able to extract a
valid file, so then I'll just set up an image url constant and access request
file and there the path variable which multer generates which holds the path to
the file as it was stored on my server. 

And now this image url is what I use here as an image url of course instead of
my dummy data. 

Now we should be able to extract files and really store them. 

Let me now run this but of course now we also need to tweak our frontend to be
able to make that work and I didn't do this in advance because there is
something special which I want you to know. 

In the react code, so on the frontend, go to that feed.js file in pages feed and
there, let's go to the finish edit handler. 

There we're setting up everything we need to send a request to the backend to
create a new post and right now, we're doing this with json data. 

Now we won't use json data anymore because json data is only text, so only data
that can be represented as a text which a file can't be or not easily, it will
be very big quickly and very big files are a huge issue or impossible to upload
like this. 

So we can't use json for data where we have both a file and normal text data,
instead we'll again use form data. 

Now we did use form data automatically when earlier in the course where we had a
traditional app with rendered views, when we used a form with this multipart
form ank type which we added to the form html element if you remember. 

So this form data is what we'll also use here but we'll not use anything to any
form element, we'll do it all in javascript instead. 

Here where I have this marker, this comment, we can create a new form data
object with a built-in object that browser side javascript offers, the form data
object. 

This now allows us to append data to that object, for example the title, first
argument to append is the name of the field, second argument is the actual data.


So here we'll have post data.title, exactly what we passed to the json data
before. 

Of course we don't just append the title, we also append the content, so let's
append that and now we also want to append an image because we can append files
as well. 

Now this should be named image because we'll be looking for this field on our
rest API and now here, I can reach out to post data image because that is where
I will get my image in my frontend code. 

With these three fields, I got form data prepared that now has mixed content,
text and a file and now I want to use that form data as a body for my request. 

We should not set the header to application json anymore because that would be
incorrect and would break our app because we would try to parse it incorrectly
on the server side, instead the form data will automatically set the headers,
that is kind of convenient. 

All we need to do is we need to set form data as our body and the rest will be
done for us. 

If we now save that and we create a new post, let me create a post here, a duck
and choose that lovely duck image again, this is a duck and click accept. 

Now this was pretty quick, if I now click view here, I see my duck here which is
looking good and on the server side, I also see this image which was generated,
which has a time stamp and this is the uploaded image, I got no error here so
this is all looking good. 

So uploading files also works, as you saw on the server side it has exactly the
same logic, on the client side things need to change but of course this is a
node course, so it depends on which client you are using, how you need to adjust
your code there. 

---