## 137. NoSQL Introduction

<strong><em>no description</em></strong>

We had a look at SQL based databases, now it's time to have a look at
NoSQL-based databases. 

Now the name NoSQL simply means that it doesn't follow the approach SQL follows,
it also uses a different query language but instead of having schemas and
relations, NoSQL has other focuses or other strengths. 

So in NoSQL we can still have a database and we can give this database a name,
shop let's say. 

Now that's the same for SQL by the way, there we also have databases. 

Now in SQL, we then had tables, users and orders and maybe also products, these
are just examples here. 

Now in NoSQL, tables are called collections but you can think of them as tables,
so as the table equivalent but we call them collections in the NoSQL world. 

Now in a collection, we don't find records but so-called documents which look
like this and since we're working with javascript in this course here, we of
course can kind of see that this looks a bit like a javascript object, so
documents are very close to how we describe data in Javascript you could say. 

Now that are the documents in our collections and what you can already see here
in the users collections example is that NoSQL doesn't have a strict schema. 

Here we got two documents in the same collection but the second document, Manuel
here does not have an age and that is perfectly fine in NoSQL, you can store
multiple documents with different structures in the same collection. 

Now often you of course still try to have kind of a similar structure but it's
also not uncommon for some applications that you don't always have exactly the
same fields available for the data you are storing in the database and that is
ok in NoSQL, you can definitely store documents which are generally equal but
where some fields might differ. 

One other thing is that in the NoSQL world, we got no real relations, instead we
go for duplicate data. 

Now that simply means that if we have an orders collection here, we have a
nested document, the user which also is stored as a separate document with more
details maybe in the users collection and we don't connect that through some ID
or behind the scenes setup relation, instead we simply duplicate data, to be
precise the data we need in the orders collection here. 

That of course means that if that data changes, we have to update it in multiple
places, if all these places need the latest update or the latest data change but
that can be OK because this on the other hand gives us the huge advantage that
if we ever retrieve data, we don't have to join multiple tables together which
can lead to very long and difficult code and which can also impact performance,
instead we can simply read the data from the orders collection and we probably
got all the data we need to display on the orders page without having to reach
out to other collections and therefore this can be done in a super fast way and
that is one of the huge advantages of NoSQL, it can be very fast and efficient. 

So NoSQL characteristics in general are that we have no strong data schema, we
can have mixed data in the same collection, no structure is required and that we
have generally no data relations. 

Now we can relate documents in some way and this is possible and we will see how
to work with connected data in the NoSQL module of this course but generally we
have no or only a few connections and instead try to copy data and have a
collection with documents that work on their own. 

This is the difference, we also got a difference between SQL and NoSQL regarding
our scalability. 

So as our application grows and we need to store more add more data and access
that data or work with it more frequently, we might need to scale our database
servers and we can differentiate between horizontal and vertical scaling. 

We'll have a look at this and in general how the two worlds, SQL and NoSQL
compare in the next lecture. 

---