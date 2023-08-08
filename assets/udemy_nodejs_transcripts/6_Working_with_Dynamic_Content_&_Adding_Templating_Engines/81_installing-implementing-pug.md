## 81. Installing & Implementing Pug

<strong><em>no description</em></strong>

So back at the project, let me quit the development server because now I need to
install another package and I will simply install these three templating engines
so that we can work with them. 

So let's install them with npm install --save because all three engines are part
of our node code and ship with the code we deploy on some computer in the end,
so let's install them as production dependencies and there we need to install
EJS, that is the package name and links to the websites of these packages with
more documentation can also be found in the last lecture of this module. 

So EJS, then we also got pug and handlebars, there is a handlebars package but
that's actually the wrong one, we need express-handlebars here because this has
built-in integration with Express, EJS and pug already have that built into
their core packages you could say. 

So let's now hit enter and now these three packages will be downloaded. 

Now what you can also see here by the way is that you can of course install
multiple packages at once by simply repeating or by adding all the names after
npm install, now the packages are installed and we'll not use them all at the
same time but one after another so that we can have a close look at how they
work and let's start with the most exotic package, pug. 

To use that, we have to go to the app.js file and now we have to let expressjs
know and that is an express feature, not node by the way, another strong reason
why we want to use express because with node, standalone node, this will be
harder, you would have to do all that manually, here we can just tell express
hey we got a templating engine that is express conforming and that is the case
for all three we installed so please use it to render dynamic templates. 

We do that by going into the app.js and after we created our express app here
and stored it in the app constant, we can set a global configuration value. 

Now what is that? 

App set allows us to set any values globally on our express application and this
can actually also be keys or configuration items express doesn't understand, in
that case it just ignores them but we could actually read them from the app
object with app get and this would be another way of sharing data across our
application but not really something I'm interested in here. 

What we can do is we can use a couple of reserved key names here, so
configuration items we can set that do lead to expressjs behaving differently
and you see a list of all these items here in this table. 

Now most of them don't really matter for us here but feel free to browse through
that, interesting for us is the view engine and the views key. 

View engine allows us to tell express hey for any dynamic templates we're trying
to render and there will be a special function for doing that, please use this
engine we're registering here and views allows us to tell express where to find
these dynamic views. 

So what we can do here is we can app set and set the view here, view engine to a
string, pug. 

Now you can't enter anything here, we use pug here because we installed the pug
templating engine and this engine actually ships with built in express support
and auto registers itself with express so to say. 

So that is why this works, it doesn't work for all engines but you'll find more
in the links in the last lecture, here it does work, pug is supported out of the
box and with that, we're already set to go. 

We can set an additional configuration though, we can let express know where to
find our views, however the default setting here in this last column, the
default setting for views already is our, basically our main directory and then
the views folder, still I'll send it explicitly here to show you how this would
work if you would store your views in another folder which is not called views
but maybe templates or whatever it is, that you have to set this configuration
item here, whoops this one and here, I will set it too even though it wouldn't
be needed because views is the default. 

So now we're telling express that we want to compile dynamic templates with the
pug engine and where to find these templates. 

The last step of course is that we add templates, so let's go to views and let's
add a shop.pug file here. 

So we now have a templating file and now pug actually works different to normal
html, so I can't just copy over this whole html code. 

The good thing is however in my IDE here if I type html in the shop.pug file and
then I use this html5 template, I get a pug structure of this and here we
already see the minimal html syntax. 

We get no normal html tags but keep in mind that the pug templating engine will
compile our code to normal html in the end. 

So this here is basically the equivalent to this part here you could say, except
for the stylesheet imports. 

If we wanted to add these, we can do that here too and thankfully, the IDE helps
me here, if I type link and hit tab, I get a pug conform implementation of this.


So here I now can also add my links, the paths of course to the css files are
the same as before. 

So this is now how we installed pug and how we added it, now let's quickly
finish this file to look like this file before we then actually have a look at
how we can add dynamic content. 

So let's replicate this link here and import the product.css file and now for
the body, here I got a header and I got this main area, so let's replicate this
in pug quickly. 

For this in the body, indentation matters in pug that's important, you basically
structure your nesting of html with indentation levels here, so if head is
nested in html then it's indented and if meta is nested in head, it's also
indented. 

If they're on the same level, they are siblings, so this is how that works. 

So if you want to add something into body and not next to it, we have to indent
here and then I add my header which has this main header class, so if I type
again another useful feature of the IDE, of visual studio code, if I type dot
and then the name like this and I hit tab, then this looks like it didn't do
anything but actually this is the representation of a div with this class, now I
want a header with this class so I just write header. 

So this strange syntax will create a header element with this css class and this
is something you have to get used to and where I strongly recommend diving into
the official pug docs if you want to stick to that, here by the way, I'll
replace the title with my shop. 

So let's not just add the header but also nav, unordered list and so on. 

For this in the header I want to nest something, so let's add an indentation
level and then unordered list dot and the class and now the same, whoops that
was nav not unordered list so that should be a nav item. 

Now for the unordered list, let's take that class, let's go in there and it
should be nested in the nav. 

So let's indent, unordered list dot class name and now we get the list items, so
here let's again pick the list item here or the class on it, indent because it's
nested in the unordered list, list item dot and then the class. 

And now last but not least, I have the anchor tag which also has the active
class but which then also should have some text content in it and then also have
a link. 

So let's now go in there, nest this anchor tag and the class, if you hit tab,
you automatically, this is the attribute notation, so in parentheses after the
anchor tag or after any element but always without any whitespace in between,
this allows you to add attributes onto the HTML element, so here this should go
to just slash and now for the text content, you could add this next to it, so
shop like this. 

This will basically place this text between the opening and closing anchor tag. 

Now this is the setup I want to have here, of course we have two list items, we
also got add product which leads to this link, so I have to replicate this. 

So next to the first list item, I add another one, main header item and then I
have my anchor tag, this one without the active class, just with the link and
there, I'll say add product. 

With this if I run npm start, we wouldn't see anything and I am aware of the
fact that I didn't add the main content but let's ignore that for now. 

With this however, we wouldn't render this template because we're not telling
express to do so. 

We're telling express that it should use this templating engine whenever we try
to render a template but we don't try to do that. 

So in shop.js where we do define what should be our response, we have to change
the response because right now, we're sending the html file, now we want to do
something else. 

We can use response and then there is a special render method, this is provided
by expressjs and it will use the default templating engine which is why we had
to define it here, it will use that default templating engine and then return
that template. 

And now we defined that all the views are in the views folder, we also don't
have to construct a path to that folder instead we can just say shop. 

We also don't need shop.pug because we defined pug as the default templating
engine so it will look for .pug files. 

With this if we save and we reload the shop page, we see the header, we don't
see the main content because we didn't add this but the rest is working just
fine. 

And if you inspect this or view the page source, you'll see this is normal html
code, so it's not our minimal version which the browser wouldn't be able to read
anyways but it is the html code pug generated for us based on that minimal
version. 

Now one thing we're not doing here is we're not outputting anything dynamic but
since that is the reason why we added templating engines, let's do that too in
the next lecture. 

---