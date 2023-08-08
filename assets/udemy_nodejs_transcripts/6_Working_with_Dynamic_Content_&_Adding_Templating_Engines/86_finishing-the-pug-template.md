## 86. Finishing the Pug Template

<strong><em>no description</em></strong>

Let's make sure we do set this active class on the right link depending on which
page we are. 

Now for that, I will go to my routes and there since I'm working on the add
product to the admin.js file where I do have that add product route, this one. 

Now I will return a new field here, the path field and I will set this to admin
add product. 

Now you can set this to whatever you want, it doesn't have to match the path
this route has, just a pattern I like. 

So now I pass this path into my view so that the view can find out what is the
path for which this was loaded. 

Now in main layout, we will get this path and now I can do something
interesting. 

In the main layout here, I know that I want to add the active class to this add
product if the path and the path now simply is a variable i get passed into the
page, if the path simply is this one and that is something we define and
therefore you could pick any path you want. 

So now I will add a check here. 

Now a class can be added, a css class as an attribute here too, you don't have
to use that dot notation, so class is equal to and now I'll have some javascript
code which we can enclose with brackets here and now here, I simply check if
path and path is simply just what I pass in here, so this key, if path is equal
to this value and that is why I meant you can use whatever path you want, you
are defining the condition here. 

So if path is equal to this, then I know that add product is the page I'm on
because only for the add product route I do set this path. 

So then if that is the case, I want to render active as a class here otherwise
an empty string, so otherwise I basically set no class. 

With this set up, now if I reload this page, you'll see add product is yellow
because now it is marked as active, if I go to shop that's not the case but on
shop, we also don't use the layout yet. 

So let's continue now. 

For the shop I also want to use the layout, so I will go to add-product.pug,
copy my code here and move it up over to shop.pug, let's keep the original code
for now, extend the main layout therefore. 

Now I do need the product.css file here but I don't need the forms so let's
remove that from the styles block and for the content I will need main but we
don't render a form here, instead we render this if loop, so let's or this if
block, so let's copy that entire code and put it in here, make sure indentation
is correct that you don't mess this up and now we can get rid of all the other
code here. 

Now again for the styling of the header, we would have a problem if I now reload
because it's not marked as active because I need to use that same approach I did
for the add product route. 

I pass in an additional key path and there, I pass slash like this or /shop,
again you don't have to use the real path that led to this route. 

I'll use slash though to keep this matched and now in main layout, I copy my
code from down there where I dynamically add this class and add it here for the
shop too but the part I'm checking for is just slash here and now I do add
active here if the path variable which gets injected into the template matches
slash which is only the case for this route. 

So now if I save this, I got an error here yeah this should not be an equal sign
here, this should be a colon in shop.js . 

because we're creating a javascript object and now if I reload here, this is
active, this is active  and if we try adding a book, this also works. 

So this is now working. 

Now there is one thing I saw that I forgot and that is the title for the page,
it's always page not found and that should of course not be the case. 

Now you could turn this title into a block which you then set from inside the
template or you do add a dynamic output here with hashtag curly braces and give
this a name, page title maybe and now you just need to make sure that every
render function passes in a page title. 

So for the 404 page, for the add product page and the shop page, we have to pass
in that page title key. 

So starting in admin.js, here we already got page title so we're fine, in
shop.js here it's doc title so let's rename this to page title to be in line
with the other file and with our layout and in the app.js file where we have our
404 route, I'm not passing anything so there let's also send some data into the
view and let's also set page title here, page not found. 

If we now go to our page and reload it, we see shop here as a title, for add
product we see add product and if we enter something random here, we see Page
Not Found. 

So now this is working and now we're using pug. 

Now you can do way more with pug and you can combine all these features and do
crazy stuff, I recommend diving into their official docs if you plan on using
that, I instead want to show you the alternatives too now that we learned the
basics of how templating engines work and how you can use them to output dynamic
content in your views. 

---