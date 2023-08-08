## 186. Fetching All Products

<strong><em>no description</em></strong>

So let's work on our shop pages now and let's make sure we can use our data
there. 

For this, let me go to my product model again and here, besides being able to
save data, I of course also want to be able to get my products, so I'll add a
static method again and I'll name that fetch all. 

Now here I want to interact with my mongodb database to fetch all products. 

For this, I will again return and then use db collection to tell mongodb to
which collection to connect to and here the collection I want to connect to is
products of course and then there, mongodb has a method for finding data which
is called find. 

Now find could be configured to also use a filter, for example we could find all
products that have a title of a book and there are more elaborate filters than
just equality filters available too, again something I cover in great detail in
my mongodb course if you want to learn more about that. 

Here I of course want to find all products for now. 

So I want to find all products which I can do by just calling find like this. 

Now the important thing about find is find does not immediately return a promise
though, instead it returns a so-called cursor. 

A cursor is an object provided by mongodb which allows us to go through our
elements, our documents step by step because theoretically in a collection, find
could of course return millions of documents and you don't want to transfer them
over the wire all at once. 

So instead find gives you a handle which you can use to tell mongodb ok give me
the next document, ok give me the next document and so on. 

That being said, there is a toArray method you can execute to tell mongodb to
get all documents and turn them into a javascript array but you should only use
that if you know that we're talking about let's say a couple of dozens or maybe
one hundred documents otherwise it's better to implement pagination which is
something we will implement at a later point of time in this course. 

So for now, let's use toArray and then this returns a promise and here we can
again catch any errors we might be getting but most importantly here, we should
have our products and we can log our products here and then also let's return
our products in here and let's see if that works the way we want. 

So now we have a fetch all method that hopefully works. 

One important thing is I of course need to get access to my database by calling
get db in fetch all, just as I do it in save and now let's head over to our shop
controller and there, we have the get products function. 

Now this is the function I want to work on now and instead of find all, let's
now use fetch all because that is how I name the method and there I should get
my products and hopefully I get them in a format that works, let's see. 

Let me also go to my shop routes now and here, get index and get products, that
should be fine, let me comment out all other routes for the moment because we
can't work with them right now because we have no code that would support them. 

By the way in the shop controller, you also want to make sure that get index
works by also using fetch all in there, so just as we did it in get products, we
want to do the same in get index. 

Ok so now I got some code in place, let me go back to app.js finally and comment
in that shop routes import and not just comment it in of course but also
uncomment this middleware down there. 

And now we hopefully have a set up where we can actually reload our root route
let's say, so just localhost 3000 and here we go, here is our product just like
that and of course it works automatically because I didn't change any property
names. 

If you suddenly store the title in a field named name, you would have to adjust
your view and so on. 

Well and there is something where I want to adjust my view and that is related
to how we work with the IDs but we'll see it in the next lecture. 

---