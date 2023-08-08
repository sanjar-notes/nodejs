## 75. Serving Files Statically

<strong><em>no description</em></strong>

In the last lectures I added some styles and please just take these three html
files which you find attached to this lecture and replace your existing views
with them because I don't just, I didn't just add some styling, I also added
some css classes. 

Now the page will look something like this, you can tweak the styles if this is
not your style, obviously this course is about the logic, the nodejs logic and
we will continue working on this project, the html and the styling too. 

One issue we have though is right now all the styles are defined in the html
files and I want to use external css files. 

Now the problem is right now we can't easily import them but let's see how we at
least theoretically would want to do that. 

Now typically, you would have some css files somewhere and would point at them
when your app gets served, now you can create a new subfolder and you can name
it whatever you want but the convention is to call it public because you want to
indicate that this is a folder that holds content which are always exposed to
the public crowd or which is always exposed to the public, so where you don't
need any permissions to access it and that's important. 

All your files here are not accessible by your users, if you ever tried to enter
localhost and then something like views, shop.html, that will not work because
this is simply accepted by express and it tries to find a route that matches
this. 

It tries to find it here in app.js basically and also of course in shop routes
and so on. 

It doesn't find that route and therefore it doesn't give you access, you can't
access the file system here and that is of course good and what you want. 

But now I actually want to make an exception, I want that some requests can just
access the file system because ultimately let's say in shop.html, I want to have
something like a link in here where I simply point at something like css,
main.css, anything like that and my imagination would be that in public, I have
a css folder with a main.css file in there and that is the file I want to serve
with this link. 

Now right now, this wouldn't work but let's take that code already, that style
code, cut it out of shop.html and move it in there because that pretty much is
the main styling we use in all our pages, the header and the body. 

Let's remove the style tags here and obviously if I now save and reload my main
page, all the styling is gone now because it can't find the main css file as far
as you can see here in the developer tools because we can't access the file
system. 

Now you could say yeah the path is incorrect right, it's public css but even if
I change it to this path, you will see that if I reload this file, it will never
work and now it does look in the public folder. 

For this we need a feature  expressjs offers us, we need to be able to serve
files statically and statically simply means not handled by the express router
or other middleware but instead directly forwarded to the file system. 

And for this, we register a new middleware with app use and this this one
expressjs ships with, therefore we use the express object itself, so this object
we're importing there and this does have a static method and this is a built-in
middleware as you can read on the right, it serves static files. 

So we can execute this function. 

and now we just have to pass in a path to the folder which we want to serve
statically, so basically a folder which we want to grant read access to, it's
only read access but that's still more than what we normally have. 

And here again we can construct this path with path join and then simply our dir
name, so our root folder and then public because I want to grant access to the
public folder in our current folder here, so in the dir name, so in the root
folder. 

With this, user should be able to access the public path and now if I save this
and I reload shop.html, still doesn't work. 

The reason for that is that the path with public at the beginning here is wrong.


Instead here, we should omit this and directly act as if we are in the public
folder already because this is basically what express will do here, it will take
any request that tries to find some file and that's important, it looks at the
extension, so anything that tries to find a .css or a .javascript files, if we
have such a request, it automatically forwards it to the public folder and
therefore then the remaining path has to be everything but that public, so
therefore we strip the public out of this path and just act as if we already are
in the public folder because this is where file requests will be forwarded to. 

So now if I reload here, this looks much better right, now we find that main.css
file because now this path can be resolved because we request a file here and if
I omit .css, it therefore will fail but if I add it again, this is handled by
the static middleware and forwards the request to the public folder. 

And by the way, you could register multiple static folders and it will funnel
the request through all of them until it has a first hit for the file it's
looking for But here I'll just go with the public folder. 

Now with that, we can of course take that link and also add it in add product in
our head section, now there we just have to watch out in the style text, I got
more than what I set up in main.css so I'll also add a product.css file and move
the extra styling code which begins here with product form, we'll move all that
into product.css and the other part in the style tags here can now simply be
removed and therefore I now also have to add an import here to css, product.css.


And in the 404 page, I of course also want to import my main css code and there
I got no extra code, so we can remove the style tags and simply import the link
here. 

Now with that if we save that and we reload this page, it works, add product is
looking good. 

Let's add a book here, looking good and let's visit a route that does not exist,
also looking good regarding the styling at least. 

So this is now how we can serve files statically and you're not just limited to
css and javascript files, you can also serve images and so on. 

So this is the last important piece for now, how you can serve content
statically, in the next modules we'll then dive deeper into actually doing
something with that user data we can submit there and we'll dive into a very
interesting concept, the concept of templates because that will allow us to turn
our static html code, so basically the code which is hardcoded which doesn't
have any dynamic element into more dynamic elements where we can inject data we
have in our javascript code in the html templates we return to the user. 

Pretty interesting, we'll dive into all of that in the next modules. 

---