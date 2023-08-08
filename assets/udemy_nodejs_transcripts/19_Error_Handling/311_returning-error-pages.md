## 311. Returning Error Pages

<strong><em>no description</em></strong>

I added this throw new error in app.js and to show you what it does, let me go
to another place, to admin.js, to the controller and change some code there. 

In there we of course have plenty of code to for example add a product and we do
validate the user input which is also a form of error prevention or error
handling, we do validate that input in admin.js in the routes folder, there we
added all our validation logic. 

Now in admin.js, I'm extracting my logic. 

Now let me force an error by quickly looking into my database with compass, the
graphical user interface we used before for interacting with the database and in
there, in the shop database, let's go to products and let me pick up product ID
here. 

Now when creating a new product, I will also add _id and I will temporarily
import something from the mongoose package because I want to create a new object
id here and I can use mongoose types object id here, pass my object id and add
the new keyword and now I will basically create a new product with an ID that
already exists and therefore this should fail. 

Now let me start my application and let's quickly log in with a user here and
add a product and here you can enter anything. 

Let's click add product here  and now it will fail, you've got this infinitely
spinning refresh icon and if you have a look at your code or at the terminal
where you ran npm start, you will see that our server crashed because mongodb
threw an error with a duplicate key problem which makes sense because we added a
product with an existing ID and therefore everything crashed. 

Now of course this is a constructed scenario but just because I want to ensure
that something goes wrong at this point because now I want to show you how you
could handle such a problem. 

Now we are logging that error and I can confirm that this catch block is called
by adding console log an error occured. 

So now if I save this, obviously our node server restarts, let's add a product
again or let's try this again, it will fail again of course but if I click add
product now and I go back to my code, we see an error occurred here, so this
proves that this catch block gets fired but that's great because this means that
we now have a chance of handling that error. 

Now what we could do here of course is we could return some 500 error page, we
could also redirect the user to any other page or we could render the add
product page again, we could even keep the old input and that might make sense
if we expect this to be a temporary issue. 

So of course we could take our code from validating, copy all that and output it
here or  use it here in the catch block, set a status code of 500 which is a
code indicating that a server side issue occurred and then we want to return
added product with add product page title, add product in the path, by the way
it should be fixed up there too, minor thing but make sure that the navigation
item is selected. 

Editing set to false, has error can be set to true, the error message we can put
our own error message here, something like database operation failed, please try
again. 

Validation errors can be an empty array, we don't want to put a red border
around anything and we want to keep the user input. 

If we save this and everything restarts, let's try this another time. 

So let's add a new product here like this and if I click add product, indeed now
we have a better error handling because now I am returning that same page, I
give the user some error message and the user can try again but of course this
here will keep on failing because we have a fundamental problem in the code. 

But if that was a temporary network issue, this might be a fine way of handling
this. 

Sometimes you got bigger problems though and you don't want to use this
solution, you don't want to return the same page again, instead you really want
to show an error page to show the user something bigger is wrong, we're working
on it but for now you'll probably not be able to continue. 

And for such scenarios, I'll add a new view next to my 404.ejs file, I'll add a
500.ejs file. 

We actually already have a view for error handling, the 400 page, 404 page, now
I'll add another page that will render error messages for bigger technical
issues, not for not found routes. 

I'll copy the code from 404, include it in 500 and there I will say some error
occurred and there may be some paragraph, we're working on fixing this, sorry
for the inconvenience, something like that. 

You could add anything you want here. 

Now we have that 500.ejs route and that might be something you also want to do,
in cases where you are not sure if you will be able to handle this otherwise. 

Now to return this 500 page, I'll go to my error.js controller and I'll
duplicate my get 400 route and add the get 500 action here, with status code 500
we render the 500.ejs file with a page title of error or whatever you want, path
can be /500 and  isAuthenticated, yeah we use our session information for that. 

Now we have get 500, we just need to add a route for that now. 

So let's go to the app.js because in there, I use get 404 for every page, for
every middleware that does not get handled ahead of time. 

Now there is one extra route I will add with app get/500, here I want to use
error controller get 500. 

So now I define a route like this, /500, I now just have to make sure that we do
redirect to that route when a 500 error occurs and we want to show that page and
therefore in the admin.js in the controller, in the catch block, I will indeed
redirect to /500. 

And now if we save that and I try submitting this again, I end up on my 500
error page and this can be a decent way of handling this for bigger problems. 

---