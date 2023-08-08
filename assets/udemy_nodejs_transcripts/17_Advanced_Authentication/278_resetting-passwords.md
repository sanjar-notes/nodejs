## 278. Resetting Passwords

<strong><em>no description</em></strong>

So let's start with resetting passwords. 

Obviously, that's a common thing you need to do in applications. 

People forget passwords. 

You want to offer them a way of resetting them. 

For that, we will need a new view and some new routes. 

Let's start with the view. 

Maybe so in the off folder I'll add a reset Edge's file. 

You can name it however you want. 

You could name it password reset edges, of course, and I'll copy my login Edge's
code paste it in there, but of course adjust it a little bit. 

I'll still leave the error message here because eventually I might display one. 

I don't want the password field here, but I need to see a xref token and I need
to email field because I want users to enter an email for which they want to
reset the password. 

Then here I'll label this button reset password like this. 

So now we have that reset Edge's view. 

Let's now go to the off controller file and add some new actions to it. 

So we'll export a new action, which I'll name get reset that should simply
render that reset page. 

So here we have the well-known function with the free arguments. 

And in there I'll use response render and we'll render a page just as we did it
many times before. 

So I'll just copy that from up here to type less, render a page off reset is the
view path here. 

The path in the URL will be just reset. 

Let's say title of the page could be reset password. 

Now regarding the error message, I'll also copy that this code here where I
extract any message that might exist and pass it to The View. 

And with that we got the controller action. 

Let's now create a fitting route in the off routes file here. 

I will add a new get route to slash reset and use off controller get reset here.


This is the route I want to load when we request the password reset. 

With that, we just need a way to reach that route and that would be on the log
in page. 

Of course there below the form we want to offer a reset password link. 

So here I'll add a new link which leads to slash reset where I say reset
password like that. 

Now let's all wrap that in some diff. 

And give this death a class of centered. 

This is a class I defined earlier in the course. 

Now back on the login page. 

If we reload it, we have reset password here. 

Now you can work on the styling if you want. 

The main thing is if I click on it, I'm taking to my reset password page. 

Now in here, the idea would be that you enter a password and then you receive an
email with the password reset link. 

Now let's start working on that in the next lectures. 

---