## 119. Extracting Dynamic Params

<strong><em>no description</em></strong>

So time to extract this ID from the url and for that let's go to the routes
folder, there in shop.js. 

we want to handle a new route and I will add it below my all products route
here. 

It will be a get route because we want to display a new page for now and part of
the path is products but that's not everything, we also have this dynamic
segment, the ID. 

The express router supports us with this, we can tell the express router that
there will be some variable segment by adding a colon and then any name of our
choice like Product ID, later we'll be able to extract that information by that
name here so remember it. 

The important part is the colon here though, this signals to express that it
should not look for a route like products product ID but instead that this part
here can be anything and it will simply route or load this route for this path
then and we will then be able to extract that information through that name. 

This has one important implication, if you also have another route like router
get products delete let's say, so that is a normal route, this is not a dynamic
segment, the order would matter. 

If you order it like this and keep in mind that your code is parsed from top to
bottom and the request goes through that from top to bottom, if you order it
like this you would never reach that route because if you had a route like
products delete, expressjs would already fire at this route or would already
handle it in this route here because delete would basically be treated as the
dynamic segment. 

So if you had a dynamic segment and a specific route, you would have to put the
more specific route first so that for products delete, this handles the request
and thereafter it'll not continue its journey because you don't fire next but if
you then have something else which does not match products delete, then you
would go into that dynamic route. 

So this does matter, here however we don't have that case, I just want to
mention it, so for now let's simply connect a controller where we then can
handle this incoming request and where I then can show you how you can get this
information out of the url and for this, let's go to controllers shop.js and
there simply add a new controller, I will add it below get products, the
position doesn't matter but logically here we get all products so now I also
want to add the function where we get one product. 

So here I will have get product, whoops response next like this and in there
let's now extract that dynamic path segment or the value it holds to be precise.


So this will be our product ID, I'll store it in a constant named prod ID, that
name is up to you and we can get access to it by accessing our request and then
expressjs already gives us a params object on our request and on that params
object, we can access our product ID and we can access product ID here because
we use product ID in our route shop.js file as a name after the colon. 

So the name you use here after the colon is the name by which you can extract
the data on this params object. 

And let me show you that this works by logging this, Prod ID and I will then for
now simply redirect to the starting page, later we'll of course render a
different view but for now this will do. 

And with that I can now go to shop.js and use my controller here, so connect the
shop controller get product function here and with this connection set up, if I
now go back and please note I'm still on that route with the dynamic segment, if
I now reload this, I'm getting redirected which means we handle this, we don't
get the 404 page anymore and in the console here, I see my dynamic segment
logged out through this line. 

And that of course means we can not just log it, we can also use it. 

---