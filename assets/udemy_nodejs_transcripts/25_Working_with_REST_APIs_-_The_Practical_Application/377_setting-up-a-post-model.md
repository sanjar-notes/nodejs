## 377. Setting Up a Post Model

<strong><em>no description</em></strong>

So time to add some database logic and I will again use mongodb and mongoose and
I will use that same mongodb atlas server we configured earlier in the course. 

So go back to that mongodb module if you want to see how that worked and if you
want to use MySQL or something like this, you can of course also take the
knowledge you gain in the MySQL related modules of the course and implement your
own SQL solution here, to follow along smoothly you should use mongodb though. 

I will again use the mongoose package, so let's install it with npm install
--save mongoose and that will be required to connect to the database and to then
of course also create our mongoose models, store data and so on. 

I'll restart npm start thereafter and now first of all let's connect. 

For this let's open the app.js file and let's import mongoose here by simply
requiring mongoose. 

Now as you learned in the mongodb and the mongoose modules of this course, we
then esstablish a connection by using mongoose connect here and now we need a
url, a connection url. 

Now as I mentioned, I'll use that same connection url I used before in the
course so that does not change, I will just copy that, here it is, that is my
atlas server to which I can connect and this now establishes a connection and
then I can add then and a catch block, catch in case this connection
establishing fails, then I want to log the error but if we are successful, if we
are in the then block here, then I will start my node server and start listening
to requests. 

If we save that, it now gets restarted and it should succeed, you can ignore
this deprecation warning here by the way. 

Now we're connected to mongoose or to mongodb through mongoose and now what can
we do? 

Well we have to create some models to work with right because that is how we
interact with the database ultimately. 

So let's create a models folder here in our node rest API and I'll create a
post.js file in there to define how a post should look like. 

There I will simply import mongoose by requiring mongoose from the mongoose
package, we can then extract the schema from that mongoose object, that schema
constructor and use that to create a new post schema, you can name that however
you want but you use new schema to now define how a post should look like in
your database and in your application. 

Now you can of course define this in whichever way you want, I want to have a
title in there which will be of type string and you learned all about that
schema declaration thing in the mongoose module, so I'll be walking through that
a bit faster. 

So type will be string and let's say it's required and we then also will have an
image url or image or however you want to name it and that will also be a
string, it will be a url pointing at that file and this will also be required. 

Now we'll also have a content of course where the type is string as well and
which also is required, so thus far not too exciting. 

Now I also will have a creator here and that will later be a link to a user, for
now I don't have that so for now it will just be an object and be required but
this is only temporary, we'll change this later. 

So this is my current set up. 

Now I will pass an option to the schema constructor which we haven't seen
before, we can configure this and in that object I'm passing as a second
argument to the schema constructor, I can add the timestamps key and set this to
true and mongoose will then automatically add timestamps when a new version is
added to the database, when a new object is added to the database. 

So we automatically get a createdAt and updatedAt timestamp out of the box then
and you can learn more about that feature in the official mongoose docs of
course. 

Last but not least, we now need to export this and you learned that we don't
export the schema but a model based on the schema. 

So I use mongoose and then the model method to create a model based on a schema,
you can name that model however you want, I'll name it post and therefore this
will create a post database and I will export my post schema here or use my post
schema, so this is the model defined. 

One important note about my connection string by the way in app.js, there I'm
connecting to a database and I will connect to my messages database, you can
name this however you want. 

So now we'll connect to this database and thanks to this model, there mongoose
will use a posts collection for us when we start using that model. 

Well speaking of that, let's start using that model in the next lecture. 

---