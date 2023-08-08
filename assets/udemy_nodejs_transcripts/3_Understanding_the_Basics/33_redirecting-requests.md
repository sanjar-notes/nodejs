## 33. Redirecting Requests

<strong><em>no description</em></strong>

So we made sure that we listen to requests to just slash nothing and that we
return some html code with our input field on it. 

Now when we click that send button, we send a post request to /message but we're
not doing anything with that, time to change that. 

Let's add another if statement here and let's check if the url is equal to
message and let's add another condition and that condition is that I want to be
sure that we're not handling a get request but a post request here, so let's
also parse the method from request method and make sure that method is equal to
post. 

Now we'll only enter this if statement if we have a post request to /message
which happens to be exactly what we create with this form. 

In this case, I want to do two things, I want to redirect the user back to slash
nothing, so not leave him on /message and I want to create a new file and store
the message the user entered in it. 

Now this involves a couple of things, let's start with redirecting and creating
that file. 

We actually already worked with a file in the first core section and do you
remember how that worked? 

Feel free to go along on your own if you know that. 

We need another package, another core module and that was the file system core
module. 

So let's import it by storing the functionality in a constant, you can name it
however you want, I'll name it fs because the package is named fs but you can
also name this differently. 

This, not the package, just the constant. 

So fs allows us to work with the file system and here I now want to write a new
file, so here let's execute write file and write file takes a path to the file
and I'll just use the file name to create it in the same folder as app.js and
I'll simply name it message.text and in there, I obviously want to store what
the user sent. 

Now this is a little bit more work, so for now let's just put some dummy text in
there and let's redirect the user. 

Now important, we should actually use write file sync for now and I'll explain
what the difference to write file which also exists is in a while, so let's use
write file sync for now. 

Now write head which basically allows us to write some meta information in one
go and then we set a status code of 302 which stands for redirection and then we
pass a javascript object with some headers we want to set and you could also do
this in two steps by the way, you can also set the status code to 302 and then
simply have, whoops set header And there we set the location, this is also a
default header accepted by the browser and we set that location to just slash
and I will automatically use the host we're already running on and then we have
to call res end. 

And important, as before return this so that we don't execute these lines
otherwise we will get an error. 

Now let's restart our file here and make sure to go back to slash nothing and
reload that page with the input field and send any value and you should simply
reload that in the end because you get redirected here but you can see that
redirect here in the network tab of the developer tools, here 302 indicates we
send a request to message and we were redirected to localhost. 

So this is working and we also got the message text with dummy inside of it. 

Now let's also get rid of that though and let's work on actually parsing the
data the user sent us and writing that data into that file. 

---