## 357. Using Stripe in Your App

<strong><em>no description</em></strong>

You can simply Google for Stripe and you should find their page. 

And they have a really great documentation, by the way, in case you want to use
it. 

So definitely dive into developer documentation, but we can simply click create
account here and then create an account real quick. 

Now once you got your account created, you can already get started. 

First of all, you need to validate your account. 

So make sure you click on that verify email link. 

You get in an extra email. 

And once you did that, you are ready to get started. 

Now, important. 

Under developers, you'll find a bunch of API keys which you will need to add
Stripe. 

And we are seeing special testing data here, which is fine for our development. 

If you want to build a real application, you want to push it to production, you
would switch to your life data here for this you have to activate your account
though will not do that here. 

We'll work with the test data to get started and with that we can go back to
home and there click on Grow Your Online Business with payments and read the
docs. 

Now this takes us to the Stripe documentation. 

It turns out that you have various different ways of implementing payments with
Stripe, and of course you can check out their entire documentation to learn all
about the different ways of collecting payments. 

Now here we can go to web under, build your own and click on Integrate Stripe. 

JS This simply allows us to implement a JavaScript library on the front end. 

So in our views, to make that whole payment process very, very smooth and
straightforward. 

So what we'll do is we'll pick this script here and go back to our code and
they're in the checkout. 

Edge's file. 

Let's go to that diff where we output our sum and let's actually add a new diff
below it, which also has that centered class. 

And in this new diff. 

We can paste in that script, but not just this script. 

Let's also add a button here with an ID of order dash BTN and a class of button
for the styling where we can say Order just like this. 

Now let's add another script tag here where we now will write some inline script
and that's all front end JavaScript. 

So not running with Node.js on our server, but instead executing in the browser
of our users. 

Now here we can, first of all, call Stripe with a capital S like this and insert
your local testing key. 

Now you'll find it here in the documentation already. 

Prefilled. 

This is the key. 

You can also see in the developer part of your home screen. 

So put in other words, here under developers API keys. 

This. 

Is the key I'm talking about. 

This is the same key you see here. 

So you can grab that key and enter this as a string. 

As an argument here for this strip function call. 

This strip function is available because we're running this scripture, we're
importing this script, and thereafter let's get access to our order button by
using document, get element by ID, that's DOM API, which we can use in
JavaScript, which runs in the browser to get access to an element on the page. 

And here I will get access to that button by its ID by simply passing the ID
here. 

So now we simply have access to the button where I now want to listen for a
click. 

So on the order button we can add an event listener, a click event listener, and
then pass a function which should execute when that button gets clicked. 

Now here, we'll not send the user to our own back and to our own roots, which we
registered instead. 

Here we'll let Stripe do some magic. 

We'll use that stripe. 

Object which we created up there and call redirect to checkout written like
this. 

Now redirect to checkout takes a JavaScript object where we can configure this. 

What this will do in the end is it will redirect the user to some of stripe's
pages where the user then enters credit card data and so on. 

And once all of this is done and the payment is confirmed there, the user is
redirected back to us. 

Now here we have to provide a session ID and that's the interesting thing. 

That should be a string, but at the moment we have no such session ID. 

So what do we do there? 

Well, how do we get that session ID? 

Well, for that we have to go to the controller where we in the end render check
out Aegis. 

And that, of course, is here in shop charges, the get checkout controller here,
here in get checkout. 

We now have to adjust our code a little bit because besides rendering this
checkout page, we have to prepare such a stripe session in the end now to
prepare that. 

We have to install a new package, so I'll quit my development server and go
ahead and install it by running NPM. 

Install Dash Dash Save Stripe. 

Stripe is the package name which we need to install. 

This is now a package which we can use on our server side code. 

So in Node.js. 

So let's wait for this to finish. 

And then restart my server. 

And now here at the top, we can import stripe by requiring stripe like this. 

But then this actually gives us a function which we need to execute to which we
now need to pass our private stripe key. 

That's the key you have to reveal here. 

And by the way, of course, I'll change those keys after this recording session
so you can't use mine. 

Copy that key here. 

And Enter is here. 

Now always keep this key private, so only use it in your Node.js code. 

Never expose it in one of your views because there your users could see it. 

And this is a key you should always keep private. 

Now with Stripe imported like this, let's go back to get checkout. 

So to the controller where we prepare the checkout page and in there of course
we want to gather all the product data. 

