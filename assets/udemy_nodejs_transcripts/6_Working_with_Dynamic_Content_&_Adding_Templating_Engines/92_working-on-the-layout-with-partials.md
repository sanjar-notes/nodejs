## 92. Working on the Layout with Partials

<strong><em>no description</em></strong>

Now we added some ejs magic or some ejs templates here. 

One thing that is missing here is the layout functionality pug or handlebars
gave us and indeed ejs doesn't have layouts but we can use so-called partials or
includes, by the way a feature that pug and handlebars also know. 

The idea here is that you have some code blocks which you reuse in different
parts of your templates and you can therefore just share them across your
templates, so it's a bit like the opposite of a layout, instead of having one
master layout where you put your individual view parts into, you have a couple
of separated shared view parts which you can merge into the views you're
creating and for that I'll create a new subfolder in the views folder which I
call includes and that name is up to you. 

There I will create a couple of shared files or shared code blocks and which
code do we share across all our views? 

Well we certainly share this part here where we have like the beginning of the
html document including the title, including the main css even and then we share
the body of each document so we also can outsource that even though it's not
that much code right now but that might change if we have a common script that
we import everywhere, we also share the navigation. 

So there are three include files I want to create here, head.ejs for the start
of the document, end.ejs and of course you can name these files however you want
and navigation.ejs. 

And now I'll just go to the 404.ejs file, grab the beginning of the page,
everything that is shared, cut that out of here and move it into my head.ejs
file. 

Now I just need to import this and this can be imported into the 404.ejs file by
adding our ejs syntax, now with a minus and you use that if you want to output
unescaped html code, that by the way means that by default if you have this
syntax with the equal sign and you would render some variable that holds a
string that holds html code, it would not render that html code but render it as
text to avoid cross-site scripting attacks, with a minus you can avoid this and
really render the html code. 

We can do this combined with a keyword offered by ejs, the include keyword which
allows us to include a certain element into this page and then you close that
with the normal ejs tag, without the minus. 

Now here in include, you simply add a string which holds the path to the file
you want to include and you have to enter this path as it's seen from the file
you're in, so the 404.ejs file is in the views folder so the file we want to
include is in a subfolder. 

So we just have includes and then head.ejs and this will now take the html code
in here and as I mentioned, then also render it here. 

Now let me save that and let's go to some route that doesn't exist and we still
have a valid document here as we can prove if we open the page source, so this
all works, now we're using an include. 

By the way if you use an equal sign here, you see now it gets rendered as text
and that is what I meant, this is escaping the values so it's not rendering it,
so if you had some script tag or anything fishy in there, it would not render
it, it would just display it as text and therefore protect you but if you know
what you're doing like we do here because we wrote the code we're including, we
can and we should of course include it as html. 

So this is now using an include and we can now also use that for navigation, so
let's take all that navigation code here, put it into the navigation.ejs file
and in there, we'll also have to manage the active link again, I'll come back to
that in a second, for now let's just go back to 404.ejs and here again, I will
just include includes navigation.ejs and close that. 

And last but not least, the end of the document is also shared even though it's
very short, let's move that closing body and html tag into end ejs and let's
share this too, so here at the very end I will have include includes end.ejs,
like this. 

Now with all that out of the way, I can still load this page just fine and it
works. 

Now let's also implement this and this is of course a great practice for you
too, so feel free to pause the video, let's also implement this for the other
two templates we have. 

Were you successful? 

Let's try it for add-product.ejs, there we also want to take our common code
here out, so the start of the document not the two links which are exclusive to
this page here though, so which we really only need there but instead of the
other part, we can now include our includes folder and there, head.ejs to bring
back that start of the document here. 

In add-product, we obviously need to replace more like the header, so there we
also should use include and then go to the includes folder, navigation, close
that and close the tag and also the same for the end of the document since we
did that before include, go to includes and then here includes and then there we
have end.ejs. 

So now we get this in there too but of course one problem we face if we reload
this page is that our active class is gone here, so we need to bring that back
and mark this navigation item as active if we are on the add product page. 

Now for this, let's go back to the admin.js file real quick where we do render
this route and there let's remember that we already added this path for pug and
we can reuse that functionality. 

We can go to our navigation.ejs file and then add a class here and there simply
output something rendered through ejs, we can do this inline with an equal sign
so we don't need to enclose a block of html code and simply check if path is
equal to and now the path here is /admin/addproduct, so basically the path which
we define here and if this is equal, I'll use a ternary expression here which is
an inline if statement in Javascript, so here we have the condition and if that
is mapped, we now do whatever comes after the question mark. 

So then I want to render active here and since I'm inside the class text here, I
will basically just add the active class, this is how you can read this, always
keep in mind that this simply gets replaced with text when the template is
rendered, so this will just become class equals active and then I add the else
condition with a colon and else is just that I rendered nothing. 

And now I can copy that here, that class assignment and do the same for add
product where this should belong, there where I did it originally, I should
check for just slash because that is actually the path we set for the shop here
in the shop.js, this path. 

So now I got this in place, I'm checking for the two different paths here and I
render the active class based on that and therefore if we save all of that and
we reload the page, we got add product added here. 

Now let's go to the shop.ejs file and there let's do the same. 

Keep the link which we need in that file, which is the product.css file and
replace the other part with our general include, so in the includes folder,
there we have the head.ejs file, replace the navigation as we did it before, so
there we have include includes navigation.ejs and of course also replace the
body of the document. 

So here we have include includes and ejs, like this. 

And now with that, if we save that too and we go to the shop page, it looks like
it did before and we should still be able to use our application as we did
before but now we're using includes which is kind of giving us the same
experience as with layouts, we have to repeat all this include code all the time
but that is okay and we still benefit from having shared code. 

So with that out of the way, we got ejs added and we'll continue to work with
that throughout this course and I hope you got a solid understanding of why we
use templating engines, which options you have and how they roughly differ and
with that, you should of course be able to choose your favorite. 

---