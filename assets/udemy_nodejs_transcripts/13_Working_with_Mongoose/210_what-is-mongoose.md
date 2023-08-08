## 210. What is Mongoose?

<strong><em>no description</em></strong>

So what is mongoose? 

Mongoose is an ODM, an object document mapping library and that's really similar
to sequelize which was an ORM, an object relational mapping library and the
difference of course just is that mongodb is not a relational database, it's a
document database, it thinks in documents and hence we have an ODM here. 

So the idea stays the same though, we have some data, some entity in our
application, let's say a user and we want to save that to a collection, we want
to map our javascript object to a document in a collection that could look
something like this and of course we can write the query for that on our own,
that is exactly what we did in the last module but it would be a bit easier if
we could just focus on our objects, on our data and see how it should look like
and then work with it and this is not even the final syntax you see here, we can
use mongoose a bit differently than you see it here but even that would be a bit
more concise. 

So just as sequelize, mongoose tries to allow us to define models with which we
then work and where all the queries are done behind the scenes which of course
does not mean that we can't influence and that we can't change some things. 

The core concepts are that we work with schemas and models where we define how
our data should look like and then we have so-called instances where we
instantiate our models, so where we create real javascript objects we can work
with that are based on our blueprints and once we get that setup, we can run
queries and there we again use our objects, we use our models and we can then
query the database but through mongoose with various helpers we get, some
syntactical sugar and so on. 

So that's the idea behind mongoose, really similar to what sequelize did for SQL
and therefore with that, let's dive in, let's add it to our project and let's
see how we can use it there. 

---