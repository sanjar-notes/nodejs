## 177. What is MongoDB?

<strong><em>no description</em></strong>

So what is mongodb? 

Now let me first of all tell you that I do actually have a complete course for
developers on mongodb, so you might want to check that out if you want to learn
way more about mongodb than I'll be able to cover in this course but now with
that let me start with a brief introduction to mongodb at least, what is it? 

Mongodb is both the name of the company which developed mongodb but also then of
their most famous product, a database solution, a database engine you could say,
a tool you can use to run very efficient NoSQL databases. 

The name stems from the word humongous because mongodb was built for one major
purpose, that you could store and work and that really is important, the work
part, that you could store and work with lots and lots of data. 

So mongodb is built for large scale applications, mongodb is built to quickly
query data, store data, interact with data, so it's really fast and it's really
awesome database philosophy that is behind NoSQL databases and therefore also
behind mongodb. 

Now how does it work? 

Well just like in the SQL world, we spin up a mongodb server and there we can
have multiple databases, for example a shop database. 

Now in such a database in the SQL world, we would have multiple tables, in the
NoSQL mongodb world we have multiple collections like the users and orders
collection for example. 

Now inside of each collection, we don't have so-called records but we have a
couple of documents. 

Now documents also look different than records did and it's not just about
different names being used, the core philosophy behind the database really is a
totally different one. 

For example mongodb is schemaless, inside of one collection, your documents
which is your data, your entry so to say don't have to have the same structure. 

In SQL that was totally different, we had a users table there and in that users
table, we had an ID, a name, an email, a password. 

Now here that is different, here we can have any kind of data in one and the
same collection. 

Often you will still end up with an at least similar structure but you're not
forced to have exactly the same structure and this gives you more flexibility,
also for your application to grow and to change its data requirements over time
without that being difficult to depict in your database world. 

So this is one thing, a document in mongodb looks like this and this looks a lot
like javascript object notation and to be precise it kind of is. 

Mongodb uses json to store data in collections, so every document you store
looks something like this, it follows the javascript object notation format. 

To be very precise mongodb uses something which is called bson for binary json
but that only means that mongodb kind of transforms this behind the scenes
before storing it in the files but you don't have to worry about that, you will
basically use it as json. 

Now such a json document is basically the same as a javascript object you could
say and there as you see, we can have nested or as mongodb calls them, embedded
documents, for example the address here would hold an embedded document. 

And you can also have arrays inside of that document and that array can like in
this case hold other documents, other objects or it could also just hold
strings, numbers, anything of that kind. 

So again for the data, you have great flexibility and the existence of these
nested documents also means that relations are managed a bit differently in the
NoSQL mongodb world. 

So let me come back to that in the next lecture. 

---