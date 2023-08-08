## 152. Defining a Model

<strong><em>no description</em></strong>

With the connection set up, let's go into our models folder and there to the
product.js file and there we can actually delete everything. 

We don't need all of that right now, we'll write it from scratch. 

Here I first of all need to import two things. 

The first thing is sequelize itself, so again I will require, whoops, require
sequelize here and that will give me back a class or constructor function hence
I name this here with a capital S. 

The next thing I'll import is my database connection pool managed by sequelize,
I'll also name this sequelize but with lowercase s, so I'll basically import
what I export in my database.js file. 

Here I will import this by requiring and then go up one level into util and then
there to the database.js file. 

Now with these two things imported, we can now define a model that will be
managed by sequelize. 

So here in this file below my imports, I'll create a new constant and I'll name
it product because in the product.js file I want to define my product model. 

Now this model is not defined as a class as we did it before but instead I use
sequelize with the lowercase s, so my database connection pool which is more
than a connection pool, it's actually a fully configured sequelize environment
which does also have the connection pool but also all the features of the
sequelize package and there we can define a new model by calling define. 

The first name that is the model name and by the way, here in the suggestion you
also see an example and so on as you do in the official docs of course. 

Now the model name typically is a lowercase name and I'll name it product like
this, you are free to name this however you want but to follow along smoothly, I
recommend taking this name. 

The second argument defines the structure of our model and therefore also of the
automatically created database table. 

This will be a javascript object and in there, we simply define the attributes
or fields our product should have, for example I want to have an ID. 

Now an ID is then in turn defined with an object where I configured this
attribute, there for example we set the type and the type is now one of the
types defined by the sequelize package. 

So now I use sequelize with a capital S, so from this import here and there you
find a bunch of types like number or string, so not var, char and so on but here
you have the more javascript-ish names I could, would say and I want to use an
integer here because my ID will be a number starting at 1 and then incrementing.


To make it increment, I also configured this attribute to be auto-incrementing
by setting auto-increment to true and in case you're wondering how I do know all
of that, well again you find that in the official docs. 

On docs.sequelizejs.com, you can dive into sequelize, learn more about how it
works and how you can configure it and under model definition, you learn all
about how to define a model, how you can define your different tags for the
model and you also see a list of all the supported data types, like the integer
we just used. 

So this is where you can learn more about this and I can tell you that I want
this to be auto-incrementing so I will set auto-increment to null, to true. 

I also don't want to allow this value to be empty, so I will allow null to false
because I don't want to allow null values in there. 

Last but not least, I'll set primary key to true to basically define this as the
primary key of the table which is an important concept in SQL databases for
retrieving the data and then also for later defining relations. 

With that defined, a product of course also has other fields, for example a
title. 

Now we can again define a javascript object to configure it in detail or if you
just want to set the type, you can also use sequelize and then the type, so this
is a shortcut in case you only want to set the type, though you could argue that
we also at least want to set that this should never be null but here as a demo,
I will just assign the type. 

For the price I'll go back to the javascript object and set the type to
sequelize and then double and I will again set allow null to false to not allow
null values here. 

Then I will set my image url here again to a javascript object where I set the
type to sequelize string and I will set allow null to false to not allow null
values here. 

And last but not least, I also want to have a description which also will have a
type that is of type sequelize string and I will set allow null to false. 

Now this is my product model, last but not least we need to export it. 

So below my model definition here,I'll simply use module exports and export my
product here, so this constant in which I define, store the defined model, this
gets exported here. 

And with that, we made a huge step forward and we can now start using this
product. 

Now let's see how we use it over the next lectures. 

---