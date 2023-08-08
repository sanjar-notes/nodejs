## 79. Sharing Data Across Requests & Users

<strong><em>no description</em></strong>

I'm back in the project and I actually changed the html code and the styles a
little bit, you'll find all css files and html files attached and just make sure
to move the html files into the views folder and the css files into the css
folder in the public folder. 

I did this to well change the styling a little bit and also add a little bit of
additional markup which we'll use in this module but no worries, I will walk you
through all of that markup and regarding the styling, it's just a little bit
nicer to look at right now and I also added some styling which we'll need in
this module. 

So with that, I can of course visit the page on localhost 3000 and this is how
it looks like right now, a little bit nicer than before in my opinion but of
course you can always style this to your needs but let's now focus on the data. 

And right now, we don't really work with data in our app right in admin.js for
example, we do get that data for a product here in a host route but we just log
that to the console, we're not storing it, we're not working with it and working
with it is kind of hard right now because we have no database where we could
store it permanently but one thing we can of course do is we can store it in
javascript variables and see how that works and if these are then shared across
incoming requests from different users and that of course will hold some
important learnings because you often well don't want to share such data. 

So let's see how that works before we then later in the course move towards a
more permanent database driven solution. 

So let's say the incoming product title which we output here should be stored in
a more permanent place and in general, I actually want to also add some fields
to the form then later so that we can add more for a product than just the title
but step by step. 

So let's start storing that title which we get here and just to bring that back
to memory, right now we got this field here and if I submit this, well then I
get this object with the key title and the value the user entered. 

So how can we store this? 

Well we could add a variable where we store it in and the first thing we could
try is we could add a variable here in admin.js, let's say we create a new
constant here which I'll name products which is an array and keep in mind even
though it's constant, the array can receive new elements because the array
itself is still the same object, we just add or remove elements to it but that
doesn't affect the overall holding object. 

So now I got my products here and I actually want to export my products, so what
I'll do down there is I will use a different syntax where I export my routes and
export a router here and exports products and export my products constant. 

This has one important implication, since I changed the way I export my routes,
I have to go to the app.js file and with that in the app.js file where I import
my admin routes here, well actually this is the admin data and there, I want to
access the routes object because there will be such a routes object because I'm
creating it here. 

So admin data refers to all the exports you could say and there we now have
routes and products and therefore when I do import my routes, I have to import
them like this, of course admin data is then also something I have to change up
here in the import. 

So now I got this adjusted and now I got my products exported too, products is
an empty array. 

Now in here, in router post let's take the products and push a new element into
this array, a new object let's say and that object will have a title which is
the title I'm getting, so request body and keep in mind that also is an object
with the title property so I will extract the title with the dot notation, I
could of course just push the overall request body since that will be an object
of the exact same structure but later I want to add more fields here and
therefore, I will create a new object here, also to make it a bit clearer to see
what's happening here. 

So now we're adding this to products, now in shop.js where we output all our
products or where we want to do that at some point, we therefore need to get
access to the products and for this, let's add an import up here, let's import
admin data by requiring admin, so this admin.js file where we do export its
routes, something we're not interested in in this file but also this products
array, so now here let's console log admin data products so that should be the
array. 

Now save everything and now let's simply see what we get. 

If I reload this page, the shop page, I get an empty array which makes sense
because initially, this is an empty array, we export it, that makes sense. 

So let's go to add product now and let's add a book here and it clicked add
product, we're back to the shop page and we see something interesting. 

We see the array with the book inside of it and that console log statement,
where is this actually coming from? 

Well that is coming from the shop.js file here, we can also make this clearer by
adding shop.js here and logging the products, so logging two things to make it
clearer what is responsible for the output, so shop.js is logging the empty
array and now let's try outputting that book here and now we got shop.js with
the array with the book in it. 

Now this is interesting to see, so we can export something, some object or
array, a reference type therefore and if we change that in the other file, it
also gives us the update here. 

So this is interesting, this is one way of sharing data and to be honest we'll
later use different ways because this has one disadvantage. 

Here if I reload shop, we still got that in there. 

Now let me open up a totally different browser, I'm in Firefox here and I also
visited localhost 3000. 

So this is a totally different browser and this is kind of like a brand new
user, it doesn't share any cookies with the other browser, nothing of that kind,
it used the same IP address but that doesn't matter here. 

It's a brand new request as if it were made from a different machine and you
will see, I still log this, so this is actually data which is inherent to our
node server as it is running and therefore, it's shared across all users. 

Sometimes this is what you may want but very very rarely to be honest, actually
you will probably never implement this, you always want to fetch data for a
specific request and if that happens to be the same data you show for all users
that send this request, this is fine but sharing this data across requests,
across users is typically something you don't want to do because if you now edit
this with user A, user B will see the updated version even though you might not
want to show that. 

Maybe it's added that normally it wouldn't have been saved to the database yet,
so you don't want to show that to the other users yet, maybe it's some personal
data. 

So this is a pattern we can use for now here and it's fine for practicing what
we want to practice here but later we'll learn about a technique to share data
in memory here, in the node app across different requests but only for one and
the same user and not across users because now we have shared data across
requests and across users and we will later of course also learn how to use a
database. 

But for now let's stick to this approach, let's use that for some dummy data
sharing and let's see how we can get this data into our view now. 

---