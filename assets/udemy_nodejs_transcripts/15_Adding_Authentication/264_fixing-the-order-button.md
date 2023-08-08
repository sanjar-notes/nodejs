## 264. Fixing the Order Button

<strong><em>no description</em></strong>

So now that the csrf protection was added, let me quickly fix that error where I
was not able to order an item and there, the path username is required is the
issue which is thrown, let's quickly check the shop controller and there, the
post order and in there, I indeed store the username and I'm not storing the
username anymore here. 

When signing up, users only have the email, so here we could store the e-mail
for our user with request user e-mail on the order, like this. 

So instead of the name, I now store the e-mail of the user in here or you also
omit this and just store the user id, whatever you want. 

Now in our order model, this means that here I also don't expect the name but
the email which still is a string and still is required, So this is a tiny
change that needs to be done to fix that issue and if I now go back to products
and I add this to my cart and I add it to my cart again let's say therefore I
have to order this, now this works and the cart is empty. 

So this was just a little node something that was required, let's logout, this
all works. 

This is this bug fixed. 

---