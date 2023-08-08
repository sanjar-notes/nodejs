## 244. Fixing Some Minor Bugs

<strong><em>no description</em></strong>

So now that we learned a lot about sessions, let me fix some things here real
quick and for example if I go to my cart or to my orders, I have some issues
there. 

And the problem of course is that without a valid session and we don't have a
valid session now after destroying it, all these methods in there, all these
actions where I do reach out to my user to fetch the current orders, these will
all fail and of course this makes sense because we need a session because we
need a user for that. 

So what would work are shop and products and there details, add to cart will not
work though. 

So a first step to improving that besides checking for the existence of a user
on the server which we will all add in the authentication module but a first
thing we can do is that we adjust our frontend to only display things we can
actually interact with based on our current authentication status. 

So for that, I'll go back to my views and I'll start with the navigation first
of all because there we can also say that login and log out should only be
displayed, should only be rendered when we are actually not logged in. 

So here I'm checking if we are authenticated to show add product and admin
products, first of all this should move up and also include cart and orders
because these only makes sense if we have a user because otherwise as we saw,
we'll get an error if we visit these pages and then we can repeat the logic down
there and only show this entire unordered list if we are not authenticated, so
if this is not true then I want to show these items. 

So now we can also add this code and if we now save that and we reload this
page, we only see shop and products by default, once I login though, we see the
rest. 

Well actually log out should be visible once we are authenticated now that I
think about it. 

So we should revert this, move that in there and only don't show this login list
item if we are not authenticated, if we are authenticated so here we can use
else, if we are authenticated then I of course want to show the log out screen. 

We get this correct here, so now here I can now close this. 

So now if I save that again and I reload my page here, I do see log out, once I
click this, I see login and once I do login again, I see the inverse. 

And now also feel free to pause the video, make sure for add to cart the same is
true, this should only be visible when you're logged in but not when we are
logged out. 

Here's your chance to pause the video. 

Were you successful? 

It's actually the same logic because isAuthenticated is information we pass to
every view anyways, so therefore we can go to the product list.ejs file where we
do include Add to Cart, so we should go to add to cart actually and there, this
entire view should only be rendered if we can add the item to the cart, so if we
do have a session if we are authenticated. 

And therefore let's go back to the product list, this entire part here should
only be rendered if we are authenticated, so if isAuthenticated is true then,
we'll include this here otherwise as we won't. 

So now with this change if we save that, if I reload this page and I'm not
logged in, I still see it because I'm on the wrong page. 

For products this will work but for the index page, this is a separate page,
it's index.ejs, there we should also replace our include with that updated logic
where we check for the existence of our, well logged in user. 

So now with this added to index.ejs too, now if I reload the starting page, this
is only there after I logged in as you will see. 

Now we can add this to the cart and we fail again though, now why is that? 

Let's check this in the next lecture. 

---