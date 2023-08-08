## 63. Handling Different Routes

<strong><em>no description</em></strong>

So let's see what else expressjs can do for us and let's also start building a
more exciting application then. 

So for this, we want to handle different routes, different urls. 

To do that I'll first of all remove our dummy middleware which is not doing
anything and this second one should only trigger for requests that go to just
slash nothing. 

Now how can we filter for such requests? 

Well I mentioned that the use function here has multiple versions, you can see
that here for overloads, so we basically have four different or five different
ways of using that function. 

You can see a great explanation in the official docs in the end, on
expressjs.com there I'm in the API reference for the version we're using here,
the latest version and there you find app.use where you find the explanation of
how to use it. 

Now don't be confused that this is only one definition instead of the five I've
promised, the five basically just is made up of different combinations, so in
the end, this is how you can use app.use. 

You got an optional first argument which is some path and that already is what
we're looking for, this allows us to filter out certain requests, however this
works a bit different than our if statements did before but I'll come back to
that. 

Then we have the callback so basically the function that should be executed and
we can have more than one of that callback, we can have as many as we want, we
can also have multiple path filters here. 

Now you can obviously read more in the docs here but let's just use it and learn
during the course. 

So we can add a path at the beginning, for example just slash, this however is
the default by the way and now we would handle this for just visiting slash
right. 

If I reload, we still see hello from express, Now what happens if I for example
enter /add-product? 

We still see hello from express and we still see I'm in another middleware, so
this middleware gets executed for both slash and add product because this does
not mean that the full path, so the part after the domain has to be a slash but
that it has to start with that. 

Now of course every route starts with just a slash and then we have different
other criteria. 

So what we can do is we can simply duplicate this and add it before this
middleware and add /add-product. 

Now why before this middleware and not after it? 

Because remember, the request goes through the file from top to bottom and if we
don't call next, it's not going to the next middleware. 

Well I am not calling next here, so in the end if we have /add-product, this
middleware will be reached first because top to bottom, add product will match
this middleware and since I don't call next, this middleware will never get a
chance of handling that request even though the filter here would have well,
matched that request too. 

So here if I just add the add product page like this and I save this, you will
see that on /add-product, we see the add product page and on any other path
including random stuff or just slash nothing, you see hello from express and
this is how we can use that middleware approach to control what is getting shown
and the order here as well as the fact whether we are calling next or not
matters a lot. 

By the way if you are sending a response, this is a good indication that you
never want to call next too because you don't want to execute any other response
related code just as before with vanilla nodejs, you don't want to send more
than one response, this won't work and will result in an error. 

So this is the code we can use here, this is the code that allows us to route
our requests into different middleware and if we have a middleware that should
be applied to all requests, we would simply add it on top of all the other
middlewares and then add it like this. 

If we don't add a filter or a filter that matches all requests it should match,
then this middleware will always run first and if we call the next function,
well then of course the request will also be able to continue. 

So if we have this middleware here which allows the request to continue and we
have console log, this always runs well with this code. 

What we will get is that if I save this, if I reload here and I also go to add
product here, we have this always run twice because well, this always runs,
that's just how it works. 

So this is how the middleware works and how you can work with it to funnel your
request into the right place. 

---