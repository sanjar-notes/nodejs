## 424. Adding a Mutation Resolver & GraphiQL

<strong><em>no description</em></strong>

We have the create user schema, let's now work on a resolver that allows us to
create a user and for that in the resolvers file, I'll add create user like that
and now here I actually get some arguments, you also do so in queries where you
get data by the way, there you could also get arguments for example when you
want to retrieve a specific post with a specific ID. 

Here my arguments are no post ID though but the user input data. 

My first argument there will be an args object, there is a second argument
available which is the request by the way, this will become important later. 

Now on the incoming args object, I can retrieve all the data I defined in my
schema, so email, name and password, that is my argument data so that is what I
can retrieve from the args object. 

Not directly on the args though, instead args will have a user input field
because args actually will be an object containing all the arguments passed to
that function, here it's only one but it could be more, so args will have a user
input field and in there, I will have email, name and password. 

So I can retrieve them, I can for example retrieve my email by typing args user
input because in my schema, I name this field here user input and on the user
input, I can get the email, so .email like this. 

This is one option, we can also use destructuring to get user input out of my
args object and then the email will just be user input email, so a bit shorter. 

Now we'll use this in a second, first of all let's import the mongoose user
model because I'll still interact with the database of course. 

So I will require models user and then in here, I want to use the async await
syntax, to use that I need to change the way I write this method. 

I add a colon after create user and use the function keyword and now I can add
async in front of that. 

So now I can use async await, that is purely optional though, you could also use
the normal then catch approach with your promises. 

Now in there, first of all I want to find out if that user already exists and
for that, I'll get an existing user by awaiting for user find one where the
email in the database matches the email entered in the user input. 

Now one super important note, if you're not using async await, you need to
return your find one query which you're executing here where you then add then
because if you don't return your promise in the resolver, graphql will not wait
for it to resolve. 

When using async await, it's automatically returned for you, we don't see the
return statement here but it is there, so that is super important. 

So now I'm getting my existing user and if I have an existing user, well then I
know I don't want to create a new one. 

So in this case, I will create a new error with a message of user exists already
and I will throw that error and I will come back to error handling and graphql
in a later lecture. 

If I do have no existing user with that email address, then I can continue with
storing it and the logic for that is similar to the one in my auth controller,
we need bcrypt to hash the password. 

So in my resolver function here, let me import bcrypt at the top and then there,
we can use the hash method to hash the user input password with 12 salting
rounds. 

Now again I'll use async await here, so I'll get my hashed password eventually
after awaiting for this to finish. 

Now after I got that, I can create a new user object and in that user object, I
will pass the email which is user input email, I'll pass the name which is user
input name, I'll also pass the password which is my hashed password. 

Now I need to save that to the database and I do care about the created user, so
I'll store that, stored all that created user in a constant by awaiting for a
user save and that will just return that user object I created. 

Now here finally I need to return some data and we see which data in our schema,
we need to return a user object. 

For that here, I will return my created user_doc field which contains just the
user data without all the metadata mongoose would add otherwise and I will
override the _id field by adding it as a separate property and therefore it will
override the one I'm pulling out of _doc because I need to convert it from an
object id field to a string field otherwise it will fail, so here I will access
created user _id and then call toString. 

This is now the user object I'm returning when I'm creating a user. 

Now one important note before we actually try that in our frontend application. 

We can of course try that from inside postman but there is an even more
convenient solution for testing this. 

Before I show you the solution, let me first of all clean my database though so
that we start from scratch and before that, I'll delete both my posts and my
users collection here. 

It will be created on the fly again once I got data to enter and I simply want
to remove all entries I have thus far. 

So now with the clean database, let me show you that simpler approach I'm
referring to. 

To test this mutation, I can go back to app.js on the backend code and there
where I register or setup my graphql endpoint, besides setting the schema and
root value, you can also set graphiql, written graphiql to true. 

This gives you a special tool and this is the reason why I'm not listening for
post requests only here because now with your running server, try visiting
localhost8080/graphql and this will send a get request, if you enter something
in the browser here here, you sent a get request and you will get this screen
which allows you to play around with your graphql API. 

Now if you go back to your backend, to the schema, quickly add a query again to
your schema here, root query and let's create that type here real quick and in
there, just add that hello again like this. 

We don't need a resolver for that, we just need that query. 

Now if you reload your graphiql interface, you actually have that documentation
on the right here where you see the operations you can do but you need to have a
query defined for that, even if it leads into the void and there you can click
onto it to see which mutations you have, which data you need to send and so on
and you can not just explore that here, you can even send your data. 

So in here, you can now create a new mutation about typing mu and you will even
get autocompletion, then curly braces and now with control space, you even get
suggestions, if you have more than one object, it will not be filled in
automatically but you'll get a dropdown instead, you get suggestions for what
you can run and here you now see this needs a user input then a colon and then
an object that contains the user input data and there you see we need an email
wrapped in double quotation marks, test@test.com, we let's say need a name, that
could be max and we need the password and that is tester and thereafter we add a
pair of curly braces and now we can define the data we want to return after this
query is done. 

With control space we get some suggestions, like the ID that was generated or
the email. 

And now you can run this query by pressing that play button up there or hitting
control enter, you also see the commands here and this will now execute it and
it seemed to have succeeded. 

You see the ID of the created user and the email and if you go back to mongodb
compass and you refresh that here, you should have the users collection back and
you see the user in there with the hashed password. 

So this is a great tool for playing around, better than postman because you got
this nice interactive support with the auto-completion, you've got the
documentation here and you can test your graphql query in this tool in a really
nice way. 

And now with that, let's see how we can enhance this for example by adding
validation before we then also connect our frontend application of course. 

---