## 138. Comparing SQL and NoSQL

<strong><em>no description</em></strong>

So we learn about SQL and NoSQL, let's now compare them and let's start with
horizontal and vertical scaling because as I mentioned at the end of the last
lecture, we often need to scale our database to keep up with our growing
application with more and more users. 

Horizontal and vertical scaling are the two approaches we can use to scale our
database. 

Now what do they mean? 

Well in horizontal scaling, we simply add more servers. 

and the advantage here of course is that we can do this infinitely. 

We can always buy new servers, be that on a cloud provider or in our own data
center and connect them to our database and split our data across all these
servers, of course this means that we also need some process that runs queries
on all of them and merges them together intelligently, so this is generally
something which is not that easy to do but this is of course a good way of
scaling. 

Vertical scaling simply means that we make our existing server stronger by
adding more CPU or memory or with something like that, especially with cloud
providers, this is typically very easy, you simply choose another option from
the dropdown, you pay more and you're done, the problem here is that you have
some limit, you can't fit infinitely much CPU power into a single machine. 

So these are the two ways we can scale, how let's compare a SQL and NoSQL
regarding that and in general. 

Now in general in SQL we use schemas, we also have relations, these are two core
characteristics and data is typically distributed across many many tables which
are then connected through relations. 

Now regarding the scaling, it's important that horizontal scaling often is very
difficult or even impossible due to the way SQL works, you can of course add
more servers but running them all on one shared data cloud so to say, one shared
database is pretty difficult. 

Vertical scaling is easily possible, you can simply make your server stronger
but adding more servers can be very hard or even impossible, so definitely not
trivial. 

So this is a problem possibly if we have multiple or thousands of read and write
queries per second, then maybe our SQL database especially if we do very complex
joins between related tables can reach limits or can not be the best choice. 

NoSQL is schemaless and has only a few relations if at all, the data is
typically not distributed across multiple collections but instead we work with
merged or nested documents in an existing document, though we of course also
have a couple of collections for the different features of our application
typically. 

With NoSQL, horizontal scaling is easier, still something where you have to know
what you do but there are cloud providers which do that for us so we don't have
to know the ins and outs of that and in general, due to the way it works with
less connections and so on, this is possible. 

And therefore we also get great performance for mass read and write requests and
NoSQL can be very performant in an application with high throughput. 

Now this makes SQL look very bad but the full truth is that it always depends on
the kind of data you are storing, if you are storing where the relations are
really important and where you want to have a split up across tables and where
you want to have strong schemas, SQL can be perfect, also not every part of your
data is accessed multiple times per second. 

You can have parts of your application where you manage general data, let's say
user data which does not change that often and therefore, SQL might be very good
there. 

Other parts of the application, let's say orders or shopping carts that do
change frequently could be stored with NoSQL and there, the relations might also
not be that important because you can always put all the information that
belongs to a shopping cart or to an order in one single document and even if you
do for example store some user data there, you might not need to touch that
document just because the user change his photo because you probably didn't
store that along with the order anyways. 

Now in this course, we will build both, we will use both because I want to teach
you both and it's not so much about this course application but you should know
how to use SQL with nodejs because maybe you need to add in your application or
you're working on a project where you don't decide which database to use but you
simply have to use it. 

So we will use SQL first but then I will also show you how to use NoSQL of
mongodb, so we'll basically implement the course project or the current state of
the course project with both databases and you will see how to interact with
both of them. 

And let's start with SQL in this module, let's install a MySQL database and
learn how to interact with it from inside our nodejs code. 

---