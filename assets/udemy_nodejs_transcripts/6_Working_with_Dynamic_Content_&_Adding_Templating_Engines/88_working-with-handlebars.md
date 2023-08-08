## 88. Working with Handlebars

<strong><em>no description</em></strong>

Now we had a very close look at pug as a templating engine but it's only one of
three options. 

Now this was a quite extensive look because I also explained what templating
engines are and what their core logic is, it'll be a bit faster for the two
other languages therefore or the other two solutions so let's continue with
handlebars which does not follow such a minimal html approach but uses normal
html mixed with some templating logic. 

So let's use handlebars and for this, let's go to app.js . 

and in there, we now need to change our view engine. 

Now we did install express handlebars but this actually is a package that is not
auto-installed by express, so instead we manually have to tell express that
there is such an express handlebars engine available and for this, we first of
all import it and to find out whether you do need to do this for your favorite
engine or not, you'll simply check their docs because there, this is mentioned. 

So for express handlebars, we add express.hbs, the name is up to you by
requiring express handlebars. 

So now this is imported and now we have to tell express that this exists, that
this is an engine it can use. 

We do this by calling app and now there is an engine method and this registers a
new templating engine in case we're using one which is not built-in, pug was
built-in kind of, express handlebars is not. 

So to register this, we have to define a name for our engine and you can use any
name you want though of course you should try to not clash with the built-in
engines to which you also find a link at the end of this module by the way. 

Handlebars is a name we can use for example, so let's give this engine this name
and now we just have to tell express this is the name, now what is the actual
tool I should use? 

And that is express.hbs, so that object we just imported, that just turns out to
be a function we can call and we have to call that basically initialises this
engine you could say, so this function returns the initialised view engine which
we can assign to engine here. 

So express handlebars gives us this engine and now we have to switch the view
engine here to handlebars and obviously this name here has to match the name you
set up here. 

With this you're good to go, now you're ready to use handlebars in your code. 

Now how do you use it? 

Now you do create new files for this and let's start with the 404.html page. 

I'll create a 404.handlebars page, now we have to name it handlebars here as
this is the default by express handlebars and we defined this as an engine name
here. 

You can also change the name for example to hbs, like this and now you're able
to use .hbs as an extension, so this is how that works and how you register
handlebars as the view engine. 

Now with that registered, let's use it and let's take the 404.html file and copy
its content into the 404.hbs file because handlebars uses normal html with some
custom syntax therefore there is no minimal html version as it was with pug. 

Now in this file let's remove that active class on that link in the navigation
because that's still wrong, in that file I now want to change that here, I want
to output that title dynamically so that you can see how that works with
handlebars. 

Keep in mind that in app.js where we load that 404 page, we are passing in this
data and the way you pass data into templates doesn't change with the engine,
this is always the same type of flow. 

You pass in an object with key value pairs where the keys and therefore
indirectly also the values are available in the template, just the way you use
it in a template differs from engine to engine. 

And in handlebars, we output this value here by adding double curly braces,
opening and closing and between these we add page title, so that key name for
which we want to output the value. 

And with that if we save that and we go back and reload some page which does not
exist, we should still get page not found, this time handled through handlebars
and just as before with pug if we inspect the source, we of course see no
handlebars code, the double curly braces was simply replaced with the content
that should be rendered. 

So this is how we use handlebars and now if you're feeling confident with the
help of the official docs where you learn how to use if statements and loops,
feel free to go ahead and also replace the add product pages with the handlebar
equivalents otherwise we'll of course do that together in the next lecture. 

---