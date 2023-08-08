## 422. Understanding the Setup & Writing our First Query

<strong><em>no description</em></strong>

To see it in action, I'm back in our rest API project we created earlier where
we previously added socket.io . 

and first of all, I'll get rid of that socket.io part, I'll remove it, I'll
remove the socket in js file, in app.js I will also remove my routes because we
will have no more routes, we'll not set up routes anymor, we'll use graphql
endpoints instead. 

I'll leave the rest as it is for now, remove that code where I use my routes and
then here I will not store the server because I will not setup any socket.io
connection and we can also now remove the routes folder because we'll not use
that anymore. 

So now I clean that up a little bit and now I want to use graphql and for that
I'll install two new packages. 

The first one is called just graphql, this will be required for defining the
schema of our graphql service, so basically the definition of the queries and
mutations and so on we want to allow and I will also add express graphql to
install a simple server that will do the parsing of incoming requests and so on.


Now if you want to learn more about graphql, check out graphql.org, it's a great
resource with a lot of documentation on graphql and its query language which by
the way is clearly defined and we need a strong ruleset to know how we write
queries and there if you click on code, you also find libraries for all kinds of
languages and if you choose javascript, you'll find the graphql package we just
installed which allows us to define such a schema as I mentioned. 

You'll find the express graphql and you also find other solutions for other
frameworks, Apollo for example is super popular and works with any node
framework, it offers more than the barebone setup express graphql gives us
though and I want to show you a very raw approach in this module so that you
understand all the behind the scenes things, Apollo would hide some of these
things, so I will instead use express graphql. 

Now with that out of the way, we installed that, we cleaned up our project, now
let's add some graphql logic and how do we do that? 

First of all I'll create a new folder named graphql where I will put my graphql
related code and there, I'll add my schema.js file where I define the queries,
mutations and types I work with in my graphql service I'll create and I'll add a
resolvers.js file where I will define the logic that is then executed for
incoming queries. 

Now in schema.js, let's start with that, there I'll first of all import
something from that graphql package I installed, not from express graphql but
just graphql and that something I import is the build schema function which
allows me to build a schema which can then be parsed by graphql and by express
graphql. 

I will export this schema so I'll use module exports and then I will call the
build schema function and I will return that schema object this will generate
for me and now here we pass a string where we describe our schema. 

Use double backticks here, so not single quotation marks but backticks to create
a string literal, a template literal because there you can simply write
multiline strings. 

And now to define a graphql schema in this string, we type schema and add curly
braces, please note that there is no colon after schema and in that schema we
now define a query field and this now will be an object with all the queries and
queries are the parts where you get data, so all the queries you want to allow. 

To make that easier to read, I'll now add a separate type for that with the type
keyword which I'll name query, you could name this differently, you name this
root query, however you want. 

Now in there, you will have all the different queries you can make in the end,
for example you can add one that is named hello, simply a basic dummy query
here, hello which let's say returns a string. 

This is how you define the return type for a query, you add a colon after the
query name and then the type and graphql knows a couple of types, strings,
integers, floats, booleans, IDs and you can learn all about that in the official
docs of course. 

So now this is my root query and this is the return type of my query here, this
is now a very basic schema where we can send a hello query to get back some
text. 

Now that some text now is the defined in the resolver, the resolver is an
exported object where we now need a hello function, a hello method, so you need
a method for every query or mutation you define in your schema and the name has
to match of course, I have a method named hello here because here I have a query
named hello. 

You don't need a resolver for this query because in your schema, you basically
setup your root query which is then made up of these sub-queries which now need
resolvers. 

So now we have a resolver for hello, that hello method and there we need to
return a string, right, we expect the string, you can by the way make this
string required by adding an exclamation mark. 

Now if you don't return a string, you'll get an error. 

So here I could return hello world like this, if I now save that I have a very
simple graphql service. 

Now before we test it, let's make it a little bit more complex, in my schema
I'll add a new type and I'll name that test data, the name is up to you and
there I'll have a text which is a string and I'll have a views property which is
like say an integer. 

Both are required, please note there is no comma after these fields, you simply
use new lines and now let's say my hello query should return that test data
instead of a boring string. 

Well then we can go back to the resolver and now we need to return an object in
there with a text field that should be a string, hello world and with a views
field which should be an integer. 

Now we have a valid resolver, we have a valid schema, now we need to expose it
to the public and that can be done with the express graphql package. 

In app.js, we now import that, so here I'll import graphql http, you can name
this however you want from express graphql and let's now scroll down all the way
to the error handling middleware and there let's add another middleware so that
all the other middlewares do apply and here I will apply this to /graphql and
you could change that but that is a common convention to use and I deliberately
don't limit this to post requests here and I will show you why in a second so
please make sure you use use here and then you use that graphql http method
which is provided by express graphql and you pass a javascript object to it to
configure it. 

Now this needs two items to work. 

The first is the schema and for that we need to import the schema which we
export in the schema.js file, so here I'll import graphql schema by requiring it
from graphql schema and I need to import my graphql resolver by importing it
from the resolvers file in the graphql folder. 

Now we can go down and use the graphql schema here as the schema and we also
need to set the root value which now points at our resolver, so this is now the
graphql resolver. 

With this setup, we can start our node server here and now let's try this out. 

You might remember that we have to send post requests right,

 

08:57.530 --> 09:01.850

so let's use postman for testing. 

There I'll send a request to localhost 8080/graphql and that should be a post
request. 

Now in the body of that request, we send some json data that describes our
query, so we set this to raw application json and here, you send data like this.


You send a javascript object with a query key and this does not mean that we
send a query and not mutation, it simply is something which the express graphql
package will look for. 

Inside of these curly braces, you now write the real query but actually here
this is a string and then the value here between double quotation marks is your
graphql query expression and there, you add curly braces and in-between, the
name of the query you want to target and if we have a look at our schema, we see
that we have a hello query. 

So we can target hello here and hello returns us test data which has text and
views. 

Now we need to define which data we want to get back for that query and
therefore after the name of the query, we add another pair of curly braces and
in-between, we list the properties, the fields we want to get back for that
query, we simply separate them with blanks. 

So here I could get my text for example but not the views. 

If I now hit send, indeed you should get hello world here and if you add a
whitespace and then views, you will get the views too and this shows you the
flexibility already. 

It's one and the same endpoint but we define which data we want to get on the
frontend and it's important to understand that we don't filter the data on the
frontend, it gets filtered on the server by express graphql in our case which
does the heavy lifting here and we simply define our schema and the resolver. 

In the resolver, we return all the data but then graphql on the server will
filter out just the data that was requested by the client. 

This is how graphql works in a nutshell, let's now see how we can add a
mutation. 

---