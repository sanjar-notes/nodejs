## 101. Storing Data in Files Via the Model

<strong><em>no description</em></strong>

So let's make sure we can save our product to a file and not to this array here
anymore. 

For this when we call save here, I want to save it to a file and of course in
that file, I want to have all products, the old ones and the new one. 

So therefore first of all, we need to be able to work with the file system, so I
will import fs from the core fs module. 

Now that file should then also be created in special path, so I will use the
path tool, the path module to construct a path that works on all operating
systems. 

Now here in save, I will then create my path and I will do that with path join,
so using the path core module, whoops, and I name this p so that I avoid
namespace clashes and the path should be my root directory and we actually still
have that helper function but if you deleted it, you can of course recreate it
as we did before or simply copy this code here if you want, you also find it
attached to this lecture again in case you deleted it. 

I will simply copy that logic here and move it in there but of course I could
absolutely simply use my helper function I created there. 

But this is of course just the root directory, in there I will have a new data
folder and I will create it ahead of time so that we don't get permission
issues. 

So I'll have added the data folder to the root project folder and in that data
folder, I want to store my file, so that will then actually be a file and that
should have a name of products and I will give this an extension of json because
I want to store my data in json format. 

Ok so that's products, now to store a new product in there, first of all I need
to get the existing array of products, so I will first of all read that file. 

So let's use fs read file and this reads the entire file content of a file and
by the way for very big files, there are more efficient ways because you don't
want to read them all into memory before you work with them, you can read them
as a stream then, there is such a function, you can create a read stream with
this function but we can read the entire file here, this is ok and I will read
the file at this path, p which is that file I'm interested in and then I will do
something once I'm done reading it and there we either get an error or we get
data, so we get the the file content you could say, there will be a buffer
though. 

Now let's log the file content here and let's see what we get if we now call
save. 

If I go to add product and I'll type something here, it crashes and it crashes,
if you the scroll up because products is not defined in fetch all of course. 

In save however, it didn't throw an error but we get undefined here as you can
see and we did get undefined because this file simply doesn't exist, there is no
content in it therefore, you can see that here we've got no file with that name
so reading it therefore kind of failed. 

And if I add an error here to print the error we get and I try this again, so
let's go back to add product, click that and we scroll above this error message
here, you see this is the error message we're now logging with this line and
there we see no such file or directory and that makes a lot of sense because
indeed, it does not exist as I just mentioned. 

So obviously if it doesn't exist, then I also want to continue and I can. 

I will simply check if we got an error and this will be null if we get none but
if we have one then I simply want to create a new empty array because we have no
existing products.json file, so we got no old products stored and otherwise I
want to use the existing one. 

Put in other words I'll add a new variable here which I'll name products and
initially this is an empty array and I will actually keep it as such if we do
have an error but if we get no error and therefore I will add an exclamation
mark here, so if we got no error, if this therefore is null so if we got no
error, then I want to read the products from the file which I extracted. 

So therefore here I know that file content will be something, it should be the
content of my file and since that is a json file, I will store it in json format
there so then I will set products equal to json which is a helper object
existing in vanilla nodejs, so you don't need to define this on your own  and
there we have the parse method which takes incoming json and gives us back a
javascript array or object or whatever is in the file. 

So here I can parse the file content and that should work or at least we should
try that. 

So now I know that product will be an array, either the one I read from the file
or an empty one and therefore, we can now append our new product there, so I
will call products push and push my new product which is this onto it. 

Now important, to ensure that this refers to the class, you should use an arrow
function here because otherwise this will lose its context and will not refer to
the class anymore. 

We have this setup though where I do use an arrow function, this should refer
still to my class and therefore now I can push this onto this array, either to
the new one or the one I read from the file and now the remaining work is that I
need to save it back into the file. 

So again I will use the file system module and now I'll use write file and I
will write it to the same path as where I read it from and I will put my json
data into it, so again I will use that json helper object and now there is the
stringify find method which takes a javascript object or array and converts it
into json so that this has the right format, so there I will take this products
array and convert this to json and then this gets written to the file. 

And here I also have a callback where I may get an error and I will simply log
that error here to see if that works. 

With all that, let's go back, let's go back to the add product page and click
this button. 

This error of course still exists but now if we scroll up, let's see if that
worked. 

Here that is looking good and in data, we indeed see a products.json file which
does contain that one product we created. 

Now that was the we have no old data case, let's now go back and add another
product here and see if that also works. 

If I scroll up, well we also see it here I guess, this also worked out just
fine. 

So this is working, we are able to read a file, append data to the existing data
or create it if it didn't exist yet and therefore our data storage in the file
seems to work, obviously it's a very basic storage but better than nothing. 

Now obviously we also want to be able to fetch the data from there, so in fetch
all I also want to read this file here I will read the file at my path and I
also will therefore get my error or the file content using arrow function here
and this will then hold the data I want to use. 

Now if I got an error here, I want to return an empty array because then I got
no products right, I always want to return an array because that is what fetch
all expects but it should at least be empty in case of an error and of course
you could also throw an error message and show one but here it'll just be the
empty array otherwise and I don't need an else block because after return, we
would finish the execution of this function anyways, so after this if block, I
will return my parsed and that's important, otherwise it will just be a string,
my parsed file content and this is important to keep in mind because this here
is in the end retrieved as a text. 

So to return it as an array, you need to call json parse. 

So now I return my file content in a parsed form and therefore, I get rid of the
return product statement here and I will now always return my objects or my list
of products. 

So let's see this in action, let's save this and reload this page here, key is
not defined, makes sense, I'm trying to read something from this path but that
path is only defined in the save method. 

So for now let's copy it, we can of course refactor that but let's copy it for
now and now if I reload this page, I still get this error and this can now be
very hard to debug or to understand but do you know what's going wrong here? 

We'll fix it in the next lecture. 

---