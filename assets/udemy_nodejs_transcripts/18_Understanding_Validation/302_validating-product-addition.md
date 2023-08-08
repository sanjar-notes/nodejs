## 302. Validating Product Addition

<strong><em>no description</em></strong>

Now that we learned a lot about validation and sanitizing input, let's practice
this one last time for adding a product and for editing it as well and there,
feel free to again pause the video and try out some things on your own. 

Add your own first validation steps, after the pause we'll do it together of
course and you're free to add any validation that you want to add that looks
good to you for the different fields we have here and thereafter, I'll show you
my suggestion on how we could validate this, so here's your chance to pause the
video. 

Successful? 

Well let's try it out. 

We get four inputs here, title, image url, price and description. 

Now what would make sense to be validated here and again there is no single true
solution here, you can have different requirements for the app you're building. 

Now I want to have a title which should be alphanumeric, so only normal
alphabetic characters and numbers, it should at least be let's say three
characters long. 

The image url should be a valid url, the price should be a floating point
number, so a number with decimal places and the description here should also be
not alphanumeric, there should be special characters like the exclamation mark
should be allowed but it should be at least let's say five characters long. 

And with that information, let's add validation to the admin.js file which is
where we have these post routes for, whoops, for adding and for editing. 

For that first of all, let's import the body or the check function, whichever
you prefer by requiring express validate or /check and then let's add it here to
add product. 

There I'll add an array to group all these middlewares together and then I'll
validate my different inputs step by step. 

Let's first of all have a look at the views real fast, so there at the edit
product view and there we see we got a field named title, one named image url,
one named price and one named description, so these are the four fields I want
to validate, title, image url, price and description. 

So back in the admin controller, excuse me in the admin route not in the
controller, in the route, I'll start with the title. 

Now there, you're free to add whatever you want, I will add isAlphanumeric as a
validator and isLength should have a minimum length of 3 let's say. 

We can also add some sanitization and trim excess whitespace at the beginning or
the end of the title. 

Now this is the title I want to validate, I'll now copy this and continue with
the image url, however there I will check isUrl, that is the only thing I want
to validate there, that this is a valid url and that is another built-in
validator that checks whether this fulfills the characteristics of a url, then
I'll add my validator for the price here. 

Now for the price, I want to have, I could check isNumeric to allow either
integer values or floating point numbers  But there also is isFloat to ensure
that this has to have some decimal places. 

Now I'll add my last validation here and that will be on the description and
there, I just want to trim that and have a length of at least let's say 8 or 5
characters, whatever you want, you could also add a max value of course, let's
say we have a max of 200 or 400 characters, something like that. 

Now I added validation to adding a product, I'll already copy that and add it to
edit product here, to the post route edit product as well, so there I edit the
exact same fields because we'll be editing the exact same fields there so I want
to have the same validation in place. 

Now with that in place, let's go to the admin controller and make sure we
collect these validation errors and return them. 

For that we'll first of all import something from the express validator by
requiring express validator /check and there, I want to import the validation
result function. 

And in post add product, here before we create that new product, I will actually
collect all my errors by passing the request to validation result and I'll then
check if not errors is empty which means we do have errors and in that case, if
we make it into this if block, I will actually render my edit page, so here on
get edit page, I will call this render function here in the end but I'll do that
in this if block I just edit. 

I'll also set this status code of 422 which is a good practice for indicating to
the browser that some data that was passed was incorrect. 

I'll have add product as a title and now if we have a quick look here at edit
product, we see that there we already set the value if editing is set to true
and then we output product title, product image url. 

Now we can tweak this a little bit, I'll still set editing to false because we
still are not editing and I don't want to change anything else on the page but
what I will do is I'll set my product here equal to an object where I do set the
title and so on to these fields, to these inputs which I did fetch. 

So I'll set the title, the image url and also the price and the description to
these fetched inputs so that we can use that old data in the way we are already
using it but I'll now add another field here, hasError maybe and I'll set this
to true here. 

Now that simply means that I should ensure that hasError is also set in other
places where I render this page, like here where I set it to false for get add
product and for get edit product down there, I will also set it to false, so
it's only true right now if I'm in the if block of my post add product route
here. 

Now in my view I can now take advantage of this new has error field and I can
say I want to output the existing product title if I'm editing or if hasError is
true, so that is my alternative condition here to ensure that the old data in
this case then is output like this. 

Now of course it would also be nice to display some error message, so we can
grab that from the login page and check for the existence of error message here
above my form and output it if we have one, this just means that again back to
my routes and not to my routes, to my controller in the admin.js file, we should
have an error message which simply is null by default. 

And here in my if block where I do have validation errors, I will set the error
message to errors array, the first error which we are guaranteed to have and
there the msg property property as we did it before and of course I'll also set
error message here when we get the edit page, there I set it to null. 

And now with that, if I hit add product here, I get invalid value because I set
no custom errors but it did to re-render this and if I enter first book here,
then this is also kept if I click add product, it still gives me that default
message of invalid value because I never set my own one, you could of course do
that with the techniques I showed. 

We also have no red borders because we didn't add that logic yet but it is
reloading the page, it's not submitting the request and it's keeping all the
data which we did input right, so this is not thrown away and that is of course
worth a lot. 

We can of course also edit products and for this, let me quickly add a valid
product, this also allows us to test whether this works. 

And it looks like it failed but actually if we go back, we see we get a double
headers sent error which is stemming from my admin controller, I should return
this otherwise after sending this error response, we continue with the rest of
our code which I don't want to. 

So now if I hit add product here, this still fails though. 

The interesting thing is if I go back to my products collection, first book was
added before though, well that was added because I did not return in case of an
error as I'm doing now, so now the returning works but still I get this invalid
value and if we want to find out for what I get it, I can log errors array here
so that we can have a look into this errors object. 

If I add this again, now it fails of course, we see it's the title. 

The title failed somehow, the title somehow is valid in a way that tells us that
it does not fulfill our criteria and the title for adding a product should be
alphanumeric, have this length and be trimmed. 

Now the thing is my alphanumeric check, the whitespace here is neither
alphabetic character nor a number, so maybe we should just check if it is a
valid string because that will allow whitespace as well and now if I hit add
product, now this succeeded and it did add it therefore. 

So now I've got two first books here, let me delete this real quick. 

Now if I try adding this again though, maybe a second book, it does work and now
it also shows that image correctly, so seems to have been a bug. 

So this is now working, now we added validation for adding this and how is it
for editing? 

If I add an exclamation mark here, this is accepted, we see the exclamation mark
up there and if I now enter something incorrect like the price is missing, well
then this seems to break it doesn't continue and indeed I do have an error down
there which makes a lot of sense because what didn't we do yet? 

Well we didn't add our error collecting and error returning to the edit route,
we only worked on add thus far, post add product. 

So in the next video we'll take care that for editing a product, we also get
validation errors instead of a broken app when we do submit invalid values. 

---