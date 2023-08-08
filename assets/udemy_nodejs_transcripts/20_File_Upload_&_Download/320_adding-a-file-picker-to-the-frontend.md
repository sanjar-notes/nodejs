## 320. Adding a File Picker to the Frontend

<strong><em>no description</em></strong>

Now let's start with uploading files and there, we have a really great use case
and that of course is that when we add a new product, we right now always have
to enter a url. 

That is not a very realistic set up because in a real world application, your
users who are trying to sell things will probably not have pictures of their
products stored somewhere in the web, so we definitely want to give our users
the possibility of uploading images and that is exactly what I'll work on now. 

Adding file upload means that we have to do two things, the first thing is that
we need to adjust our form here to show a file picker to our users, so a tool
which they can use to well select a file on their operating system on their
computer. 

And then the second part is that we need to be able to accept that file in the
place where we well handle it, where we handle the incoming requests. 

Now let's start with the form and let's add a file picker there. 

So we'll dive into our views and there it's in the admin section, the edit
product.ejs file, there we will have our image url control, this one and in the
end, this image url should now become a file picker. 

For that, I'll copy this old block and comment it out so that we still have it
around in case we need it later but this will now become a new image uploader. 

There I'll just have image as a label. 

Now that class here where I try to mark this as invalid, I'll remove that
because we'll not have an input where we would add a red border around, the type
here will be changed to file, the name I'll change that to image and I'll change
the ID too, also up here therefore and now the value with which I'll
pre-populate this, I'll remove that because even if we're editing this, I will
always present an empty file picker and we'll just have to tweak our backend
logic later so that when we're editing this and we're not sending a new file, we
simply keep the old one and we overwrite the old one if we do send a new one but
for now I'll simply set up my file input like this. 

Now if I save that and I reload this page, now we have our file picker here
which is a default html element and if we click it, we can select a file like
this boat here, you can pick any file, it should be an image of course. 

So now I have chosen that and now if I would enter the rest and add this
product, we would fail because right now we got no logic in place to handle an
incoming file, to store it or to do anything with it and this is the part we'll
have to adjust now. 

So in the next lecture, I want to make sure that we can handle incoming files
just as well as incoming text which we previously always accepted. 

---