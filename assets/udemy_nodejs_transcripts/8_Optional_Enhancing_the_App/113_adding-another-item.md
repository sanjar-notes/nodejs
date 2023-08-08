## 113. Adding Another Item

<strong><em>no description</em></strong>

To conclude this module, I will now simply add one additional view here in the
shop and that is the orders.ejs route which is responsible for displaying
orders. 

We don't have any yet so I will just take my cart.ejs content and put that in
there so that we at least have the navigation and obviously we could then
display something in-between, have some main element and say h1, nothing there
but we'll work on that obviously and I want to add this in my navigation too. 

There I already have the cart, now next to the cart I will add one additional
navigation item where I say orders and I go to /orders and the path here which I
check for the active css class is /orders and now therefore in my routes here in
shop.js, I want to add a new route which allows me to go to /orders and this
means I need a new action in my shop.js controller, there I also want to be able
to load that orders page, so I will just duplicate the get cart action your name
does get orders like this and then simply return shop orders, this new view I
added and then path orders and then here also your orders, like this and now we
can go back to shop.js in the routes file and have get orders here. 

With that, this is looking good. 

If I save everything and I reload, I have this new menu item with nothing there
yet but now we're well prepared, I will make some styling changes and provide
the finished code at the beginning of next module and then we will learn how we
can actually use the express router to work with dynamic data or in general,
data in the url and how we can use that to retrieve specific items or interact
with specific items. 

So for now, let's finish this module and let's move on. 

---