## 218. Adding and Using a User Model

<strong><em>no description</em></strong>

We worked on the admin side and on the basic product, let's now add a user again
and let's see how we can add a user model, how we can connect it to a product
and so on. 

For that I'll go to my user.js file in the models folder and first of all, I
want to import mongoose here by requiring mongoose, like that. 

So let's now work on the user schema. 

Well first of all, we need define the schema, so the user schema. 

The user schema is defined by using something from the mongoose package which
you don't have to but I will store in a separate constant, so mongoose schema. 

With that we can call new schema down there and I pass a javascript object to
that constructor and in that object, we describe how a user should look like. 

Now here I will say that I want to have a name where the type of data will be a
string and this will be required. 

As a next field, I want to have an email as well, this will be of type string
and this will also be required like that. 

Now we also used a cart before and I still want to embed the cart into my user
document, that hasn't changed just because we use mongoose. 

So we'll add my cart here and now in that cart, that will be an embedded
document and we can define it just like that, I will add items here and items
will be an array and this is how you define that you want to store an array in
here, you simply create an array and then you add, what is inside of this array?


You could say an array of strings if you have an array of strings or numbers or
booleans or an array of well documents, that of course is also possible. 

Now I want to have an array of documents where I have a product ID which I'll
configure with this document here, I'll come back to that and I'll have a
quantity and the quantity I'll configure that right away will have a type of
number and is required. 

Now what's the product ID here though? 

The product ID will have a type of and now I need to get something from the
schema, there we have a types field and there we got all these special types
like object ID, so I'm telling mongoose that this will actually store an
objectid because it will store a reference to a product and that this also is
required. 

Now that is a bit of a more complex schema therefore because we have an embedded
document and we have an array of then even embedded documents but this is how a
user should look like. 

Now just as before, I'll export this by calling mongoose model, give this a name
and the name will be user hence this will be stored in a users collection
because mongoose will automatically take the plural lowercase version of that as
a collection name and I pass my user schema here. 

Ok so now we get everything we need to inform mongoose how a user should look
like, now of course I want to work with a user. 

And for that I'll go back to the app.js file and I will actually create a user
here before we start listening. 

For that let me import the user model again in app.js and with that import
added, I can create a new user by simply calling new user and just as before, I
pass a javascript object where I configure it, where I assign a name, where I
assign an email and where I also need to set my cart and that cart will have an
array of, well empty items. 

So this is my user, I can then call user save and this will be done when I start
my server. 

So here after it restarted we should have a user already, if we refreshed the
overall database server, we indeed see our users and there we see one user with
that nested data. 

So now with that user created, it's that ID I'm interested in, so let me copy
that ID and go back to the app.js file and comment this middleware back in. 

Here I again will find a user by ID, I just need to paste in that ID of that
user we just created. 

Find by ID is a method provided by mongoose so this will work, we get back the
user here then and then I can simply store that user in my request and keep in
mind, this is a full mongoose model so we can call all these mongoose model
functions or methods on that user object and therefore also on the user object
which I do store here. 

So this should work, if I now save this for every incoming request, it should
actually give us that user. 

Now one issue is that with every restart of the server, we also create a new
user as you can see here, so let me delete that new user because I have my user
creation code down there and I don't check whether I want to create one or not. 

So what I'll quickly do is I will first of all see if we do have a user with
user find one and find one with if I give it no arguments will always give me
back the first user it finds and then here in the then block, I will have my
user object and only if this is undefined so if it is not set, only then I will
create a new user. 

So therefore now if I refresh this we shouldn't have a new user, if I however
delete that first user here and I therefore temporarily get rid of that let's
say and I save and it restarts, now if refresh my users collection I do have a
new user and now I just need to grab that ID and paste it back in here and now
we get a set up where I don't constantly create new users. 

Ok so this is how we add a user model and how we basically use it but now of
course we want to use it in conjunction with the products model and with the
products. 

So let's do that in the next lecture. 

---