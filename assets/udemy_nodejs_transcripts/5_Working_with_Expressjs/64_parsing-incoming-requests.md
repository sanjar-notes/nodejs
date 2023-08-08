## 64. Parsing Incoming Requests

<strong><em>no description</em></strong>

Now we had a very close look at the whole middleware thing, let's now understand
how we can actually work with incoming requests and how we can extract data and
for that I again want to be able to handle a post request. 

So let's say on add product here, I want to actually return a html page with a
form. 

For that I'll again return a form and just as a side note, this of course is a
bit of an incomplete html document, we should also wrap this in html and body
and so on tags. 

I'm keeping this shorter here to make it easier to read but later we will also
write proper html code, no worries. 

So I have my form here and in there, I'll have my input of type title, of type
text here with a name of title let's say and I'll add a button again and that
button will be of type submit because it should submit this form and send a post
request therefore and I'll simply give it a caption of add product. 

So let's simulate that this is a form that allows us to add a product to our own
online shop or something like that. 

Now this is our form here and the form needs an action, so the path, the url to
which the requests should be sent and let's name this product and the method
should be post let's say, can also be written like this. 

So this will send a html code back which holds a form and now we need a route or
a middleware that handles requests to product. 

So we can add app use/product, now the important part here is we can place that
prior or after this middleware, they won't clash because they have nothing in
common regarding the path, they have product in common but /add-product is
different to /product, it just has to come before this one because otherwise
this would execute prior to that. 

So this position here looks all right and then we again have our function which
receives these three arguments, as a side note, you can of course omit an
argument you are not planning to use, at least the third one you can't omit to
the first one if you want the response because the order does matter but if you
never use the third one, you can omit it but I always add it here to make it
clear that it exists. 

So now with that, we have this function which we'll execute for product and in
there I want to redirect and for now I want to log the incoming data to the
console. 

Now what we can do here is for redirecting, I can use response redirect which
certainly is easier than manually setting the status code and setting the
location header. 

So redirect is another convenience function added by express and here I can
redirect to let's say just slash, so it will automatically redirect me to the
slash route. 

But of course this is not the only thing, I'm also interested in getting the
body of my incoming requests, so extracting what the user has sent me and for
this, expressjs now has a convenience feature for us. 

If I console log request body here, this is a new field added by express and
let's see what's in there. 

So if I now save this, we should be able to go back to /add-product and
hopefully see an input field and let's add a book here and hit add product,
we're redirected to slash, this is working and in the console, we see undefined.


Now let's get rid of the other console logs so that this is less clouded with
logs, we can also remove that. 

So we see undefined and the reason is that we're almost there, request gives us
this body convenience property here but by default, request doesn't try to parse
the incoming request body. 

To do that, we need to register a parser and we do that by adding another
middleware. 

and you typically do that before your route handling middlewares because the
parsing of the body should be done no matter where your request ends up and
there, I want to parse the incoming request body. 

Now for that we can install a third party package and we do that by running npm
install --save because this will also be a package that is used in our code
here, that does matter for production. 

So just save not save dev and the name is body parser. 

Now this would actually be included in express by default because the community
wanted that again, it was in the past, then it was removed, then it was
re-added, I will use that third party package which is the recommended way of
using it because if they ever decide to pull it out of express again, this code
I'm teaching you will still work. 

So now we installed a new package, the body parser and we can import that here,
I'll store it in a body parser constant, the name as always is up to you and the
package is named body-parser and now we can use that here by calling body
parser, so using that object and then .urlEncoded. 

This is a function you have to execute and you can pass options to configure it
but you don't have to here and now what this does is it registers a middleware,
so this function in the end just yields us such a middleware function, so this
parses such a function here in the end even though we can't see it and this
package will in the end, in this middleware function call next in the end, so
that the request also reaches our middleware but before it does that, it will do
that whole request body parsing we had to do manually in the previous core
sections. 

Now this will not parse all kinds of possible bodies, files, json and so on but
this will parse bodies like the one we're getting here, sent through a form. 

If we have other bodies like files and we'll do that also in this course, we'll
use different parsers and this makes expressjs so extensible. 

If we need something, we can just plug it in, you see how easy that is, it's one
line of code, well two if you count the import then. 

Now with that, we should actually get an output for this console log statement. 

So now let's restart the server, by the way if you install a new package, you
need to restart, you can't rely on the auto-restart from nodemon and we should
configure one thing as I'm getting warned here, you should pass the config
options here and set extended to false, this is if it should be able to parse
non-default features you could say, so let's add this to comply with what we
should use here and with that, we get the body parser enabled. 

Now let's try this again and let's go back to add product and let's add our book
again, add product, we're redirected and now we see this is what we get, a
javascript object with a key value pair which also makes extracting that value
easier than we had to do before with the split function where we manually had to
create that array and so on. 

Now we get an object where we simply get the key we defined in our input here,
so this name and then the value the user entered and this is definitely simpler
than our custom approach we used before and now we can work with all the data
our users yield us, store them in the database, something we'll do later, show
them in the response, whatever we need to do. 

Now one thing of course is missing. 

This right now would also execute for incoming data request, well we only want
to listen to a post request, so what can we do regarding that? 

---