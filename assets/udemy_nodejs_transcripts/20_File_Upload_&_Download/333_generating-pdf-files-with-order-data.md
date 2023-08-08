## 333. Generating .pdf Files with Order Data

<strong><em>no description</em></strong>

So let's create a more useful pdf now. 

Now you can configure a lot and the official docs of pdf kit are the place to go
to learn more about that but let me show you how you can generate some nicely
looking pdf in little time. 

For example, let's set a font size here of 26 and then add some text and this
text will now have this font size and this will have text of invoice. 

If I now save this and I reload this page, we get invoice written like this, we
can also pass an object as a second argument here and configure this, for
example you can set underline to true here on the text and now if I reload this,
we have the underlined text. 

So of course you can style way more, you can even add images and all that stuff.


Now I'm happy with that title, I'll simply add some dashes as the next line here
and then thereafter, I want to have my different items. 

So now I have to loop through all the items that are part of the order, in this
order I only have one product but I might have more products and actually we can
of course do that. 

If I go to products, I can add this product to the cart twice and I can quickly
create a new product, prod2 and boring as I am I'll use the same image for 29
bucks, product 2, let's quickly create that product and then after we created
it, I can add that to my cart as well and then I could order this and now I've
got a brand new order. 

Now by the way, I should place that invoice link next to the order not next to
the product now that I have a look at it but it doesn't matter, we can change
this later. 

For now this will always lead to the same invoice so it does not matter too
much, now I have multiple products in there and I should loop through them when
creating the output. 

So I can add a for loop or simply access, keep in mind we already have access to
the order here since we fetched it from the database, I can access order
products and products is an array because we store this products in a database,
it will be an array of objects where each object has a quantity and then a
product key with more detailed information. 

So I can loop through my products for example with the forEach method which is a
built-in method provided by javascript, I'll then get information about my
product and I can now output some text where I print the prod, product is then
the detail object and in that product, we have the title for example, so I can
output the title here, then let's say we add a blank and a dash and a blank and
then I have prod quantity right because we have the quantity key directly on the
product itself and then I add let's say a times character and then we want to
output the price, so I'll have let's say a dollar sign and then last but not
least, I'll have the product price, so this field here. 

Now of course you could also use the next gen javascript syntax with back ticks
to make this a bit easier to read, I think it's maybe easier to understand how
we are concatenating this from hardcoded values and dynamic values and now we
should be outputting a line of data for each product in that order. 

Now let's also add a sum at the bottom and we can calculate that on the fly
here, let's total price start at zero and if we are looping through all the
products anyways, we can use that to also update our total price because total
price will then be the old total price plus the product quantity times the prod
product price. 

So basically what we print here is text, we'll then also add it to our total
price here, by the way this can be written in a shortcut with this operator, now
this will always add the result of this calculation to the old total price and
then here outside of the loop once we are done calculating the total price, I'll
access my pdf doc, output some text here and that text will be total price
dollar sign and then simply total price, like this. 

With all that let's save that and let's click on invoice for the second order
and here I get my invoice which looks like this. 

Now of course we can also revert the font size here by setting font size to
let's say 14, so that we don't use that super big font for all our text, so now
by adding this line inside our loop, I am sure that this looks like that and
then maybe just some stylistic thing, though it will not become super pretty. 

I can add maybe some more dashes here to separate the list from the total price
and set the font size of that total price a bit bigger, to maybe 20. 

Save that, reload and here it is. 

Now obviously, this is not the most beautiful invoice we ever saw and you can
learn way more about how you may style that in your official docs of pdf kit. 

The important thing is the data in there is correct, so the data does look
correct, the total price is correct and this is how you can generate data on the
fly and how you can then return it in a response and also save it in a file
because that is important too. 

We do both at the same step and I believe its very interesting to see which
power nodejs has and what you can do with it especially when also playing around
with the features of writable and readable streams, like here where we are
creating a pdf on the fly and we were streaming it both into a file and back to
the client. 

---