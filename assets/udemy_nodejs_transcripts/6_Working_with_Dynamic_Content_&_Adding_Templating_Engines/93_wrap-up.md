## 93. Wrap Up

<strong><em>no description</em></strong>

So it's time for a quick summary and clean up, first of all let's clean up. 

Since we're using ejs now, we don't need the layouts folder because we only use
that for pug and handlebars,  so let's delete layouts here. 

We also can delete all hbs, html and pug files here because we don't need either
of those, we just use the ejs files now, so let's delete all these files. 

Now this is much cleaner and now I just want to make sure that you really
understood the flow of how data flows into the templates and what the templating
engines do. 

We do render a template with the special render method provided by expressjs,
that render method will always look for the registered view engine, something we
do here at the beginning in app.js. 

We do register our ejs view engine in this case by setting this special view
engine configuration, a reserved configuration key which is understood by
expressjs. 

We also tell expressjs where our views are to be found though that actually
would be the default setting here by the way, so you don't need to add this if
you do use the views folder. 

With that, expressjs . 

will render, will take our templating engine which we still have to install
separately as a npm package keep that in mind, we did install ejs as we did
install pug and handlebars and then you always just refer to the name of your
view, like we do here, add-product.ejs, by the way if that were in a subfolder,
like products, it would simply refer to it like this. 

But then you just refer to that view without adding the file extension and you
can also define an object which will hold the data that is passed as variables
into that template, so not the entire object is passed in there as you learned
but instead, you will have a page title variable available in the template,
you'll have a path variable available in the template and so on and this is why
we can use something like this here. 

This is now syntax understood by the specific templating engine we're using, ejs
in this case. 

It simply detects these tags here and then it simply looks for a variable named
page title and tries to output its value, well and finds the page title because
we do set a page title property here. 

And we got more features than just outputting values, as you can see in the
shop.ejs file, we can also use if statements or for loops and you learned the
different versions of this for the different view engines in this module. 

So this is how the templating engines work, what they do and why you use them
and it's important to keep in mind that in the end if you inspect the source
code, you always just get back normal html code, you don't find any ejs code in
here or any javascript code. 

This is just html code that is generated on the fly but also on the server. 

This is not code that would be generated in the browser,  it's generated on the
server, on demand for the request you're getting. 

And templating engines also do some advanced stuff like caching some built
templates for you if the data input didn't change, so that they can return the
template even faster and don't have to rebuild it for every request even if the
data didn't change. 

But that some behind the scenes stuff, for you it's important to understand the
general flow. 

---