## 125. Pre-Populating the Edit Product Page with Data

<strong><em>no description</em></strong>

So to pre-populate this form with the product data, we need to fetch the product
first, so for in added mode here after not being redirected, then I want to get
my product information. 

For this I need the product model which I already have and I need the product
ID, prod ID can be retrieved from the incoming request because if you check the
routes real quick, we have that dynamic segment here,  so by this name we can
extract the Product ID. 

So in admin.js, here I can set or I can access request params product ID and get
that ID from the URL. 

Therefore I can then use my product model and find this product by id and then
here, I have my callback where I receive the product that was retrieved and by
the way of course, you should also try to add a check to see if you have a
product and redirect the user in case you don't but let's do it like this for
now. 

So here I will now get my product and I will then render this page assuming that
I always get a product and pass my product on a product key and you can name
this key whatever you want of course. 

And we can for example add a check if we don't have a product, so if this is
invalid, if it's undefined then we could return a redirect for now which is not
the best user experience, most of the time you would want to show an error
instead but let's now, for now do it like this. 

So we assume we always make it here and we get the product in the view now, so
let's move over to the edit product view. 

And here first of all let's work on that button. 

Right now it's add product but I want to change that button caption if we're in
edit mode. 

Now remember we're setting this editing property here so this is a variable
available in the template. 

So here I simply want to check if editing and then add a curly brace, if this is
true then I actually want to display the edit or maybe update product text here
on the button otherwise and for that, I'll close the first if block here and add
an else block still in my ejs tags of course. 

So otherwise here if we're in this else block here, I want to show add product
and thereafter I also have to close my curly brace of that if statement. 

If I now reload this page, we see update product correctly and by the way if I
go to add product, I'll now get an error because editing is not defined. 

So to fix this, I also have to make sure that in my controller, for showing the
add product page, I set editing to false of course. 

And now here reloading this page will work, going back to the editing page will
show us the update button. 

Now that is one step, back to the template I don't just want to show the caption
here, I also want to change the action. 

So here on the form, the route we're sending the request to should also change
of course. 

Right now it's always add product but it should only be add product if we are
not in editing mode. 

So here indeed I will also output something dynamic, I will check if we're
editing, so I'll have the same logic as for the button and if this is the case,
I went to load /edit product let's say, otherwise I'll close that and have my
else block open up, so otherwise this is my ejs else block, I'll add add product
into my url here and I can inject these segments into the url because this will
just be converted to normal text in the end. 

This is what ejs does or or what all templating engines do. 

So also close that curly brace of the else block here and with that if I save
this, we should make sure that if we click that update button, we go to edit
product. 

Well let's go back and let's see if we can pre-populate this with product
information. 

Now keep in mind that in admin.js, I am retrieving the product, whoops not here
but here in get edit product and I pass the product information into my view. 

So therefore in the view, we can of course use that and we can set it on all our
inputs, here on value, I also want to check if I'm in editing mode and if I am,
I want to display my product information, if I'm not I don't want to do that. 

So same logic as before, I'll check if I'm editing, if I am then I will display
product title here because this is the title input otherwise I will not do
anything and therefore I don't even need an else block, I just do this if I am
in editing mode otherwise nothing will happen. 

So if I now reload this, we indeed see product title and the issue here is that
of course this is simply output as text, to output the real value behind it, we
need that equals ejs tag here nested into our other ejs tags like this, so this
was now added, equals unclosing with a dollar sign greater than sign. 

And this can be hard to read, you simply have to divide it up in blocks, you've
got if, then you've got the output and then you've got the closing curly brace
for and with that saved if you now reload, you'll see the real title behind
that. 

Now let's do the same for all the other values, so I'll just copy that value
here real quick, for the image url. 

I obviously want to output image url, for the price. 

I want to output product price. 

For the description we get a text area, so here I will not have value equals,
I'll just output the value between the opening and closing text area tags and
here I'll output the description. 

And with that all saved if we reload, this is looking good and now we can start
editing our products. 

Now I want to hook up that edit button so that we can really load the product
and this newly added view. 

So let's do that and then also work on the functionality to store the updated
information over the next lectures. 

---