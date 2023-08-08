## 304. Wrap Up

<strong><em>no description</em></strong>

That's it for this module. 

We added a bunch of validation logic for signing up, logging in and creating
products and you learned that this is a two step process of adding validators to
your routes with that third party package we're using, express validator so that
it's a two step process with adding these validators to the routes as middleware
and then for this package we collect errors in our controllers and then we do
something if we do find errors. 

Most commonly you would re-render that form page, so that page which wanted the
user to input something and to provide a good user experience. 

You want to make sure that you keep the original input the user entered and that
you show at least some error message that gives the user an idea that nothing
was wrong on your server but that something was wrong with the user input
instead. 

These are the core takeaways and other than that, I can only encourage you to
play around with the different built-in validators, build your own ones and of
course there are other solutions, other express or node packages for validation
out there as well. 

This is a pretty popular package, pretty easy to use and I can only recommend
using it but as always it's most important that you play around with these
things and that you practice using it. 

---