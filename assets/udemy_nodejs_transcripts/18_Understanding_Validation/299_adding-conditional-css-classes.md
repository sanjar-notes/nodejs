## 299. Adding Conditional CSS Classes

<strong><em>no description</em></strong>

We're now able to keep the old user data and as you see, it was relatively easy
using that value we attribute and ensuring that we simply return the input the
user entered. 

Now obviously you can also do even more on your frontend side, for example you
could give these invalid inputs a red border, that is also something you often
see and for that you just have to keep in mind that you have to use that
information which you're getting to pass it to your view and then render
something different based on that information. 

So in our case here for example in the sign up route, we do have our errors
array here right, here where I output my errors array and that errors array
contains all the problematic fields. 

Now we then return an error message based on that array but of course we could
pass another key here, validation errors or whatever name you want and that
could be just errors array. 

So the full array is now returned as well in my render function, so now I'm
returning not just the first message which I picked to show but also the full
array of errors. 

Now as always this means that I should go to my other scenario, get sign up and
also render that, so validation errors here would be an empty array because I
got no errors and now we know it's either an empty array if we load that page
without errors or we have an array of inputs that do have well problems. 

So how can we now benefit from that array of errors? 

Well we can go back to our frontend and there, we could change the styling of
that input based on the existence of an error for that input, now how can we do
that? 

Well let me structure this over multiple lines to make it a bit easier to read
and then here on this input, we could assign a conditional css class that sets
an invalid styling. 

So we could add class here and now we use ejs syntax to output something there 
and what I want to output here is that I check my validation errors which is
that array of errors which I just talked about and there I try to find which is
a built-in javascript method we can call on arrays, I try to find an error where
error param is equal to email and keep in mind these are the error objects in
that array, they do have a param field which holds the name of the problematic
input. 

So here I'm trying to find an error for the email input because I'm on the email
input here in my html code. 

Now this will either return undefined or null if I don't find it or it will give
me that entry I'm looking for. 

So I can check if that is not false-ish, so if it is not undefined or anything
like that, then I want to add invalid as a class here otherwise I will not add
anything, so just an empty string because that should be text that is added as a
css class. 

Now with that I should get that invalid class on my input when I do have an
error for the email control. 

Now to see something, I'll go to my a public folder real quick to css and there
to the forms.css and in there, let me now add the invalid class which is the
class I just defined in my template and let's give it a border color of red. 

Now due to the way css works, I should also be more precise here and say if a
form control input has the class invalid, so this css selector. 

Let me save that and let me hit sign in again and now we see this red border
because if we inspect this element, we see that indeed the invalid css class was
added. 

And now that is a pattern which we of course can repeat in our view, we can go
or we can take that logic here for adding a class and we can add that to any
input obviously, not just to the email. 

So here I'll do it for my password and I'll simply check for the password
control here and of course you could find other ways of implementing this, this
is just one example but it is an example where we would now also mark the
password red if it is invalid and the same for confirm password of course. 

There we can also simply restructure that for readability reasons, for nothing
else than that and then simply add this css class here based on the confirm
password field. 

And now with that changed if I hit sign up here, you see these are all red. 

The password is not because it's actually valid, if I would enter a too short
one, they're all red and now this is another way of enhancing the user
experience. 

Now feel free to play around with that and find your own solutions, see what
else you can do, I just want to give you the ideas on how you can utilize that
information the server side validation package gives you and of course, you also
see how you can pass that information to your frontend. 

---