## 322. Handling File Uploads with Multer

<strong><em>no description</em></strong>

So let's use multer now on our backend. 

We can restart the server already because we installed that package and now
let's go to our admin controller and let's work on post add product here, we
want to use multer to extract incoming files. 

Now multer is actually not a package which we will use in here, instead just
like the body parser we use here, multer is some middleware which we execute on
every incoming request and it then simply has a look at that request, sees if
it's multipart form data and tries to extract files if that is the case. 

So it is some extra middleware we add and therefore we can import it here in our
app.js file. 

We can import multer by requiring it from the package like this, multer and
thereafter we can use it, so maybe after the body parser, we can use multer. 

Multer has to be executed as a function and then we have to call another method
on that and that simply defines if you expect to get multiple files or only one
file and we will only expect one file, so we use the single method and then we
define the input name which will hold the file and in our case, that is image
and this is not a random value, I'm using image here because in my view, this
input which holds the file, so this file picker here is named image as well. 

So with that, we initialize multer and let's now see if that works. 

Now to see that, we need to know how multer will actually store the incoming
file and for that, let me go back to post add product and instead of extracting
request body image, let me access request file here and let's see what this
gives us, I will also console log image url now. 

Now let's save all that and see what that gives us. 

If I now try to add a product again, I'll choose that same file from before,
enter any values up here, click add product and I still get an error. 

Now if we go back, we see something interesting though, indeed here this part is
what I log here. 

So here what we see is that multer seems to have done something, it seems to
have stored something in that file property on our request object and that is
what we print here essentially and it stored the name of the field where it
extracted that, it detected the file name, it detected the mime type so which
type of file that is and that buffer here is essentially how node handles the
binary data. 

You'll learn about streams and buffers earlier, in the end this is the result of
the streamed data, the file basically was sent to our server as a stream or was
handled as a stream to handle it efficiently if it was bigger and then this is
the collected data in a buffer which as we learned is like a bus stop, it gives
you a way of working with the stream data, here in this case it's the combined
stream and data and we could indeed work with that buffer to turn it into a
file. 

Now you can actually configure multer a bit differently if we go back to app.js,
when we set up multer, we can pass an object to the multer function and there we
can set some options and one option is the dest option. 

Now here we could specify /images or just images, like this. 

What this will do is that when I again add a product here and don't worry that
it still fails because we're trying to store the file in the database right now
and we'll do all kinds of stuff with it for which our code is not prepared but
the upload works but with this option set, you also see that the output down
there changed a little bit. 

We don't have the buffer because now multer is able to do something with the
buffer, instead of just buffering it all in memory, it can then turn that buffer
back into binary data you could say and it stores it in this path here. 

So indeed if you have a look at your folder, you should not have an images
folder with some file in there. 

Now that file has some random hash name, does not have a file extension and is
not recognized as an image but indeed if I change that and I add .png at the
end, this is the image I uploaded. 

So this does work. 

All we now need to do is we need to tweak the way this file is named and that is
something we'll do in the next lecture. 

---