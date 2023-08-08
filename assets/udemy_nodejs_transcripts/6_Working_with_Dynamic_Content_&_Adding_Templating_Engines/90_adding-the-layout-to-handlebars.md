## 90. Adding the Layout to Handlebars

<strong><em>no description</em></strong>

Handlebars does support layouts but it works a bit differently than it did with
pug. 

First of all we have to configure something, in app.js where we register our
handlebars engine, we have to pass in some options. 

Now my IDE helps me here, if I hit control space it shows me which options I can
set and you can of course explore the official docs to learn all about them. 

Now what it allows me to do here is it allows you to set up where my layouts
live, so which folder I can find my layouts. 

Let's set this here to a string which by default is views layout so you don't
need to set this but you can set it kind of to reconfirm this but this is
redundant, you only need to set it if you would store it somewhere else, like in
lays or if you had a different default views folder. 

I'll set it to this even though that is the default so that you see that
setting, now you can also define a default layout that should be used for all
files and here I'll just name it main and that means you will have to have a
main or main layout in my case, you will have to have a main-layout.hbs file in
your layouts folder. 

So let's add a main-layout.hbs file in the layouts folder and let's set it up
similarly to the pug layout and that was of course influenced by the 404 page. 

So let's copy over the 404 html code into the main-layout.hbs code and first of
all page not found, of course we want output this dynamically here, we'll output
the page title here with the handlebars handlers. 

Now regarding the styling, in pug we defined a block where we could dynamically
add the content that should be rendered from inside the view that extended this
layout. 

Unfortunately hbs doesn't have such a feature so we can't do that, we can't
define a block here, instead the only thing we can do there is we can define a
placeholder with three curly braces, opening and closing, so not normal double
curly braces but three curly braces and then adding body here and you have to
exactly use this placeholder. 

This is understood by handlebars and you will then be able to target this in
your views that extend the layout automatically because you set it as the
default layout. 

However if you have some part like this where you need to add some styling
depending on the page you are on, you will have to solve this differently, in a
kind of a similar approach as we solved the active class here in pug, you will
have to add an if statement here in your main layout and this is of course a bit
of a more cumbersome or complex way, though you can do way more with handlebars,
you could define custom helpers that help you with that but this is beyond the
scope of this course where I just want to give you a brief introduction, so let
me show you the easiest way of solving this and this is that we add an if block
here and we check if product.css and if this is the case, let's also close the
if statement here, then I will add a link to my product.css file and I will
repeat that same logic of course for forms and again as I said, this is the easy
solution but it will do for now. 

So forms and here we have forms.css. 

So this is working now, now what regarding the active class, we also want to add
that dynamically, right? 

Well again we can simply add the class here and I add my handlebars handlers
here and I add an if statement and check if active shop is true and this is a
variable we'll have to pass into this view, if that is true then I'll add the
active class and of course also close may have statement so he can also write
this inline, that is an important take away and I'll do the same for the add
product route here where I check if active add-product is true. 

Of course we'll have to make sure that these variables are also passed into the
view at least when they're needed, if you don't pass them, they're always
treated as false, so you only need to pass them if you want to have them treated
as true. 

With that, our layout is prepared, now let's go back to the shop.js file to
start with that and as I just mentioned, we now have to pass in active shop,
this is this variable or this property we're checking for here in the if
statement and we should set this to true for this route to ensure that for this
route, the active class is added. 

So let's set this to true and therefore in the main layout, this will be true
and therefore active will be rendered, active add product would be false because
we don't pass it at all and therefore this would not be rendered. 

So that is that, now of course we also need to make sure that the product.css
gets rendered, so we need to pass in this too. 

So back in shop.js, let's also pass in product.css and set this to true, so you
can already tell, you configure a lot from inside node express when using
handlebars and that is its philosophy. 

So now with that set up, we can go back to the layout, have that finished and
move over to shop.hbs. 

Now this will use the layout by default, you could disable this by going to the
render function for a given page and setting a special layout key and setting it
to false, this is a special key that is understood by handlebars and it would
not use the default layout, otherwise it will. 

So since it will do that by default, in shop.hbs we can get rid of this entire
code here, including the header and just have in this file what should be
injected into our triple curly brace body tag in the main layout, so here,
whatever should get entered in this place should be added to shop.hbs and
nothing else. 

So with that if we save this and we go to the shop, you'll see we get an error
and the error is a bit annoying to be honest with express handlebars, it's
looking for the main layout.handlebars file. 

So it does not take .hbs here and for whatever reason, you explicitly have to
tell handlebars to do that differently. 

You have to go to the options and set the extension name which only applies to
the layout and not to all files, just as this applies to all files but the
layout, you have to set the extname here to hbs. 

This is really strange but it is how express handlebars works, so now we're
setting the extension to hbs for layouts too and now if we reload this page, we
see our normal shop page. 

And with that we can of course also go to add product, here add-product.hbs,
remove everything but the part which should be rendered in the place of our
body, triple curly brace body tags. 

And if we reload, something's missing right, do you know what went wrong? 

Well we're missing some styles and the reason for that is that we need the forms
and for this however, we need to ensure that forms css is set to true, we will
also need product css by the way. 

So in admin.js, we should ensure that when we rendered this route, we set forms
css to true and product.css, this one, product.css to true and that we also to
get that active link in the navigation, that we also set active add product to
true because active add product is the key we're looking for here. 

With that, if we save all files and we reload here, this is looking better and
now it's all working again with handlebars. 

So as you can see, handlebars uses a different philosophy, definitely something
you have to get used to, therefore your templates are leaner. 

And there is no better or worse way of doing this, it really is up to you which
one you prefer. 

Let's now have a look at a third option, ejs which is my personal favorite. 

---