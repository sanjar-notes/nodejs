## 70. Serving HTML Pages

<strong><em>no description</em></strong>

So welcome back, in case you skipped you'll find these two html files attached
to this lecture, so make sure to download them and enter them, insert them into
your views folder and now the goal is to serve them. 

We didn't work on the js files in the last lecture,  we just added the html
files and make sure to explore them to understand what they do, in the end we
got the same content as before, we just added an extra header and then in add
product, we still have the form, in shop.html we got some dummy code since we
have no products to serve yet and now I want to serve these html files in my
routes. 

Now how does that work? 

Let's start in the shop.js file, instead of sending some text or this html text
here in this case, let's instead send a file with send file and send file well
allows us to do just that, send back a file to the user and as you see here in
description, it automatically sets the content type response header field and
we'll see if that works for us or not. 

So send file is what I execute and now we just need to point at that file we
want to send. 

Now here, the question is how does the path look like? 

The file is in the views folder but how should this path now look like? 

Well we could try using slash and assume that we see all of that from the view
of the app.js file which is in the end the file which starts our entire server,
the fact that shop.js in in a subdirectory doesn't really matter because we
export its functionality and import it into the app.js file which is in the root
folder. 

So we could try using slash for the root path, an absolute path seen from the
root folder and then views and then shop.html, like this. 

Let's give this a try, let's save this, go back to the page and reload localhost
3000 slash nothing and I don't see that. 

Well the reason for this is that this path is incorrect, let's try ./ here, if
we now reload, path must be absolute is the error we get. 

So whatever we tried, this doesn't seem to work, the reason for this is that an
absolute path would be correct but slash like this actually refers to our root
folder on our operating system not to this project folder. 

So in order to construct the path to this directory and this file here
ultimately, we can use a feature provided by nodejs, another core module. 

We can import the path core module by requiring path like this and then here, we
send a file where we create a path with the help of this module by calling the
join method, join yields us a path at the end, it returns a path but it
constructs this path by concatenating the different segments. 

Now the first segment we should pass here is then actually a global variable
made available by nodejs and that is the underscore underscore and that's
important, these are two underscores dir name. 

This is a global variable which simply holds the absolute path on our operating
system to this project folder and now we can add a comma and simply add views
here because the first segment is basically the path to this whole project
folder, the next segment is that we want to go into the views folder and then
the third segment will be our file, so here shop.html and don't add slashes here
because and that's important, we use path join not because of the absolute path,
we could build this with dir name and then concatenating this manually too but
we're using path join because this will automatically build the path in a way
that works on both Linux systems and Windows systems because as you might know,
on Linux systems you have paths like this and I'm not talking about paths in the
url but on your file system now but on Windows, you use backslashes for your
paths and therefore if you manually construct this with slashes, it would not
run on Windows and the other way around. 

Path join basically detects the operating system you're running on and then
automatically builds a correct path. 

Now with that, we could expect that it works but actually dir name here will
point in this routes folder, right. 

Dir name gives us the path to a file in which we use it and we're using it in
the shop.js file in the routes folder, so this will point to the routes folder
but views is actually located in a sibling folder to routes. 

So what can we do regarding that? 

Now the solution is that we add one more segment in there and that is ../ and
this simply means go up one level, so this will now build a path where it first
goes into the folder of these files, so into routes, then it goes up one level
then into views, so if it's up one level it's in the root folder then into views
and then it serves this and with that if we now load localhost 3000/ again, we
see that html file being served. 

And now is a great time for you to pause the video and ensure that you serve add
product when this route gets loaded. 

Were you successful? 

Let's do it together. 

For this, let's first of all import the path module again, the core module, so
const path require path to pull that in. 

We don't need to install that because it is a core nodejs module and then here,
we don't use send but send file and we will then use path join, the dir name
variable to get the path to these files folder and then we can go up one level
and then into views,  whoops, should be a string, views and then we want to
serve the add-product.html file. 

With this if we save that and we head over to add-product, whoops that should be
admin/ add-product, we see this page too. 

Now the styling is missing because we don't have any but this works and we can
also check on add-product that the correct content type was assigned by express.


So this also works and now we see how we can serve simple html files for the
different routes we have. 

Now here's one bonus task for you which I want you to solve and which we'll
solve together in the next lecture, add a new html file which is your page not
found page which you then serve if we ever reach this middleware function. 

---