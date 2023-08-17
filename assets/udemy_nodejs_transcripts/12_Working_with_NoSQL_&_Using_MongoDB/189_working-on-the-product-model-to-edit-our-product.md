## 189. Working on the Product Model to Edit our Product

<strong><em>no description</em></strong>

Time to edit products and for this, I'll first of all work on my admin.js file
in the controllers folder. 

There we have two routes that are or two functions that are related to editing
products. 

To get edit product page which is responsible for fetching the product that
should be edited and for rendering it and the post edit product page which is
responsible for saving these changes to the database, I'll comment both back in
and let's start with get edit product. 

There the majority of the code can stay as it is but when we then fetch the
fitting product, we of course do this differently, we use product find by id and
we find the product with Prod ID like this and then we still get back products
however, well actually we don't get back products anymore, we get back one
product here so no need to store it in a constant like this and extract it from
an array, we get back one product automatically because we wrote that method in
such a way and we therefore can render this product, so this should work. 

Now let's quickly have a look at the view that belongs to this controller
action, so to this edit product.ejs file and in there, you know what I'm looking
for, we want to make sure we're always using product_id when using the product
ID just to make sure that we extract the right thing from the document we get
back from the server. 

So now with that, we get everything in place to hopefully make this edit button
work partly, if I click on it, well almost, let's leave it on this page. 

The controller should work but in the routes in the admin.js file, I of course
have a comment this get route back in, so let's make sure this is done. 

And now that if we now reload that page, we indeed see the form with the default
values filled back in. 

So now this is working but of course it's not that useful to only see the data
and we were able to fetch data before, the interesting part now would be to
update it. 

Now to update it, let's go back to the product model. 

How could we update our product which is stored in the database? 

Well let's go to the constructor and let's add a fifth argument here, the ID and
then I'll say this _id is equal to the ID I'm getting here, you could name this
_id here too if you wanted to. 

So now we accept a kind of optional fifth argument, we're not passing it in the
other places of the app but here I do at least create the option of passing this
too. 

An ID will therefore be undefined and be auto generated by mongodb or we did set
it and then when we called save, I don't want to insert one, I want to create a
new product instead. 

So for this what I'll do is I'll simply check if this _id, if that is set and if
it is set, we'll update the product otherwise we'll insert it, so I'll move my
const db function up there, I always need access to the database in both cases
and now I'll create a new variable, let dbOp for db operation and in the else
case where we insert a document, dbOp is equal to my connection to the database
and then connecting to collection and then inserting one and then down there, I
can use dbOp to follow along and actually return that. 

So now I have one case where dbOp is simply my insert command and then I return
my result or dbOp is access to my database and to the products collection still
but then here I use update one and as the name suggests, update one will update
exactly one element. 

There also is update many where you can update multiple elements at once but
here I know I only want to update one, so I can use update one and now update
one takes at least two arguments. 

The first one is that we add a filter that defines which element or which
document we want to update, so here again I'll pass a javascript object and we
can filter for equality also or run more complex queries which you again can
learn about in my mongodb course if you want to and here I only want to find a
document where the _id is equal to and now again I'll create a new mongodb
objectid to which I pass this _id, so the ID which is part of that object here. 

So I'm looking for a document where the ID matches the ID I have here in my
product I'm currently working with and for that document, we now as a second
argument to update one, we now specify how to update that document. 

This again is a javascript object where we describe the update and this is now
not the new object, so we don't say this here as you could imagine that we tell
mongodb find me the existing document and replace it with this, update one does
not replace. 

Instead we have to describe the operation and we do this by using a special
property name which is understood by mongodb, kind of a reserved name you could
say, $set. 

This again takes an object as a value and here we describe the changes we want
to make to the existing document which we found with this filter. 

And here you could actually say this and you would instruct mongodb to simply
set these key value fields which you have in your object here to the document it
found in the database and therefore since these are only key value pairs which
exist in the document in the database, it will update the values of the document
in the database with your new values. 

You could also write this in a more verbose way and explicitly say title should
be equal to this title and so on but since we want to replace all fields, we can
just say this here. 

And now with that we have a database operation that will update an existing
database object, by the way the ID will not be overwritten or anything like
that, only the other fields are. 

So with that let's go back to our admin.js controller and and in post added
product, that is the part I want to work on in the next lecture to make sure
that we actually are able to save our product. 

---