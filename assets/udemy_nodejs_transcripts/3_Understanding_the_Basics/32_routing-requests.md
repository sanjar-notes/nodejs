## 32. Routing Requests

<strong><em>no description</em></strong>

In the last lectures we learned how to spin up that server and that we get a
request object with information about the incoming requests and the response
object that we can use to send back a response, let's now connect both, requests
and response. 

Instead of printing some request data to the console which of course doesn't do
much for us, let's instead start writing a very simple web server that does
different things depending on which route we enter, so depending on which slash
whatever part we enter here. 

So let's say for slash nothing, we want to load a page where the user can enter
some data which we then store in a file on the server once it is sent. 

We can do this by first of all parsing the url. 

I'm storing it in a new constant and I do this by accessing request url,
remember that was something like slash, /test, whatever we entered. 

I will then add an if statement and check if url is equal to just slash and only
this will match, by the way the triple equal sign means that this will only be
true if url is both a string and has that value. 

So now here if that is the case, I want to return a response which holds some
html that gives the user an input form and a button that will send a new request
in return and that will not be a get request by the way. 

So let's do this step by step, let's copy this code here and put it into this if
statement and here I will write a html document with a head, maybe a different
title, enter message and the body will now not hold a h1 tag but instead a form,
this is a default html element of course with an input of type text let's say
and a button and this will be super ugly because we have no styling but it's
about the functionality for now, the button tag must be closed by the way. 

The button will be of type submit so that it submits the form and that will be
some default html behavior we're using here where a button with type submit in a
form element will send a new request and we'll configure that request in a
second. 

Let's first give the button a caption, send and now on that form element here,
we add an action which is basically the url this request which will be generated
automatically should be sent to and I will use /message here and this will
automatically target the host it's running on, so localhost in our case here,
localhost 3000 to be precise and then we define the method, the http method that
should be used and there we previously saw if we expand this, that we get a get
request which is the default if we enter a url, well here we are not entering a
url instead we want to send a so-called post request. 

There is a limited set of http words you can use, get and post are the two most
important ones. 

A get request is automatically sent when you click a link or enter a url, a post
request has to be set up by you by creating such a form, there also are some
other ways by using javascript but we'll ignore them for now. 

So in html we create such a form and we defined that the method should be post
and this will send a post request to /message and the cool thing about form is
it will not just send such a request, it will also look into the form, detect
any inputs or related elements like selects we might have and if we give that
input a name which we should, message, it will also automatically put that
message into the request it sends to our server. 

So now here when we visit just localhost 3000 slash nothing, we will return a
response where we render this html code. 

Now let's also put a return statement in front of res end. 

This is not required to return a response but to return from this anonymous
function and to not continue this code because we return prior to it and this
will quit the function execution. 

And we must do this because I told you that after res end, we must not call any
other res writes or res set headers but this what happens if we not return
because then it would just continue execution with these lines. 

I don't want that,  if we make it into the if statement, we should also quit
here, we should exit out of this function. 

With this let's restart the server by quitting it with control c and restarting
it with node app.js and let's reload this page on localhost 3000 slash nothing
and we see my input and the send button here. 

Again not super pretty but it's working. 

Now let's make sure that if we enter something and we hit send, we see this,
that we now not only see this but that something else happens. 

By the way we do see this because now the url is /message and /message does not
make it into this if statement and therefore this code runs. 

But we want to do something else so let's do that in the next lectures. 

---