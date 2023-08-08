## 423. Defining a Mutation Schema

<strong><em>no description</em></strong>

We edit our first graphql query which allowed us to get data, let's now add a
query that allows us to save data. 

And for that, why don't we start with our frontend which we used and make sure
that we can actually sign up users so that we can create users because that
sounds like a mutation to me. 

For that, first of all let me clean up my frontend. 

I'm not using socket.io error there anymore, so in the feed.js file, at the top
remove that open socket import and then let's remove that logic from
componentDidMount where I created my socket connection and let's also remove add
post and update post, I'll do that differently later. 

After changing this, let's go to app.js which is where we do sign up and we want
to make sure that for the sign up handler, we now reach one of our mutations and
for that, we first of all need to create it. 

Now how do we create a mutation? 

I'll get rid of this resolver, we'll later add query resolvers again, for now I
will get rid of my query here, for now I only need a mutation and we add that in
our schema by adding mutation here and then just as with the query, we define a
type which you could name mutation or root mutation, whatever you want and there
you now define the different mutations you want to allow, so here I'll just
point at the root mutation. 

And in the root mutation, I'll add one which I'll name create user. 

You could name it sign up, you can name it whatever you want. 

Now that mutation here will actually require some input, some arguments and that
is a different syntax which you now haven't seen before, you can add parentheses
after your query name and this allows you to specify arguments that have to be
given to that resolver that will run in the end. 

And here we could define that we need some user input data and now we need to
define the type of that data, so how does this data look like? 

Well first of all, we could of course accept the title of type string and then
another argument which is, not the title, the email of type string and then
another argument which is the password of type string, that would work too or we
bundle it in one object which we expect and for that object, we can create a new
type and we don't do this with the type keyword but there is a special keyword
for data that is used as an input, so for data that is used as an argument and
that is the input keyword and you can now name this however you want, I'll name
it user data and there, how does my user data look like or my let's name it user
input data maybe, how does that look like? 

Well that will be an object which has an email field which is a string that is
required, I need that to be a string and I need that field to be there, I also
will get a name which is a string and a password. 

Now this is the data type I'll use here for my argument, create user and now the
question just is what do I get back after a user was created? 

Well there I want to get back a user object. 

So for that I'll define a new type, not an input but a normal type which I'll
name user. 

There I'll have an _id field which will be an ID type, it's a special type
provided by graphql which simply signals that this is unique and well, treated
as an ID. 

I'll then also have the username which is a string, I'll have the email which is
a string, I have the password which is a string which I don't require let's say
because I don't necessarily need to return that, I'll have a status which is a
string and I'll have my posts, now that will be an array and for that I also
need to define how my posts should look like, so let me define another type
here, the post type and that will have an ID, that will then also have a title
of course, a post will also have a content, a post will then also have an image
url and of course you might notice some similarities to my mongoose models. 

There I also defined how the data will look like and how it is connected, we're
essentially doing the same here because this will allow us to then retrieve that
data efficiently. 

So now I have my post image url, we also will have a creator which is a user
object and we'll have the createdAt field. 

Now graphql does not know dates so I'll use a string here and the same for
updatedAt. 

Remember we'll get these two fields because in the mongoose model for the post,
we enabled timestamps. 

Ok, so that is the post model. 

We needed that because in the user type, we now will have an array of posts and
this is how you tell graphql that you have an array of something, you enclose it
in square brackets and that user data is now what I want to return here when I
create a user. 

That is the schema defined, let's now work on the resolver for that. 

---