## 330. Restricting File Access

<strong><em>no description</em></strong>

Now how can we improve this serving of the data? 

Well first of all, right now this is only available to authenticated users
because on my route here, I have the isAuth middleware but every user could view
that, I don't have to be the user who placed that order. 

However for that order, I of course know which user belongs to it, I have the
user id here. 

So we can add an extra check in our middleware, in our controller action here to
see if for this order, the user is eligible of downloading it. 

Now how do we do that? 

Well we use the order mongoose model, find that order by that ID in the database
and then check if the order user ID is equal to the ID of the currently logged
in user. 

So here I can check order and then find by ID and I pass in my order ID, I have
then and catch here. 

Now as you know, in here we can simply next an error to use the default error
handling function and here we'll have our order element though that could be
undefined if no order for this ID is found, so if no order is found, then I will
also return next with new error maybe, no order found, whatever you want, you
can handle this differently. 

If we do have an order however, I want to check if the order is from that user
who's logged in. 

So then I can check if order user and then keep in mind, in the user object we
have user ID field, so if that user ID toString, if that is equal to request
user_id, so if the currently logged in user toString, if that is equal I am
allowed to access this, if it's not, so if I'm checking the opposite, if it's
not equal then I will return a new error unauthorized, something like this. 

And only if I make it past these two if checks, only in this case I want to read
that file and output it. 

So if I now save this and I access this, it works, if I change the three here to
a two, I get my error because now it's an invalid url and if I copy that
original url which was correct and I do log out and I try to access this whilst
I'm logged out, I have to log in and if I log in with a different user or let me
quickly create that user and I then log in and I now try to access this order, I
also get an error, I have to be the correct user. 

Now of course you could show a different error message but that is always
something you can tweak, I only want to show you how you can protect this and
that you have this option of controlling that access. 

So here, this all works just fine. 

---