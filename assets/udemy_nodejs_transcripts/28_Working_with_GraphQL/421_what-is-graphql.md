## 421. What is GraphQL?

<strong><em>no description</em></strong>

Now what is graphql? 

To really explain it, let's compare it to a rest API which we already learned
about. 

A rest API is a stateless client independent API for exchanging data, so it's a
node express application or a node with any framework application of course that
we build to exchange data. 

We don't render views, we don't store sessions, we don't care about the client,
we only get requests, parse the data and return responses with data, typically
json data. 

A Graphql API is generally not that different, it's also a stateless client
independent API for exchanging data but and that's the important part of course,
with higher query flexibility and to understand that, let's look at some rest
API limitations. 

Let's say in our rest API, we have an endpoint that looks like that, we can send
a get request to /post and as you might imagine this would fetch us a post,
let's say from the database but could also be from a file or anything like that
of course and this is how a post might look like. 

Now we returned that to the client and everyone is happy but what if we actually
only need the title and ID on the client? 

What if we don't need the content or we don't need the creator data? 

We can of course have many scenarios where we use one and the same endpoint in
our frontend application, so in our single page application or our mobile
application and in one place, on one page, we might need title and content, on
the other page, we might need content and creator. 

How can we solve that? 

Well solution one is of course to simply create more endpoints that return the
different types of data. 

We can create a new rest API endpoint, for example sending a get request to
post-slim to only return title and ID. 

Now obviously by the way, you could also of course use the same endpoint all the
time and just parse or filter out the data you need on the frontend but then you
sending a lot of unnecessary data over the wire which is an issue, especially
when working with mobile devices. 

So our solution could be to simply create more endpoints that simply return the
data you need for each of these endpoints. 

The problem is you'll have a lot of endpoints and you'll have to update them
continuously and you also have a very unflexible solution here. 

If your frontend engineers and in bigger projects you typically work in
different teams, if they need more data on a new page, they come to you as a
backend developer and ask you to give them an endpoint that returns that data
and they're stuck in their frontend development until you edit this. 

So fast iteration on the frontend is made harder and on the other hand, you on
the backend continuously have to add new endpoints to cater for the needs of
your frontend engineers. 

So this is not really ideal, solution two could be to use query parameters. 

On your existing endpoints, you could accept query parameters like data equals
slim. 

Now obviously that is an option but just as with the first solution, you always
have to add it so that your frontend engineers can continue and you have this
dependency between frontend and backend. 

Additionally your API might become pretty hard to understand because it might
not be clear which query parameters can I set, which values can I set on these
query parameters, so this is also not ideal. 

Ideal for apps where you often have different data requirements on different
pages is to use graphql. 

There you don't have the problems I described before because there as you will
learn, you have a rich query language that you use in your frontend to send it
to the backend which is then parsed on the backend and dynamically retrieves
just the data you need, so it's almost like a database query language which you
use on the backend like SQL or mongodb query language, almost like something
like this for the frontend, so which you put into the request you send to the
backend. 

Now that is the idea but how does graphql work then? 

Well we get our client, we got our server and on the server, you generally have
your logic for interacting with the database, with files, anything like that. 

Now what do you send from client to server? 

In a graphql world, you only send one kind of request and that is a post request
to graphql, /graphql. 

So you only have one single endpoint where you send your http requests to, even
for getting data and why is that? 

Well for a post request, you can add a request body and that request body will
contain the query expression, graphql defines its own query language and I will
show you where to learn more throughout this module of course and you use that
query language, you put it into a request body and you just can't send request
bodies on get requests for example, so you put your query language expression
into that request body and that will be parsed on the server to then do some
magic on it and return you just the data you want. 

That is the idea behind graphql. 

Now such a graphql would typically look something like this, it's a json
object-like structure where you have an operation type, query would be for
getting data, you also have other types like mutation for editing or deleting or
inserting data or subscriptions for setting up real time data subscriptions
using web sockets. 

You also have the endpoints you could call them or the commands you can execute
and you define them as a developer on your backend, the available endpoints and
then the fields you want to extract and that is the flexible part because you
could in one place get the user with just a name and in another place, you could
get name, age and email, so that is exactly what you put into your query which
you send to your backend which is then parsed there. 

Now regarding these three operation types, as I mentioned we got a query, there
we retrieve data and we use a post request for that but if we want to compare it
to the rest API world, then this would be your equivalent to sending a get
request to some path there. 

We also got mutations which basically are used for everything that changes data,
so what you previously handled with post, put, patch and delete requests and
subscriptions as I mentioned set up real time connections via web sockets, we'll
not focus on that in this module because this is no graphql course and indeed
you can create whole courses on graphql, here I want to focus on the core
features. 

So to sum it up, in a big picture, we have our client, we send a request to that
single graphql endpoint on our server and then there and this is the part you
will do with me in this module, there you set up your definitions for queries,
mutations and possibly also subscriptions. 

In these definitions, you use type definitions because graphql uses a typed
query language which means you define the types of data you work with, the types
of data you return in a query and so on and these endpoints you define here, so
these queries and mutations and subscriptions you define, these are connected to
so-called resolvers which are functions that contain your server side logic. 

And if you compare that to a rest API, the definitions would be your routes and
the resolvers would be your controllers and that is how you can look at graphql
and this is how we will implement it. 

So to sum it up, it's a normal node and possibly express server, of course you
are also not limited to using expressjs, you're also not limited to using node
by the way, the graphql language approach can be used with any programming
language just as rest APIs could but this is a node course of course so we'll
focus on that. 

You have one single endpoint, typically /graphql though you could change this of
course. 

You only use post requests because you put that query expression into the
request body and you have resolvers on the server side that analyze that request
body and then do something with your data based on the query expression you had
in that body and we'll use third party packages for that parsing and so on. 

So posting for getting data, that is the most confusing thing you typically have
when diving into graphql, yes this is what we do, this is what is ok here
because we describe that data we want to get in the request body. 

Now that was a lot of theory, let's see it in action. 

---