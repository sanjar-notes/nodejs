## 157. Getting a Single Product with the "where" Condition

<strong><em>no description</em></strong>

Time to retrieve a single book when we click on details, so essentially I'm
talking about the get product action here in my controller. 

We get the product ID here and indeed this is the old find by ID method I
defined but if we were to delete it, we see that sequelize also has a find by ID
method. 

So actually if I leave this code exactly as it is right here at least, it will
work, one difference is that with sequelize, we don't get an array of products
here instead I get a single product so I can just use it like this. 

So with these tiny changes, turning this into a single product and using it as
such and leaving this as it is actually, I should already be able to view the
details and I am, just the images may be a bit oversized here, that is something
we can quickly fix in css. 

I quickly added the image class to the div wrapping my product in the product
detail view here and now in the main.css file where I also have my centered
class, I will add a new image class and restrict the max height to let's say
20rem and then also say that any image text in the, nested in an element with
the image class should respect that height and that should also be just height
not max height. 

And with that if I now reload this page here, this is looking better and we
should have no problems with the image anymore. 

Just a tiny change, the main takeaway of course is we can retrieve the product
like this. 

However I also want to show you an alternative way, so using this syntax here is
perfectly fine but let me also show you how we can use the normal find method we
also got, find all to be precise. 

We only have one product with that ID of course but I want to show you that
where syntax, so any object we can pass to find all, I'll set the where key and
there you got a rich query language or a rich amount of options you can use to
configure this. 

More can of course be found in the official tutorial, if you go to querying
there, there you'll find all the details about how to configure your queries,
for example you can also control which attributes are retrieved, you don't have
to get all attributes all the time, if you only need the title, you can define
this too and you'll also see how to use where. 

How to use it in a basic form, where you want to simply check that one attribute
has one exact value but also how you can use operators to have alternative
conditions or to check if something is greater than or greater than equal or
lower than a value and so on. 

So you got a lot of options there and definitely check out these docs, here we
could say I'm looking for all products where the ID is equal to prod ID and then
I will use them or catch any errors. 

Now the one important thing here of course is by default this gives us an array
because even though we know that only one product will have this ID, find all
per definition always gives you multiple items even if it's an array with only
one element. 

So if we use this syntax and we render this, we'll have products and we're
interested in the first product, in this case also the only product as we know. 

So now I can comment out the other approach and if we save that and we go back
to our application and we reload that detail page, it looks like it works but
actually this keeps on loading so something went wrong and indeed we got an
error here, product is not defined. 

Yeah here for the title I should also use products zero of course. 

So now with that if we save that and let it restart therefore, now we can reload
this page and it works as before but now is using find where, find all with that
where query and I simply wanted to show you this alternative approach. 

Of course it's perfectly fine and even preferrable in this case to use find by
ID, so I will actually switch back to that other approach. 

It's good to know how you can query though. 

---