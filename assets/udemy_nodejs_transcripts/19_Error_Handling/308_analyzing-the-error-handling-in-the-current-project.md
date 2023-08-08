## 308. Analyzing the Error Handling in the Current Project

<strong><em>no description</em></strong>

So in our application, we get a bunch of error handling in place already, let's
start in the app.js. 

There I do already handle the case or I do have a catch block at least where I
try to fetch my user at the beginning of the request and fetch the user from a
session and then store that user object, still we can improve that and we will
improve that in a second. 

In my controllers, I also have some error handling, let's say in the auth.js
file. 

There I do check in login whether this email address does exist and if not, I do
already return the same page with an error code actually where I do pass that
information that the input was invalid. 

We do the same with the validation logic we added earlier by the way, here in
the routes where we use the express validator package to add built-in validation
functions, so built into that package. 

There behind the scenes, this package also throws and handles errors and allows
us to simply collect all these errors which are now not these technical error
objects but which are simply, which is data managed by that package, we collect
these errors here and then we handle them manually. 

That would be the right side of this slide here because there, we handle errors
manually or we added an if check where we check if data we got is enough to
continue or not. 

We get no technical error being thrown here, these technical errors by the way
can always be seen if you have an error message down there in the terminal, we
have no such error but we still have invalid code and therefore we check this
manually and proceed on our own. 

In our custom validators however, if we have a look at that, there I do throw a
technical error for example when passwords do not match. 

Now this error would normally bubble up and would be handled by express but this
express validator package happens to also handle it. 

And now it's this error handling which I want to dive into first before we then
start implementing proper solutions for the different kinds of errors we could
have. 

---