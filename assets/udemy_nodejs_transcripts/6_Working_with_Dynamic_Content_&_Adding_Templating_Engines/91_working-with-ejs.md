## 91. Working with EJS

<strong><em>no description</em></strong>

So now we had a look at pug and at handlebars, two possible templating engines
you can use and if you plan on using them, definitely dive deeper into their
docs. 

Now I want to show you my favorite and the templating engine we'll use for the
rest of this course and that is ejs. 

Now ejs is a templating engine which is just like pug, supported out of the box
so we don't need to register the engine as we did it with handlebars, we can
remove that, we can therefore also get rid of that handlebars import and here we
just set the view engine to ejs now. 

Now ejs has a very nice syntax in my opinion and has a nice mixture of the
extended functionalities of pug, so not regarding the html but regarding the
javascript code you can use in your templates, that you can do things like that
simple comparison here in shop.pug file, this comparison here with the if
statement which we couldn't do in handlebars, that is again possible with ejs
and this is the nice thing I like about it and still, it uses normal html just
like handlebars which I personally also like but of course you can follow along
in this course with any solution, I will stick to ejs though and all source code
will therefore be provided with that templating engine. 

So let's use it then and let's start with the good old 404 page again. 

I'll add my 404.ejs file and now in there, let's start with the html code again
and let's copy that into that file here, so all the 404 html code, let's move it
in there, get rid of that active class which still incorrectly is there and now
we got this set up. 

Now ejs does not support layouts but we will find a solution to at least have
some kind of reusability of certain building blocks but for now let's just
create the whole document in that file. 

So this is now our page and let's start with the title again and let's output
that dynamically. 

Now in handlebars, we used double curly braces, in pug we used hashtag and then
single curly braces, in ejs we use a smaller than sign and then a percentage
sign and then if we just want to output a value in the place we're placing this
placeholder, we add an equal sign right after the percentage sign and then we
close this with just a percentage sign and a greater than sign. 

So this is the syntax and now here we can output the data which our template
receives and just as before, the method of how we receive that hasn't changed,
so we can still output page title here, just as before. 

So just to bring this back in memory, in app.js we're passing in that page title
here and therefore we can reference page title in our template. 

So this will still work and with that we can already test this. 

If I now save this and I reload here, I get an error for add product because
we've got no ejs template for that yet but if I enter anything else which is not
found, we do indeed see our not found page rendered through ejs. 

So this is now working and with that let's move on to add product, let's add the
add-product.ejs file here and in this file, again I'll just copy in my add
product html code, here I also want to output the title dynamically though, so
again our syntax here which we used just a second ago, let's output the page
title here and then the rest can stay as it is for now. 

Now the more interesting part is the shop file because there, we also need an if
statement and a loop. 

So let's add our shop.ejs file and in that shop.ejs file here, let's copy in the
html code we got here for the shop and let's make sure we also take that new
image here, so let's copy that from one of the other files then move over to
shop.ejs and replace that here. 

And with that, now let's remove these comments again so that this is part of our
page, let's remove that part up there and now in this file, we can of course
again simply output our title equals page title as we did it before but the more
interesting part are obviously the if statement and our loop, so we want to
output this grid here only if we do have some products. 

Now an if statement is placed a bit differently than with handlebars, we still
use our smaller than percentage sign syntax but not an equal sign because we
don't directly output a value here in this place, instead we want to enclose, we
want to wrap a certain block of code and we do this by adding our opening and
closing ejs tags you could say like this and now in there and that's the cool
thing, you can write vanilla Javascript code. 

Now we know that we will get in our shop route here, we will get our prods key
which holds our products array and this will be an array and therefore here what
we can do is we can write a normal javascript if statement, so normal javascript
code and that is really important and simply say prods.length greater 0 and if
that is the case, I want to render this, so thereafter after this grid, I also
close this and now here important, you simply close the curly brace which you
also have to open here at the beginning. 

So in the end what you do is you write a normal if statement as you would write
it in a javascript file, just that the part inside of that statement is not
javascript code but this html code and I find this to be very straightforward
and easy to understand. 

So this is our if statement here with the opening curly brace and once we're
done, we close that curly brace. 

Now we can of course then also combine this and add an else block here just as
we would do it in normal javascript again and eventually once we're done, also
close that and now here we can output our h1 tag where we say no products found.


Now that is nice, let's see that in action by saving and by now going to the
shop page and indeed, we get no products found. 

If I now do add a product on add-product here, first book, we do see it here so
the if statement is working. 

Now again of course we want to loop through all the products and output our data
and for that again, we use the same logic as with the if statement. 

We create simply the normal javascript code we would use for looping and there
are multiple ways of doing that, we could use prods forEach to use this forEach
function vanilla javascript supports or we use a normal for loop, we could say
for let product of prods and then we simply open a curly brace, wrap all the
content that should be repeated and once we're done, we add another ejs tag
where we close that curly brace, again using normal javascript and then we have
our product in there and now we can again output it as before with this ejs
equal syntax as I like to call it here, basically this inline output syntax. 

And now with that if I reload this page here, we see object object, that is my
mistake, obviously we want to access product title because product indeed is an
object, so now we see the title. 

This is ejs and I prefer this syntax because I like having that flexibility of
being able to write some javascript code in the template whilst having a clean
syntax that nicely mixes with html because I personally like using html instead
of the minimal version pug offers us. 

But as I mentioned, you can go with any approach you like. 

---