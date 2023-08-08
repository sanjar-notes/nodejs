## 89. Converting our Project to Handlebars

<strong><em>no description</em></strong>

So let's work on handlebars now, for now without the layout. 

So let's go to the add-product.html page and copy that over into a
add-product.hbs file, like this. 

Now this is now our add product page, this is all looking good, now let's output
the page title dynamically and we're not using a layout for now, I will show you
how this would work in a second too, so let's add the page title, active class
should here be on add product, no need to assign this conditionally because
we're in the add product.hbs file anyways here, this is not in the layout. 

And now let's also go down there, this should all of course still work, so this
was pretty straightforward I guess. 

So if we now save this and click on add product, this should work and this is
now rendered by handlebars because that is our view engine. 

Now let's go to the shop.html file and let's copy all that code here and add a
shop.hbs file here, add that code here, the title becomes shop or better
dynamically output page title. 

And now the interesting part of course is here in the main section, there we can
comment in this code, so let's remove the comment tags here and now I want to
loop through all the articles and then of course also change the image here,
this  is still the old not working image, let's take that new image link I added
in the pug template, so let's move that into here too, like that. 

And with it added, let's now repeat this article for all the products we have
and show no products found text if we got no products and for this we need to
use a new handlebars index which you obviously don't know yet. 

Maybe you explored it in the official docs, otherwise let's add it together
here. 

First of all there is an if helper, you still add your double curly braces here
but then you add a hashtag for special block statements, block statements simply
are statements which are not just outputting some text but which actually wraps
some content that should be output conditionally or in a loop, here we can then
add the if keyword and check if prods.length is greater than zero. 

So it's the same condition as in the pug template, just the syntax is a bit
different. 

Now we want to output this article or actually not the article, the entire grid,
so let's actually switch that, the entire grid here, let's indent this,
indentation here doesn't matter but makes it easier to read. 

Here we want to wrap this and now we want to close that block at the end and we
do that with a closing statement where we also have if here, by the way if here
also has to sit next to the hashtag. 

So this opens an if block with the condition, then this content is only rendered
if that condition is met and then we close it. 

Now of course we also want to have an else block so let's add this here too,
hashtag else is then the key and there we simply put the content we want output
if the condition is not met, no products found. 

With that let's save that and let's go back to the shop and we get an error. 

The problem we have here is that handlebars doesn't actually support statements
like this, it just supports the output of keys that yield true or false. 

Now this means that we have to move that logic from the template into our node
express code and pass the result of this check into the template. 

So we would go to shop.js and there, we actually add a new key value pair we
pass into the template, has products maybe and this simply holds a value which
is the result of our check here, products, so this products array here length
greater 0. 

So now we just pass this key in there which is true or false, the result of this
check and this is a core difference to pug already besides that html thing. 

Here in handlebars, we can't run any logic in our handlebars template, we just
can output single property, single variables and their value and we can only use
these in if blocks too. 

So here I can now check if has product is true because this is now the data I
pass into this template and this actually also has a positive side, it might
sound very complex but it forces us to put all our logic into the node express
code where our logic typically should live and keep our templates lean because
if you put too much logic in your templates, it can be hard to understand your
code because you always have to check both, your express code and your templates
otherwise you know the template is really just about displaying stuff, the logic
always happens in node express. 

So these are two kinds of philosophies, it's up to you to choose your favorite
but this is how express handlebars or how handlebars in general handles this. 

So now with this change, we can reload this page and now we just have a problem
with else here but that is just that it's not #else, just else, just the else
keyword my mistake, so now if I reload, we have no products found and if I do
add my first book here, we do actually see that. 

However this of course is not the values we have in our products array, we have
some hardcoded data here because I still have to add a block where we loop
through all products. 

And this is done with an each block statement with #each and then you pass in an
array, prods in our case. 

So now prods is passed into this loop and now in there, this element is repeated
for each element and we also have to close this with /each after we're done
repeating our code. 

So now this block of html code is repeated for every product. 

The question now just is how can we access this product and here handlebars also
gives us only one way, it gives us the this keyword which refers to the element
in the array for the current iteration, so to each product. 

So therefore we can output this title here for example because this will always
refer to one product and one product still is a javascript object as stored in
the array here in the admin.js file, an object with a title key. 

So now if we save this and we reload this page, now we see first book here
because this is the title we assigned. 

So this is now how handlebars works and it's really important that you
understand this different philosophy of having less logic in the template, more
logic in the node express code, so you have to prepare everything there so that
in the template, you don't have to write any javascript expressions. 

Therefore this is now the project converted to handlebars except for one thing
and that is of course the layout. 

---