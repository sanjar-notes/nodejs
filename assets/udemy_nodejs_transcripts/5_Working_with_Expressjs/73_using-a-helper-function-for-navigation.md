## 73. Using a Helper Function for Navigation

<strong><em>no description</em></strong>

Before we work on the styling, let me add one note on how we navigate it to the
root folder in shop.js and admin.js. 

For one you could just use dot dot here instead of dot dot slash and this would
be preferable even though both should work on Windows and Mac because now we
make no assumption about the separator we're using when constructing a path. 

So with this, if I go back and I now go to just admin add product here, it still
works but now we get a cleaner way of doing this but there is an even nicer way
we could implement this. 

We could also get the parent directory with the help of a little helper
function. 

For this I'll create a new folder here, helpers or util, I'll go with util, you
can name it however you want and there I'll add my path.js file and it doesn't
matter that this clashes with the global module because we'll import it
differently anyways. 

Now there, I'll add an export with module exports and I want to export a little
function that helps me construct a path to the parent directory or not a real
function, instead a variable I should say. 

First of all here, I'll import the path with require path as we did it before
and then I will use a different function here, not join but dir name. 

Dir name as you can see in their quick help on the right here returns the
directory name of a path, so this sounds pretty useful, if we use that we just
have to find out which directory or for which file we want to get the directory
name. 

Well there we can use the global process variable, that is also a variable that
is available in all files, you don't need to import it and there you will have a
main module property. 

This will refer to the main, well module that started your application, so
basically to the module we created here in app.js and now we can call file name
to find out in which file this module was spun up. 

So put in other words, this gives us the path to the file that is responsible
for the fact that our application is running and this file name is what we put
into dir name to get a path to that directory. 

With this we can import from this file, here I'll add my own import separated
from the other ones simply to make it easier to identify and I'll name this root
 dir, the name is totally up to you but I will require this from going up one
level into util and then path and this root directory is in the end what I want
to inject here. 

So root directory is what I'll start with when creating this path. 

And now let's try reloading this page here and it still works and it should
still work because now we're in the end having a pretty neat way of constructing
a path to our root directory. 

I'll do the same in shop.js, import root dir from the util folder and the path
file in there and replace dir name dot dot with root dir. 

Again you could have totally sticked to the old approach but this one is a even
cleaner one and one that should be pretty straightforward to use and that should
work on all operating systems and it always gives you well the path to the root
file. 

With that, let's move on to the styling. 

---