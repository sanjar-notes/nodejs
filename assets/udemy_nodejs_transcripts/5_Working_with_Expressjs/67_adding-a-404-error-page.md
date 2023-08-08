## 67. Adding a 404 Error Page

<strong><em>no description</em></strong>

Now one thing we did in the last lectures is we used the express router and
right now, we have a set up where we also have some unhandled routes. 

If we enter some random string here, we get this error. 

Now typically, we would want to see a 404 error page and we can do that. 

Back in the app.js file, we can take advantage of the middlewares or the way
express uses the middlewares and funnels the request through them. 

Remember that the request goes from top to bottom so if it finds some middleware
that handles it, it will go in there and then for example here for slash with
that get method on the router, we would actually end here, we also get no next
call here so no other middleware would be executed. 

But if we got no fitting middleware and we don't have one here, then we actually
make it all the way to the bottom and eventually we don't handle that request. 

So to send a 404 error page, we simply have to add a catch all middleware at the
bottom where we don't need a path filter but we could add slash but that's the
default anyways  and then simply handle request response next since I use use
here, this will also handle all http methods, not just get requests and there, I
can then also send some code like Page Not Found. 

So little dummy html document and maybe we also want to set the 404 status code
and you can do that by chaining another method prior to send and that is the
status method and of course you cannot just use that here, you could have used
it here or in the admin.js file too. 

So always before sending, you can call status to or set header, you can actually
chain all these method calls, send just has to be the last one. 

So here I'm calling status to set my status code, another convenience method
added by expressjs and I'll set it to 404 which is the common code for a page
was not found. 

With this added, if I save this and then I now reload my dummy path here, I get
page not found whereas for add product, I still get that form, so this is still
working, the rest however changed. 

---