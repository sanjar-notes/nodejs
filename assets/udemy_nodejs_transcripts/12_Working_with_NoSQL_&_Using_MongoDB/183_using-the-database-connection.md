## 183. Using the Database Connection

<strong><em>no description</em></strong>

So now we're importing something which allows us to get access to the database
connection we set up initially when starting our server which now is a concept
that we can reuse. 

So in the save method of the product model, I can now get access to my database
by calling get db, remember get db does simply return that database instance we
connected to, so now we have a connection which allows us to interact with the
database and then here in mongodb, you can call collection to tell mongodb into
which collection you want to insert something or with which collection you want
to work because remember in mongodb you have databases, collections and
documents. 

We have a database connection here, so the next level is a collection. 

So here we can connect to any collection and just as with the database, if it
doesn't exist yet, it will be created the first time you insert data. 

So here I'll connect to a products collection. 

Now on that collection, we can execute a couple of mongodb commands or
operations. 

Now a full list can be found in the official docs and of course you'll learn all
about them and all the details in my full mongodb course which I mentioned. 

In the official docs, you can click on mongodb server and here for example click
on mongodb crud operations to learn how to insert find, that is what query is,
update and deletes documents and you'll see all the examples here and all the
commands and how to configure them and so on, so this is a great place for you
to dive deeper besides the other course I mentioned but of course here's a short
introduction too. 

If you want to insert data, you can do this with insert one or if it's multiple
documents at once, insert many. 

Insert many then takes an array of javascript objects you want to insert, insert
one which I'll do here because I want to insert one product only takes the
object you want to insert. 

Now what do you mean with object? 

Well you would simply pass an object where you have like for example name, a
book, price 12.99 and so on, so this is something which would be valid code,
that would insert such a document into the database. 

By the way this is not json, this is a javascript object but it will be
converted by mongodb . 

However here in our case, essentially it's the product which we want to insert
right, so we could just say this and see how that works if we try to insert this
into our database. 

Now this is all we need to do right now, insert one then returns us a promise,
so we have then and catch and we can log any error we found or we can have a
look at the result we get back, so we can console log the result. 

With that out of the way, let me remove the sequelize model and export our class
with the save method and now with that, we fixed the model file, let's now go to
the admin.js file. 

And here obviously we got a couple of methods or a couple of functions which
still use parts of the model that won't work anymore, like this one here,
request user create product for adding a new product. 

This will not work anymore, for now we'll have to create a product without
storing something about the user, we'll reintroduce this later again. 

So for now, we can overwrite this here though and I also want to comment out my
other methods because these will not work anymore, so let's comment them out. 

We'll comment them back in later once it works and therefore in the admin
routes, here routes admin.js, there I also want to disable all routes that will
not work anymore. 

So essentially that's all but this post route. 

So here for getting all products, this will not work anymore and all these
routes down there will also not work anymore but these two routes should still
work for add product. 

So now with that, I need to fix one more thing in the app.js file, here I need
to import .mongo connect here from my database utility file. 

And with that now we're not only connected but we should also be able to insert
a new product already, so let's try this out. 

Visit localhost 3000/addproduct and this won't load because in app.js when I
commented out the code here in app use, well I should at least call next
otherwise every incoming request will die here. 

So with that changed, now if we reload, we are back to our admin add product
page. 

Now let's simply check this and see if it works by adding a product. 

Now I get an error here regarding create product and that of course makes sense
because in the admin.js file, I didn't change any code. 

So let's work on that code next, so let's make sure that we can add a product. 

---