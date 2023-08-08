## 334. Deleting Files

<strong><em>no description</em></strong>

Now in this module we covered a lot and we work with files a lot. 

Now one thing you might notice is that whenever we for example change an image
or when we delete a product, the file belonging to that product, the image
belonging to the product sticks around. 

Now obviously you can always delete files with the file system package, there
you also got options for deleting files. 

You could delete files whenever you added a product when you override the image,
so here if you are inside that if block and we set a new image url, then we
could also kick off a function that goes ahead and deletes the old image by
fetching that from the product first because we're fetching the product here, so
we can get access to the old image path by fetching that path and then using the
file system to delete that old image and we can of course also delete an image
when we delete the product. 

So let's add this functionality as a last step now and for that, I will go to my
util folder and add a file, js file where I will add some helper functionality. 

There I'll import the file system, so the file system is imported here and I'll
have a constant which holds a function which I'll name delete file. 

This function should accept the file path and that's it let's say. 

In here I can use the file system package and there, you'll have the unlink
method, it deletes the name and the file that is connected to the name, so it
deletes a file at this path. 

So here I pass file path and then this has the callback we know with an error if
it fails and in here, we can simply check if we got an error and then I want to
throw it again and then it should bubble up in our default express error handler
should be able to take over otherwise I'll not do anything here. 

So it's like a method I can always call to pass in a file path and delete that
file. 

And now we can use that in our admin controller, so let me import my file helper
here by requiring it from the util folder and there the file, file and now I can
use that file helper for example in the place where we added a product. 

If we are in this if block and we know we'll replace the image url, then before
I do so, I will use file helper and I call my function there, for that I need to
export it though. 

So in here I want to export delete file, this will hold my delete file constant,
so this function and now in the admin.js controller, here I can call file helper
delete file and I pass in product image url, so that path to that file and now
this should fire. 

I'm not waiting for this to complete, I continue with my other operations, I'm
doing this in a fire and forget manner, so I'm firing this function and I don't
care about the result. 

If I wanted to, I would have to pass my callback here, so a function which then
continues with the rest in this function here but I simply fire it like this and
I will do the same when we delete a product. 

So in there when we do delete it, here I also want to delete the respective
image and for that, I first of all need to fetch my product of course, so I will
have find by ID in here, find it by prod ID and then here I have then and catch.


In catch I can next any error I get and in the then block, I will have access to
my product, so here I can then execute my file helper. 

I should of course also check if product is not set in which case I'll also
return next with a new error product not found and otherwise I delete that and I
should only trigger delete one here after I found this otherwise we have a race
condition where deleting could finish before finding is finished and that would
be bad. 

So we'll grab that delete one code, move that in here and return it to return
the promise returned by delete one and then I can actually replace that catch
block with my old then and catch block and this will catch errors in any of the
then blocks and it will also make sure that I first find the product and once I
found it, I delete the image and I simultaneously start deleting the product
itself. 

Let's save all of that and let's see if that works. 

If I go back to admin products here and I delete product one, this is cleared
and here I also have one image less, if I delete the second product, it's only
three images, so this works. 

The other images are still sticking around because previously when I started
deleting products and so on, I did not have that logic in place but now this
works. 

Fetching my invoice or generating it on the fly works and thanks to the fact
that we store a snapshot of that in the database, it even works after the
product was deleted which is of course the way we want it to work and with that,
we have a really nice setup here. 

---