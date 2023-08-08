## 225. Storing All Order Related Data

<strong><em>no description</em></strong>

Now let's see what was causing that issue and for that let's console log user
cart items to see what's in there when we place an order. 

So if I click order now now and I increase the console, we see product ID indeed
does hold a full object and not just the ID which is what gets stored though, if
I refresh my orders, now I got two but both orders actually just have the
product ID in there, not the full product, I want to have the full product data
though. 

Now one thing we can do is here when I store the product ID, I can wrap that in
curly braces to create a new javascript object, use the spread operator and use
that not directly on the product ID but on a special field mongoose gives me,
_doc. 

I can access this here because product ID actually will be an object with a lot
of metadata attached to it even though we can't directly see that when console
logging it but with .doc we get really access to just the data that's in there
and then with the spread operator inside of a new object, we pull out all the
data in that document we retrieved and store it in a new object which we save
here as a product. 

And with that if we save that and we go back to the cart and I click order now,
I get no error and if I go back to my compass interface and I have a look at
this new order, there I see indeed I got all the product detail data in there
too. 

So this is now working and this now allows me to store all the data I want to
store with every order. 

Now with that being stored, of course the missing part is that we also clear the
cart. 

---