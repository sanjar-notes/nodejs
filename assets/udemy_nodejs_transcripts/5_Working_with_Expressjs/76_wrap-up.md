## 76. Wrap Up

<strong><em>no description</em></strong>

That's it for this module. 

It was quite a lot, a lot about middleware I guess but it is the crucial basis
for the rest of the course where we will of course continue with nodejs but by
using expressjs, a powerful framework and that is what expressjs is. 

It's a nodejs framework, so you still use nodejs, we for example still use the
path core module in this module but you build up on it and get a bunch of
utility functions and a clear set of rules on how you should structure your app
and it's all about middleware and understanding that flow of requests through
all the middleware functions. 

Expressjs is very popular because it's highly extensible and as you already saw
with the body parser in this module, you can easily plug some packages, a lot of
packages actually into an express app because they just expose such middleware
functions and you can therefore easily add them and the request gets funneled
through them. 

Now that concept of middleware is really important, middleware functions are
these functions that took the request object, a response object that helped you
with sending a response and that next argument which turns out to be a function
you should call to forward a request to the next middleware in line and in line
means from top to bottom in your root file. 

This is a crucial point you have to understand, that you should always call next
unless you are sending a response in which case you should never call next and
that you can therefore cleverly structure your middleware to transform a
request, read something from it and send different responses depending on the
route you're accessing, so depending on the path and method you're sending. 

You learned that you can filter request by path and method easily with app use
by adding a path or app get, app post and that if you filter by method, like if
you had app get, that the paths would then be matched exactly otherwise with app
use, the path you passed would only be matched with the beginning of the url,
the part after localhost. 

You also can use the express router package instead of app use, app get because
this allows you to elegantly split your routes across multiple files since the
router you export there can be added as a middleware function into app use in
your root file. 

Last but not least, we also served some files and it's important to know that
you're not limited to serving dummy text or anything like that, you can send
files for example as we did it with html files and if a request is directly made
for a file like a css or javascript file but also images even though we didn't
see that in this module, you can enable static serving for such files with the
help of express static which is a crucial part of any web application you're
building because you typically have such files that are dependencies of your
html files for example and this is the core basic knowledge you should have
about expressjs, this is what we'll now build up on and this is where we will
now dive deeper into to learn how to render dynamic content, how to access
databases, enable authentication, manage data on the server and so much more. 

So let's continue. 

---