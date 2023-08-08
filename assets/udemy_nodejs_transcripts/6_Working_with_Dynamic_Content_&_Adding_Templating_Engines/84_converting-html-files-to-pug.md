## 84. Converting HTML Files to Pug

<strong><em>no description</em></strong>

So let's convert all these html files to pug templates now and for this, I'll
start with add product and create an add-product.pug file in the views folder. 

Now again I will create a html5 skeleton with the help of emmet here by typing
html, selecting that html5 template here and hitting tab, so this already gives
us a nice start. 

Now I'll set the title to add product and now I want to convert this form to pug
and of course the header too. 

Now the header is something we already got in the shop so we can just copy that
here, move it over to add product in the body like this, just make sure that you
move the active class from the first anchor tag to the second one because now
this is the active route and of course I also want to add my main section with
the form now. 

I'll again reverse engineer it by copying the main html code, going in there and
next to the header, I want to add it. 

Main is now just main, the form then is nested in that so let's indent it, the
form has this class so let's chain this and the form also has attributes so
let's add them here as a comma separated list in brackets. 

Now we can indent the div here because that is of course nested in the form, the
div has this class and you learned that a div can also be omitted then so you
can just have dot and the class to render a div. 

And then in there we have the label, the label here has an attribute, so let's
add this and it has some text which is separated with a whitespace as you
learned. 

Now we also have an input here, input of type text so let's add these brackets
set here to render some attributes separated with commas and the id can actually
be rendered separately with a hashtag in front of it, again using its css
selector, something you already solve for the class, this also is the css
selector for this class, pug uses these selectors, so now you have #title. 

Now let's remove the closing tag of the div and let's also add the button, it's
indented because it's part of the form so let's make sure it's in the form,
let's give that the button class don't forget this and let's add the attribute
list to make this a submit button, like that and then a whitespace to separate
the add product text. 

Let's remove the closing tags and that should be it. 

Now let's also render some dynamic content here, for example add product here,
this title. 

I'll again output this dynamically, page title for example, now we have to make
sure that we pass this key into this template and we do render this template in
admin.js. 

So here where I do send this file, I don't send this file instead I now render,
I render my admin file here, the admin excuse me not the admin, the
add-product.pug file, this is automatically picked then and I pass in an object
which holds the key value pairs I want to be able to access in the template and
there, I got my page title key, so that key I'm trying to access here, I got
that and I will assign a title of add product, just like that. 

With that if we reload, this is gone because the server restarted due to our
server side changes. 

Now if I click add product, this is the html code by the looks of it, I forgot
to add the imports, yeah I need to of course also import my stylesheets, so
let's copy the links from shop.pug and add them here in the header. 

Let's also check the add product html file, I also need to import the forms.css
file as you can see. 

So let's duplicate this here, this line and also add this import. 

Now no server restart is required because we just changed the template and
therefore nodemon doesn't restart and now the reload, this looks much better and
let's give this a try, it also still works. 

So that's it, now let's also work on the 404 page. 

For this I'll add a 404.pug file here and I will again create a normal html5
skeleton, I will say page not found here and I will already copy the, what do
you need, the main css file, I will copy that import here from the
add-product.pug file, this link, let's copy it over to the 404.pug file so that
we got that. 

And then in the 404.html file, I get the header and I got Page Not Found, well
we got the header already in add product so let's copy the header here, move
that 404.pug into the body by indenting there and next to the header inside the
body, I'll add a h1 tag where I say page not found. 

And with that we should have it, now let's just make sure that this gets
rendered and for that, we have to go to the app.js file because that is where we
have our catch all middleware and there instead of sending a file, I will now
also render the 404 file and as before, it will automatically look in the views
folder due to our setup and it will look for .pug files. 

So with that, if I now enter any random path which doesn't exist, we indeed get
page not found. 

So this is now working and this is now using pug as a templating engine. 

Now there are a couple of other nice things that pug can do that I want to show
you. 

---