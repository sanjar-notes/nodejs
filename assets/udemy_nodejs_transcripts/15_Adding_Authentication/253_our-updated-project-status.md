## 253. Our Updated Project Status

<strong><em>no description</em></strong>

So let's dive back into our project and make sure you are logged out and make
sure you download the attached snapshot because there I did add a sign up link
to our navigation bar and if we click on that, we also load a sign up page where
we should edit the caption of the button by the way. 

So if you download the attached code, what was added and you can also add this
to your own project. 

I did add the sign up.ejs file where I also should change this to sign up, so
you can simply add that file to your auth folder. 

I did manipulate or change the navigation.ejs file, there what I did add is I
simply added the sign up navigation menu entry after login, both for the normal
menu and also for the mobile menu down there, so basically one list item was
added to each menu, this is what I added in this file. 

And then I worked on my routes, there I added two new routes, posts sign up and
get sign up where I use my auth controller get sign up and post sign up actions
and in that controller, I worked on these actions. 

I added posts sign up which is an empty placeholder, nothing in there, so that
is not that difficult, get sign up also is is a pretty simple route, there I
simply render the auth sign up view. 

So you can just add this to your existing project or use my attached snapshot
and replace my mongodb url with yours and once you got all that, you should be
able to have a running application that looks like this with a sign up page that
looks like this because now we will use or we will need a way of signing up
users. 

So let's now start implementing the full authentication flow in this module and
for that, we'll first of all make sure that we can create new users, then that
we can sign users in and sign users out of course, that we can then use the
information whether a user is signed in or signed out in all our views and that
we can protect our routes on the server side too because right now even if I'm
not signed in, what I can do is I can manually visit admin add product and this
works. 

So I can't get there by menu because we hide the menu options but manually
visiting this works and this is also something we'll work on in this module. 

So let's get there step by step and let's start by adding user sign up in the
next lecture. 

---