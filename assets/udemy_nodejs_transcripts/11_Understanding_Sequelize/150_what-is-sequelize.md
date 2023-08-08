## 150. What is Sequelize?

<strong><em>no description</em></strong>

Now before we start using it, what is sequelize actually? 

Sequelize is a third party package, to be precise it's an object relational
mapping library and this is a pretty long name which simply means it does all
the heavy lifting, all the SQL code behind the scenes for us and maps it into
javascript objects with convenience methods which we can call to execute that
behind the scenes SQL code so that we never have to write SQL code on our own. 

It works like this, we got our object let's say a user with a name, age, email
and password but of course this can be anything, could be a product, whatever
you need and this is mapped to a database table by sequelize, so it
automatically creates that table for us even, it automatically sets up relations
and tables even for us, it does all that and when we create a new user for
example, we simply call a method on that user javascript object and sequelize
executes the SQL query or the SQL command that is required. 

So instead of writing this on our own, we simply create a javascript object and
work with that and here would be one example using sequelize to create a new
user which would behind the scenes execute the SQL code we don't have to write. 

Sequelize offers us the models to work with our database as I showed you on the
last slide and it allows us to define such models, so basically define which
data makes up a model and therefore which data will be saved in the database. 

We can then instantiate these models, so these classes so to say, we can execute
the constructor functions or use utility methods to create let's say a new user
object based on that model so we have a connection here and we can then run
queries on that. 

That could be that we save a new user but it could also be that we find all
users as an example and here again, this always relates back to our model which
we define with sequelize. 

And we can also associate our models, for example we could associate our user
model to a product model. 

So this is what sequelize does but of course we dont just want to learn that in
theory, we want to see that in practice. 

So let's add sequelize to our project and let's slowly integrate it to manage
our products in our cart and so on through sequelize. 

---