That's all fine. 

However, I will adjust as a bit and create a variable products here right at the
beginning of the function. 

Also a total which is zero initially and change this here to not create a new
constant or a new variable here, but instead use these variables here which now
simply are available everywhere in this function in any nested function as well,
whereas before this only was available inside of this function and that will
just not be enough once we made the changes we're about to make, leave that code
as it is otherwise. 

But instead of rendering immediately here, we now need to do something
different. 

Here, we need to do something else here in this promise and this then block. 

We should return stripe checkout. 

Dot sessions create. 

Remember, we needed such a session key in our template. 

Now here we're going to create such a session which ultimately gives us such a
key to create. 

You pass an object where you configure that session. 

Now one thing we can already do is we can grab render here, cut that and add a
new then block thereafter, which is why I had to outsource some data into global
or into function wide variables. 

And in this then block you will get the stripe session eventually. 

We're not done configuring it, but you will get it there. 

And then here you can then render the checkout page and all the paths, let's say
a session ID key to the template which holds session ID. 

So this session you're getting here, it will have ID field, which is that stripe
session. 

Now we'll use that in a view in a second. 

Before we do so let's configure that session because there are some things which
we do need to configure. 

For one, we need to add a payment underscore method, underscore types key here
that holds an array. 

And there we want to add card as a type, which means we accept credit card
payments. 

Next, let's add a line, underscore items key. 

And there we need to specify which items will be checked out. 

So here I want to use my products, which I basically created here and map this a
little bit because each product needs to look a bit different. 

So every product will be transformed with help of the built in map method. 

JavaScript offers on arrays and there the new object I return for every product
in the product's array, which will therefore be part of the newly returned
products array. 

We past line items will have a name which is p dot product. 

ID dot title. 

Description, which is product ID description. 

In case you're wondering why we can access title and description on product ID,
keep in mind that we populated that product ID field. 

So it's not just the product ID, it's the complete product data, which is why we
can access the title ID description. 

For example, the amount is PPI, product ID price times 100 because we need to
specify this in sense. 

The currency is used for a US dollar and the quantity is not quantity. 

That is data which stripe needs in the end. 

And that's the format Stripe needs. 

It needs an array of objects which have currency, quantity and amount and then
all the here our extra name and description fields and this needs to be named
name, for example. 

So with this reformatted data, we also give Stripe the data it needs to process
the payment, but we're still not done. 

There is more we need to configure on this session. 

Specifically, we need to add a success, underscore URL and a cancel underscore
URL. 

These are your URLs. 

Stripe will redirect the user to you once the transaction was completed or
failed. 

Here. 

I want to dynamically derive the URL and domain of the server this node script
is running on so that it is valid both here in development where we are on
localhost as well as later once we deploy this on the page with any IP or
domain. 

So here I will use request protocol which is a property again I can get from
this request object express gives us. 

That is simply HTTP or https. 

Plus colon, forward slash, forward slash. 

So this will build us something like http colon. 

Forward slash. 

Forward slash plus request. 

Get host. 

This will give us our host address. 

So, for example, local host 3000 during development or later once we deployed
it, the IP address or domain of the host we deployed it onto. 

So now this will give us that start of the redirection URL. 

Thereafter, I want to go to slash checkout slash success here. 

And now I will copy that and add it here as well and redirect to slash cancel. 

So these are in the end routes which Stripe will redirect us to once we ever
confirmed the payment or cancelled it. 

With Dad. 

We're creating such a session, we're forwarding the session ID to The View. 

So back in checkout edges, we now need to output the session ID here. 

Now we do so with edges. 

We can also inject something into JavaScript code, which is pretty neat. 

We can inject our session ID here with the familiar EJ's syntax just inside of
JavaScript code. 

In this case, inside of a string of our JavaScript code. 

With that we can be redirected to strip hopefully and then back. 

But the pages were redirected to. 

Once the transactions succeeded or failed, check out success or check out
cancel. 

Well, these routes might not exist yet. 

Indeed, if we check our routes. 

File here to shop. 

File. 

We have no. 

Check out success and check out cancel roots there. 

So let's add them maybe here below check out we need to add to get roots slash
check out slash success. 

And then another one slash checkout, slash, cancel. 

Now, when we cancel, I will in the end execute the get checkout controller
again. 

I simply want to redirect the user back to the checkout page. 

