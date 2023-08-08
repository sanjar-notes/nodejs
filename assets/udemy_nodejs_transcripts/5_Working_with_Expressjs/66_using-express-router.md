## 66. Using Express Router

<strong><em>no description</em></strong>

We're nearing the end of this module because we already learned a lot about the
core concepts of expressjs and this therefore is a crucial module because all
the rest of the course will basically build up on this and this knowledge of how
expressjs works. 

Now even though our dummy app here is really simple thus far, we're already
putting all our code into the single app.js file which is therefore getting
bigger. 

Now obviously for an app of this size, it's not a problem at all, it's still
pretty small but typically we want to split our routing code over multiple
files, we want to basically export our logic in different files and import it
into this file. 

We could do this, we could create files where we export these functions but
expressjs actually gives us a pretty nice way of outsourcing routing into other
files. 

And for this I'll change our folder structure a bit, I'll add a new folder which
I'll name routes. 

Now you don't have to name this, you could name it differently too but it's a
convention you often see, that you put your routing related code, so your code
that should execute four different paths and http methods, that you put that
into files which you store in the routes folder and there since we're building
or we're slowly building towards an online shop here, I'll have a route which
I'll name admin.js because this should be the route that handles the creation of
products which the admin of the shop can do. 

I'll also add another file and that will be shop.js, so basically what the users
see let's say. 

Now I'll not build the full shop here, we'll slowly develop it over to the next
lectures and modules because it uses a lot of cool features like databases and
so on but we can at least start putting our code into these files here. 

The add product route and this product post request should certainly go into our
admin.js file because these are routes that are reached by the admin and the
general route here should go into our shop.js file, so that users that are
visiting our front page see this route. 

Now one convenient feature offered by expressjs to achieve this is to go into
these files and import express again, you can and you typically do import this
into multiple files and then we can use a feature of it called the router. 

Now you can also create this with a lowercase r at the beginning, the name is
totally up to you and I do create that router by calling express.router and this
is a function I execute. 

This router is like a mini express app tied to the other express app or
pluggable into the other express app I'll say which we can export here, so here
I can use module exports and set it equal to the router. 

Now of course this doesn't do much, we have to use that router to now register
things and actually I'll name this here with a lowercase r to be in line with my
other names, this however has to have a capital case r. 

So now the router here can be used to again define a use function for all
requests, a get function for get, post for post and so on So basically we can go
back to the app.js file, cut these two admin routes from there, put them in here
in the admin.js file and simply replace app with router here. 

Now the router gets exported, so the router now has these two routes registered
because we exported here and this is the object on which we registered these
routes, the other code can stay as it is because the router functions here
basically work in exactly the same way as the app use function does or the app
get and so on function does, I'll rename this to get though because I only want
to handle get requests to add product and return this form and with that, with
this exported here, we can now import that into the app.js file. 

Now for this, I'll add an import at the top separated from express to make sure
or to make clear that this is my own file and I'll name it admin routes, the
name is totally up to you but I do require a relative path to the routes folder
and that in there, the admin file and you can omit the .js as I already
explained, this will be added automatically. 

So now this is importing this router object here and this router object in turn
has these routes registered and the nice thing is about this router that it is
actually a valid middleware function. 

So we can take admin routes and just call app use and put our admin routes in
there, just like this, not calling it like a function, so without parentheses
but simply just the object itself, the router object we're exporting in this
file. 

We can use this here and now this will automatically consider our routes in the
admin.js file when filing the request through this middleware here. 

Now just before, the order matters so if we put this after this middleware, we
will never reach that so this hasn't changed. 

Now we can do the same for our front facing route here, let's go to the shop.js
file and there again, feel free to pause the video and try this on your own, try
to implement this with the express router as we just did in the admin.js file. 

Were you successful? 

Let's import express first of all by requiring express, then let's create that
router object by calling express.router as a function, let's export the router
here and let's then use app use or paste in what I copied but replace app with
router and maybe use with get. 

You don't have to do that, the use method would exist too but now we only handle
get requests here. 

Now we can go back to admin.js, excuse me, to app.js and import all routes there
too, the order of the imports doesn't matter, so my shop routes I require them
from the routes folder and there from the shop.js file and now here again, the
order matters, we should register this second. 

Now if I save this and I reload add routes, add product, this works. 

Now actually here's one important thing to understand, even if I would switch
the position here and have shop routes first and I reload, it would work and we
would not end up in this route but this only happens because I have get here. 

Get, post and so on will actually do an exact match here. 

If I would use use here as I did before to handle any incoming http method, then
if I reload here we see hello from express again. 

So this exact matching is not achieved by using the router but because we use
get here and that would have been the same if we stick to the app way of doing
this in the app.js file we had previously. 

So get, also make sure that it's not just a get method but this exact path and
therefore now if I enter some random stuff, I actually get an error because now
I got no single middleware that would handle this but I do have my route set up
here now and split up and then registered here and as I mentioned, it's not the
worst practice to still care about the order here even though at the moment,
it'll work fine no matter what the order is but if you ever change something
back to use, it would matter and therefore why don't we just care about it right
from the start. 

---