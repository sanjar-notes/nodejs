## 376. Adding Server Side Validation

<strong><em>no description</em></strong>

So validation in the database is missing. 

Now I'll start by adding validation here and for that, I'll quit my server side
npm start process because I need to install a new package and I'll use the same
package which I used in the validation module of this course. 

Therefore you should definitely watch that module to learn how validation works
because I'll not repeat everything here, we already learned it after all. 

So here I'll just install that package which was express validator, that is a
package that helps us with implementing validation into our node express
applications. 

After that is installed, you can restart npm start and now do you remember how
you add it? 

Have a look at this module I just mentioned if you don't. 

You go to your routes and there, you add some middleware which does that
validation. 

For that, you first of all need to import something from the express validator
package and there from the /check sub-package and that something is either the
check method or the body method to check the request body or with the check
method also the headers, the query parameters and so on, I want to check the
request body here. 

Now for a get route, validation makes no sense because no data is submitted but
for the post route it makes sense and there I'll add an array of middleware that
will be applied which will be related to validation. 

There for example I will use body to check the title field. 

Now the title field can be validated in any way you want, I can tell you that on
the frontend however, I am validating that title field and you can see that in
the components, feed feed edit component, that I am validating this to have a
minimum length of five characters and to be non-empty which is of course the
case if it is at least five characters long, the content also has to be five
characters long. 

So that's just a little side note on what I'm doing on the frontend and the
backend should of course meet that same pattern. 

So my body title will first of all be trimmed to not have any whitespace in
there and then I'll use the isLength validator with an object to set a minimum
length of five. 

Now this is the title, now after a comma, I'll add my next middleware where I
will validate the content, we can also trim that and basically set the same
validator, obviously you can be more creative than that but I just want to
re-iterate how validation works and really show you that it works in exactly the
same way in rest APIs because you build a normal node in express application in
the end, that does not change here. 

So with that, we added these two validation steps for our incoming data, for
title and the content and now we can implement some logic to send an error if
our server side validation logic is not met. 

For this we go to our controller, to the feed.js file in our controllers folder
and there we also need to import something from that express validator package,
so here I also require express validator/check and that something which I am
importing here is the validation result function. 

With that imported in create post, we can simply create a new errors constant
and use that validation result function on the request, it will then
automatically extract any errors that validation package gathered and we can
check if not errors is empty which means we have errors. 

If that is not empty, we have errors and then I will return a response with a
status code of 422 which is of course our validation failed status code where I
send some json data and there you can have a message of validation failed,
validation failed, entered data is incorrect or whatever you want, it will be on
your frontend to do something with that message or not and you could add the
errors here by using that errors constant and then using the array method to
extract an array of errors and also add this to the json object. 

So with that, we're returning this response if validation fails. 

Now thanks to our client side validation, with the correct rules we could not
reproduce that because I'm already checking for a minimum length of 5 on the
frontend but if we increase the title minimum length to 7 for now on the server,
now if I go back to the frontend and I enter a title which is only 5 characters
long and therefore long enough for the client side validation but too short for
the server side validation which is of course a mismatch you don't want to have
in a real app but it's great for testing, if I do that and I accept here, I
actually get an error, creating or editing a post failed, that is an error
message I'm just showing on the frontend. 

But if you have a look at our console log in the dev tools, we see a 422 error
here and if we click on that we're taken to the network tab, we see that read
request and if we inspect that, we see our response here and that indeed has
that message we sent on the server side, validation failed and so on and it has
this errors array where we see that the title failed. 

So you see that the server side validation is working and that is all I wanted
to show you here, of course I revert back to 5 characters minimum length on the
server now too so that the client side validation logic and the server side
logic are in line otherwise we would have very bad user experiences because
users get the feedback that their input is correct and then the server would
throw an error. 

So with that, we added validation for this post route and now we can move on to
adding a database. 

---