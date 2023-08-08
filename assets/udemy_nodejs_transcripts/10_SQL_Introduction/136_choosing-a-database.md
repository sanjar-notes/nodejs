## 136. Choosing a Database

<strong><em>no description</em></strong>

So SQL or NoSQL, that is the question and to answer that question, we first of
all have to understand the differences or what SQL and NoSQL databases are, how
they differ, how they differ regarding how we store the data and so on. 

Our goal always is to store data and make it easily available or accessible so
that we have an easy way of accessing our data and not just easy from a code
perspective but of course efficient, it should be fast. 

That is why we use a database, it's simply quicker than accessing a file
especially as the data in there grows, it also helps us with things like we
don't have to read the entire file to just find one piece of information. 

Now as I mentioned, we can opt for a SQL-based database, MySQL would be an
example database engine that you can use or a NoSQL database and there mongodb
is one of the most prominent and well known alternatives. 

So what is SQL, how does it work then? 

SQL database thinks in so-called tables, so we might have a users, a product and
let's say an orders table and in each table, you have so-called fields or
columns, for example a user could be defined by having an ID, an email, a name
and a product could have an ID, title, price and a description. 

Now we fill in data for these fields, so-called records, so basically the rows
in our tables. 

For example here we got a couple of users with their data and we get a couple of
products too. 

SQL based databases also have one important thing, they allow you to relate
different tables, for example an order could simply be described as a connection
of a user and a product right because a user might order a couple of different
products and a product might be ordered by a couple of different users. 

So basically we have such relations in SQL based databases, here we can see one
example relation. 

This is one of the core things about SQL and in general, the core SQL database
characteristics are that we have a strong data schema so that for each table, we
clearly define how the data in there should look like, so which fields do we
have, which type of data does each field store, is it a number, is it string, is
it a text, is it a boolean? 

So that we have this strongly or strictly defined schema and all data in the
table has to fit the schema for this table, this is really important, so this
schema, this definition of how the data has to look like is one core thing in a
SQL database. 

We also have relations between our data, that is another core characteristic of
SQL based database, we relate our different tables with basically three
important kinds of relations, one to one, one to many or many to many, this
simply means that we can have two tables where each record fits one other
record, a record might fit multiple other records or multiple records in table A
can fit multiple records in table B and you'll see this in practice and in the
code in this module. 

So tables are connected, that's another important thing. 

Now SQL simply stands for structured query language, so queries are a crucial
things, queries are simply commands we use to interact with the database. 

And in SQL, a query look something like this, of course there are different
commands, this would be a command that selects all users, so all entries, all
records in the users table where the age is greater than 28. 

So this is a so-called query, we've got a couple of keywords there which are
making up that SQL language, so the structured query language simply has these
keywords and then we insert some parameters or some data we connect with these
keywords, this is how SQL works. 

Now let's have a look at NoSQL in the next lecture then. 

---