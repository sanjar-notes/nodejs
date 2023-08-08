## 212. Creating the Product Schema

<strong><em>no description</em></strong>

Ok so time to fix our code and make it work again. 

And for that first of all, I also connected to my mongodb server with compass
again and there I want to clear everything so that we can start from scratch
essentially and therefore I will go to my shop database and simply delete that
entire database, it will again be created on the fly or when required when we
start inserting data. 

Now I've got a problem, I connected with the wrong user where I'm not allowed to
delete a database because I connected with a user who has only read or write
access, so I'll just delete the collections here of course, the alternative
would be to simply connect with a user where I am allowed to manage the overall
database but this will do for now. 

With that I also implicitly got rid of the shop database and now we can start
working from scratch again and let's start working with it by making sure that
we can create products and for now, products that will simply use very simple
data without taking the user into account for now and where we can simply add
them through the admin controller. 

So I'll go to my product model, to the model file and there I will eventually
remove all the commented out code, I'll leave it here for reference for now and
first of all in here, we need to import mongoose. 

So I will require mongoose here, whoops, mongoose like this. 

Now with this imported, I'll create a new constant and I'll name it Schema with
a capital S, the name is up to you but I will use something from the mongoose
object I imported, I will use the schema constructor here. 

This constructor allows me to create new schemas and here I will create a new
schema, a new product schema, you can also name this however you want, I create
a new schema by instantiating a schema object by calling new schema using that
constructor here. 

Now this is just how mongoose works and to this constructor here, I pass a
javascript object and in that object you now define how your product should look
like, so you now define the data schema of a product in our case here, so this
is how you set up such a blueprint. 

In that object, you define a schema with simple key value pairs, so for example
our product will have a title. 

Now you don't just define which keys you have but also which type these keys
will have and that's important and the type I define here would be string,
string is a default javascript object hence we can use that here. 

And this would say ok so here I create a schema for an object which I will
eventually be able to work with which must have or which will have a title that
is of type string. 

Now important in the mongodb module, I mention that mongodb is schemaless so why
do we now start to create schemas? 

Well the idea simply is that whilst we have the flexibility of not being
restricted to a specific schema, we often will have a certain structure in the
data we work with and therefore mongoose wants to give you the advantage of
focusing on just your data but for that, it needs to know how your data looks
like and therefore we define such a schema for the structure our data will have.


But important, we can still deviate from this by assigning a title like this, we
could even work with a product and create a new one and save it to the database
without setting a title because we still have the flexibility of not enforcing
this, though what we can do is we can pass an object instead of just the type
here as a value and then set a type property which could be set to string and
then set required to true, this is basically a more complex way of configuring
the value for this key and here we would say well the type of this is a string
as before but it's also required and now we indeed give up some of the
flexibility we had before and we force all objects to have a title but in the
end in our application, every product needs to have a title indeed because we
will run into other errors otherwise, for example when outputting products in
our views. 

So having some kind of schema makes sense even though we have the flexibility to
deviate from that and it really just depends on your application, whether you
need all that flexibility or whether you want to have some structure and you
want to have some tool, mongoose that takes some structure and then helps you
work with that data. 

So that was a lot of talking about schemas but it is important that you
understand why we now all of a sudden start working with them, it's just a
deliberate decision to give up some flexibility but gain other advantages. 

Now of course a product doesn't just have a title, we also need to have a price
and there we can set the type to number for example and then this would also be
required and we also want to have a description and image url. 

So we'll add a description here, this will be of type string and let's say this
is also required. 

Now of course you can always deviate from my setup here but I want to require
that all and we'll have an image url and in that image url, this will be of type
string because it's just a url and this will also be required. 

So that would be my product schema, this is basically a description of how a
product should look like in my application. 

Please note that I don't add _id here because this will still be added
automatically as an object ID so we don't need to define that here, the user ID
is something we'll add later. 

So now we got that product schema defined, in the next step we will create a
model based on the schema and then create an object based on the model and work
with that. 

---