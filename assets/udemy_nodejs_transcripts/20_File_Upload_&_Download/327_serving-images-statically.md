## 327. Serving Images Statically

<strong><em>no description</em></strong>

So how can we ensure that all our beautiful images are also served to the
client, that they are downloaded? 

We got multiple options for serving files and I will walk you through all of
them. 

Now option number one which you would typically use for a scenario like this
where you have files that are publicly available to everyone, like our product
images is that we simply serve our images folder in a static way. 

What does this mean? 

This means you go to app.js and there we already are statically serving a
folder, we are serving the public folder with the express static middleware. 

Now we can serve more than one folder statically and remember, statically
serving a folder simply means that requests to files in that folder will be
handled automatically and the files will be returned, so all the heavy lifting
is done behind the scenes by express then. 

I can duplicate this middleware and now also serve the images folder, just like
this and with this little change if I save that and the server therefore
restarts, if we reload this page, we still fail. 

Well if we inspect that failing request, we see that it tried to get the image
from admin/images, the reason for that is that I'm on the admin route here,
admin products to be precise, so it's only replacing the last part of my path
with that image url and the solution for that is pretty straightforward. 

In our view products.ejs where I do show my image, we simply need to add a slash
at the beginning which will turn this into an absolute path, so it will not
append it to the current path but rather create a new path with only our domain
and then the path which gets rendered here and I do this in products and of
course also on my shop pages, so on index.ejs, so basically everywhere where I
do render an image, I add a slash at the beginning. 

The alternative would be to store that path in a database with a slash at the
beginning of course, might have been easier but I want to show you both ways so
here I'll add it in my views, also here in the product list.ejs file, like this
and also in the product detail file of course, there we also have an image. 

If we change all of that and I now reload this page, I still fail and now the
reason for that is something different. 

The reason for that is that the path now is correct but my images here in the
images folder are served incorrectly. 

In app.js where I set up this static middleware, keep in mind what I taught you
earlier in this course, we basically point to a folder there like public and
images and we then tell express serve the files from inside that folder as if
they were on the root folder. 

So we would see that image if we go there and we see the path under which I try
to find that, if we open that in a new tab, we can't find it of course but we
will see it if I remove images there and the reason for that is that express
assumes that the files in the images folder are served as if they were in the
root folder, so slash nothing. 

Of course we want to keep them in the images folder and keep the path like this
and for this, we can simply adjust our middleware here and say if we have a
request that goes to /images, that starts with /images, then serve these files
statically and now /images is the folder we assume for this static serving and
now with that if we save that and we reload, we see our image here. 

So now we got that working and now we got a static way of serving our files and
that is a great way of serving them. 

Now I want to do something different though, I want to add this to the cart,
order it so that I have an order and I want to download an invoice for that
order and that will now work differently because invoices will not be public
files that everyone should be able to access, I want to be able to access my
invoice but no one else should be. 

So let's focus on this in the next lectures. 

---