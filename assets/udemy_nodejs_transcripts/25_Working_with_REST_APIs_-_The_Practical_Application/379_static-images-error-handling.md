## 379. Static Images & Error Handling

<strong><em>no description</em></strong>

So let's make sure we can serve that image and in the future also accept image
uploads. 

Now for serving that image, we have to make sure we serve that images folder
statically, at least is the approach I want to use, you learned all about that
in my file uploads and downloads module and the general logic there still
applies, so check that out to learn more about that. 

In app.js, I want to set up static serving of my images folder. 

For that up there after I register my body parser, I'll use another middleware
and I will do that for any request that goes to /images, here I'll use a
middleware built into express, the static middleware which I use by calling the
static function and now I want to serve my images folder. 

For that let's import the path package, the core path package node provides and
then here we can use path join to construct an absolute path to that images
folder. 

By using the special dirname variable which is available globally in nodejs and
gives us access to the directory path to that file, to the app.js file and in
that same location as this app.js file, we find the images folder, so we can
pass images as a second argument and path join will construct an absolute path
to this images folder and that is the folder we'll serve statically for requests
going to /images. 

With that we should be able to use our image in the frontend code or to see it. 

If we save that server side code, to view the image on the frontend however,
we'll need to be able to click view here because the image will only be included
on the detail page and that however will not work because we need a route to
serve a single post which we don't have yet, so we'll have to postpone this. 

It will actually be what I work on next but before we do that, I want to set up
proper error handling. 

In the feed controller, right now when I catch an error here I log it and there
when I validate the input, I return an error response manually. 

You can do that and you could also return your own error response down there but
you learned that you can set up a general error handling function in expressjs
and I want to use that function. 

Now how do I use it though? 

Let's maybe start with validation. 

Instead of returning a function manually here, I will create a new error object
with new error and the message I set up here is the message I'll pass to my
error object. 

I'll then also add my own custom property which you can name however you want
and I'll name it status code and set this to 422. 

Now I will throw that error and I can remove that return statement. 

Now what does throwing an error do here? 

It will automatically since I'm not doing this in an asynchronous code snippet
or anything like that, it will automatically exit the function execution here
and instead try to reach the next error handling function or error handling
middleware provided in the express application. 

We also got another possible error and that is in here if something goes wrong
with storing the post, there I don't want to log the error instead here I will
check if my error has a status code field which it will not have but
theoretically if I had more complex code where I throw my own errors, there
might be some error that has it. 

So I check if that exists and if it does not exist, hence the exclamation mark
here, if it does not exist, I will add it and I will set my status code to 500
then because it's some server side error. 

Now you learned that since I'm inside of a promise chain, so inside of an async
code snippet, throwing an error will not do the trick, this will not reach the
next error handling middleware. 

Instead you have to use the next function here and pass the error to it and this
will now go and reach the next error handling express middleware. 

Now the last step is that we register that middleware and we do so in app.js. 

There let's go all the way to the bottom after all my routes here and let's use
a new middleware which has this error handling definition of getting an error as
the first argument and then request response and next. 

This will be executed whenever an error is thrown or forwarded with next and
here I want to log it so that we as a developer can see what's wrong in an
easier way and then I'll extract my status code here, from error status code, so
from that error object, I'll extract my message from error.message. 

This property exists by default and it holds the message you pass to the
constructor of the error object and now I can return an error or a response with
the status code of the status I extracted and we can set this to a default value
of 500 with this syntax by the way, so in case this should be undefined, it will
now take 500. 

So we return this status code and we use json data of course where I have a
message of the message I extracted. 

And now I have this general error handling functionality which should work which
I can quickly validate by going to my feed routes and changing that validation
logic again to seven for the title as a minimal length and now let's try to
enter a title that is not long enough and let's see if we now still see an
error. 

We do, we still get that error being thrown with the right status code, so this
works even though I'm now using my custom error handling function which is a bit
of a more elegant way of handling errors now. 

So this is working, let's now move on to creating the route for getting a single
post so that we can finally also see if we can see our image. 

---