If we cancel, if we succeed. 

I need a new controller though. 

And there I want to do the same thing I did before in post order so we can
simply redirect the user here to post order. 

Now we already use post order here on slash create order. 

That is a route we don't need anymore though because we will now replace that
thanks to our new checkout flow. 

So we only need checkout success and checkout cancel. 

And for checkout success we go to post order. 

We're actually here. 

I will create a new controller, get checkout success. 

But you could have used post order as well. 

Now let's go to shop Jews and their let's copy post order and simply create a
new controller function named get check out success though as I said, you could
have also just kept post order. 

I'm just doing it here to also have to get word at the beginning because in the
end a get request will reach this controller here. 

Now in this function, you can leave everything as it is. 

We're gathering all the products from the cart and then we're creating an order,
storing that in the database, and then we redirect the user to orders. 

If we now save that, let's give it a try. 

Let's go back to our page here and there to the cart where I have two items in
there. 

Click on order now. 

And I got an error. 

Now the reason for that error is actually related to Stripe. 

You could debug it by going to app trace and logging the error we're handling
here. 

I and yet need to add a name here. 

Max. 

To be able to use this. 

So after naming this here, if I reload. 

This looks better. 

Now, here I have the order button and if I click that, you should be redirected
to Stripes page. 

Now here you can enter any email address and then some dummy card data. 

Like for two. 

For two, for two. 

A lot of four choose some date which is in the future here and then any CVC code
of your choice and simply any name on the card. 

Click Pay and this now processes this should succeed and redirects you to the
orders page in yen because it goes to the checkout success page where it is this
created. 

And indeed you should see that your cart is empty now. 

Now that all works. 

But this approach has a flaw currently. 

In the end, we confirm that an order was successful by simply running the logic
and get checkout success. 

Now we can always trigger that if we just manually route to this page. 

If I add a product to the card again. 

And now I don't order it, but I simply go to slash check out slash success here.


Does all this succeeds? 

My card is empty and I place the order without paying for it. 

You can always see your orders here in Stripe, though, if you go there. 

You will see your post orders. 

And there, of course, you only see one order. 

And that's the order we processed through Stripe. 

So the order I hacked here with manually entering the URL, of course does not
show up here. 

Only the orders that really went through stripe's form can be seen here. 

And of course, you can look into the payments you received here and for example,
see the date, the email address, the amount paid, the payment method, the name
of the user and so on. 

Now the advantage is with that, you can actually compare that to the orders you
see in your database and check if there are any fraudulent orders in there. 

So you should always do that when using this approach. 

But of course, for a large scale shop, manually comparing orders is not really
an ideal solution. 

And indeed this is a weakness that is also listed here in the docs of Stripe. 

If you go to Stripe checkout one time payments, you basically learn about the
approach we just set up. 

And there you see that you should not rely on the success URL alone. 

Instead, you have to fulfill a payment, which means make sure that stripe tells
you when a payment happened instead of a URL telling you. 

Now actually here you see that you can manually use the dashboard to check if an
order really was placed. 

So that would be our solution here. 

As your application grows, web hooks here would actually be the preferred
solution. 

The idea here is that you can configure Stripe such that it sends a request to a
URL of your choice, which you would have to manage here in your application with
routing. 

And that then tells you that the order succeeded because Stripe sends you that
request behind the scenes. 

It does not send the request to a URL of your page anyone can enter. 

Instead, it will be a request validated by Stripe. 

That's not as easy to fake. 

Setting up web hooks is a bit more complex though, but the documentation here is
really great if you want to do it. 

The biggest problem we have at the moment is we couldn't really test web hooks
here because for web hooks to work, Stripe needs to be able to send the request
behind the scenes to your Web page. 

And therefore, your web page needs to be exposed to the real Internet. 

And that's not the case for us here during development. 

It's only running on our local machine, which is why redirecting the user works
but sending such a behind the scenes request would not work. 

Hence, if you need that automated process, the stripe docs are the way to go for
the moment, using the dashboard to validate orders and to make sure that you're
really only shipping goods to users who placed a valid order is the way to go
and that is how you can implement payment with Stripe. 

As I mentioned, there is way more you can do with Stripe and of course the
official docs are the place to go. 

If you really want to build an online shop and use all the cool features Stripe
offers. 

But this lecture hopefully got you started with Stripe. 

---