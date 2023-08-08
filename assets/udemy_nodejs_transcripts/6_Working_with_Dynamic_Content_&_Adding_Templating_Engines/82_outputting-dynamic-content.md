## 82. Outputting Dynamic Content

<strong><em>no description</em></strong>

We're rendering our shop template but we're not rendering any dynamic content,
that however is the whole idea of this module. 

We get our admin data with the products, so let's actually take these products
out of admin data products and now we want to pass that into our template,
inject it into our template so that we can use it in this template file and
somehow output it there. 

To do that, we can simply pass a second argument to the render method, the
render method allows us to pass in data that should be added into our view. 

Here we can simply pass products, however not like this but as a javascript
object where we map it to a key name which we then can use in the template to
refer to the data we're passing in and we can pass in prods, simply to avoid
naming confusion, you could use products but then I'll bind my products, so this
constant to the prods key in this object. 

This is passed into this template and now in the template, we will just be able
to access prods, this is now available, by the way we can also pass more than
one field, we could pass in let's say a doc title which is shop and now we can
use that too. 

And let's maybe start with the doc title so this additional field we're passing
in this object. 

In shop.pug, let's say the title here should actually be that doc title. 

For this we can use the custom templating syntax pug gives us and if you just
want to output some text, this is a hashtag followed by two curly braces and
between these curly braces, you can put any value you are passing into your
view, so any field you have in this object, like doc title, we can use that and
simply refer to doc title here. 

If we now save that and we go back to our page, right now it's still in my shop
right, if I now reload it's shop and it is shop because this is the title I'm
storing in doc title here and doc title is what we're outputting here, so this
flow is important to understand. 

Now of course we can also use that to output our products. 

For this next to the header, so on the same indentation level, this is important
because it defines the nesting of the html, we can add the main element just as
we have it here and now I don't want to have this h1 paragraph here instead now
I want to output my product with this code. 

So I'll copy it over even though it is html code but we'll adjust this and
transfer it to pug code. 

So the div here becomes just .grid, you don't need div because if you don't have
anything, it's assumed to be a div, the article with this class becomes
article.product item. 

However important, if you've got multiple classes, you need to merge them and
simply concatenate them separated by dots and never forget the indentation, the
article should be inside of this div with this class so let's indent it one
level. 

Here we got an indented header because it's nested in the article and this
header also has this class here, so let's add it like this and then in the
header, we got a h1 tag so let's also indent  this and here again this has a css
class. 

Now it also has some text and you simply separate the text with a whitespace
from the element and you never need closing tags here, that is handled for you
by pug. 

So this is really a syntax that is very different to normal html and is really
up to you if you like that that or not, I personally don't work too much with it
but if you like it, this can of course allow you to write very lean html files. 

We don't need the closing header tag because again this is added automatically,
so we can move on to the card image which should be next to the card header. 

So let's indent, remove that smaller than sign, add this class here without the
class keyword and let's add the image inside of there. 

We get an image and again as before with the links here, if you have attributes,
you wrap them in normal brackets, like this, so like the source and also the alt
key. 

You can always by the way also use emett here, this is the plugin which helps
you with auto-creating this, if you type the tag or the class name with a dot at
the beginning and hit enter, it will auto-complete that for you and give you the
respective pug representation and there we saw that we actually need a comma
after source, right before alt. 

So now this will create an image nested in this card image, don't need the
closing div tag. 

Now the card content is also a sibling to the card image, so let's indent this,
remove that and add this dot here and let's do the same for the h2 tag, indent
it, turn it into a pug conform setup here, we have some text next to it like
this, for now that's static, later this will become dynamic and let's also do
the same here for the paragraph, add the class here and have some static text
and remove the closing tag. 

Now we're almost done, only a couple of elements to go. 

We get a div, now this should be also next to card content so let's indent it, a
div as I mentioned doesn't have a tag you need to add, you can just have dot
something, so dot and the class name. 

If you have no class, of course you would write that div otherwise there is
nothing. 

The button is inside of card actions and this does have a class again and then
it does have some text inside of it which we add next to the button element and
all these closing tags can be removed. 

Now this outputs a grid of product cards however only with static content. 

Now to make this less static, we need to iterate through all the products and
remember that we do pass the product into the view here on the prods key. 

So to iterate and repeat this article for all the products, we can simply add a
special syntax provided by pug and you do create such a loop by adding each
keyword then a value in which you want to store the value for the current
iteration, so a single product in our case and then in and then the array
through which you want to loop, so this would be prods in our case, again with
prods referring to this key in this object we're passing to our view. 

So now we're looping through the prods, let's all indent this into the loop so
that we repeat this entire block for each product in this prods array and now we
can use the product variable which we're creating on the fly here to output the
data, like the title. 

Here we could output hashtag and then again just product.title because remember,
a single product we add to this array here is an object with a title key, we do
create this here in admin.js, we push a new object with a title key, this is one
single product as we'll have it when we loop through it,  so this is what we add
here or what we output here. 

With all these changes in place, if we now save this and we reload this page, we
don't see anything because we have no products yet but if we add a first book
here, we do actually see that here and we see that the image does not work
anymore, so let me quickly add another free to use image, you can of course
simply google for any image that you can use as a dummy image here for now. 

Once you got one, take that source whichever it is and simply replace it here,
this is only for practice purposes here so now if we repeat this, this looks
much better. 

By the way if you only change something in the template as I just did, you don't
need to restart the server and node one will not do so because the templates are
not part of your server side code, they are basically just templates which are
picked up on the fly anyways so if you change them for the next request that's
coming, they will automatically take that new version already. 

So with this, we get a basic introduction to pug, it's strange very minimal
syntax and how you can output single values like some text or also loop through
some items. 

Now of course we could have the case that we got no products at all, so one
thing you also want to do is you want to ensure that you have a conditional
check and render either content A or content B and we can do that too with pug. 

We can add an if statement and check if product.length, so if this array of
products is greater than zero, if it is greater than zero then we'll output
this, so let's indent it all into the if statement because then we do have some
products to output otherwise I will go into the same level as grid here, as the
if statement and add an else block because otherwise I will output h1 tag where
I say no products. 

With this, now if I restart the server to clear my products array and I reload
this page, I actually get an error because of course it's prods here, remember
we're passing prods as a key not products, so prods is what I should check here.


Now if I reload, I see no products but if I add one, first book like this, now
we see that instead. 

So now we got the three most important parts, outputting simple text and so on,
outputting a list and outputting conditional content. 

This is pug in a nutshell and this is how you use templating engines in
expressjs in general. 

Now feel free as a practice to play around with that and also work on that add
product html page and replace all these items or all the content here with pug
templates. 

Keep the html code around, don't delete these files so that we can easily switch
to other templating engines later but make sure you add pug templates for the
other two pages and that you render them, also feel free to inject some dynamic
code like the page title. 

In the next lecture, we'll do that together. 

---