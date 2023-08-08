## 140. Connecting our App to the SQL Database

<strong><em>no description</em></strong>

To use SQL or to interact with SQL from inside node, we need to install a new
package and we do that with npm install of course. 

Npm install and let me simply bring that up to make it easier to read and npm
install --save because it will be a production dependency, one which is a
crucial part of our application and the name is MySQL 2, this is simply a later
version of well MySQL one as you might guess and it allows us to write SQL code
and execute SQL code in node and interact with a database. 

Now with that installed, we made one important step forward towards using MySQL.


The next step is that we need to connect to our database from inside our
application and for that, I will close my views here and go to the util folder
we created in the past, there we have that path.js file in there which we don't
really use anymore but we can also create a new file in here, the database.js
file and the name is totally up to you by the way. 

In there, I want to set up the code that will allow us to connect to the SQL
database and then also give us back a connection object so to say which allows
us to run queries. 

For this I'll first of all import that MySQL package and store it in a MySQL
constant, so require MySQL 2 is the command I need here and now there are two
ways of connecting with a SQL database. 

One is that we set up one connection which we can then use to run queries and we
should always close the connection once we're done with a query and the downside
is that we need to re-execute the code to create the connection for every new
query and there will be a lot of queries because we fetch data, we write data,
we delete data, creating new connections all the time quickly becomes very
inefficient both in our code and also regarding the connection to the database
which is established and the performance this may cost. 

So a better way is to create a so-called connection pool and by the way, you can
learn way more about this package, its options regarding how to set up
connections and so on in the official docs for this tool, for this package and
you find a link to those docs in the last lecture of this module. 

So to set up such a pool, I'll create a new constant pool, the name is up to you
and I'll use that MySQL object and there I will call create pool and there you
also see that create connection we could use. 

Now I don't want a single connection but a pool of connections which will allow
us to always reach out to it whenever we have a query to run and then we get a
new connection from that pool which manages multiple connections so that we can
run multiple queries simultaneously because each query needs its own connection
and once the query is done, the connection will be handed back into the pool and
it's available again for a new query and the pool can then be finished when our
application shuts down. 

So I will call create pool here and I need to pass in a javascript object with
some information about our database engine, our database host we're connecting
to. 

For that I'll first of all define the host, so the server IP address or name and
that is localhost because it's running on our local machine here. 

Then I need to define the username and that by default is root that was given to
us during the configuration process, I also need to define the exact database
name because this gives us access to a database server but that server typically
has multiple databases and here our databases are our schemas, so we'll take the
node complete database here so that the value here simply is node complete. 

Now with that, we simply have to enter one more piece of information and that is
of course our password. 

So here enter a password and then I used this password, you should of course use
the password you assigned during installation. 

This will create a pool and now I can export this pool and I will export it in a
special way actually, I will call promise here because this will allow us to use
promises when working with these connections which of course handle asynchronous
tasks, asynchronous data instead of callbacks because promises allow us to write
code in a bit more structured way, we don't have many nested callbacks, instead
we can use promise chains and you will see what I mean in this module of course.


So now we can always import from the database.js file to get access to that pool
and to the connections in there and I can show this as an example by simply
going to app.js which will of course run when our application starts up and
there let's simply import database, maybe store it in a constant named db by
requiring util database, like this, so reaching out to that new database file we
just created. 

This will then be the pool basically or well the pool which allows us to use a
connection in it and if I now use this let's say here, I can run db and now we
got a couple of methods, one of them is execute which allows us to execute
queries, we also got query but execute is a bit safer so we'll use that. 

We can also end it and we want to end it whenever our application is to shut
down but we don't shut our application down in this case here so no need to call
end here, instead we just want to connect or execute a command. 

And we can execute a command here by writing SQL syntax as a string. 

Now of course that means you need to know SQL and I will teach you a very basic
SQL here in this course. 

If you plan on using MySQL together with your node app, you definitely have to
take a SQL course which dive into all the depths of the SQL language because
that is far beyond the scope of this course which is of course a node course and
not a SQL course but what we could do here is we could select everything from
products and of course we have no products table yet, so let's quickly go back
to our workbench and here on tables, right click and click create table and this
gives you now the table editor. 

The name should now be products and in there, you can add new fields, remeber
that schema thing, you add fields. 

So let's work on this and finish this and execute our first little code in the
next lecture. 

---