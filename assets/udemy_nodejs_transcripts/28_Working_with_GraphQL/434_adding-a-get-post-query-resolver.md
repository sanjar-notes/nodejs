## 434. Adding a "Get Post" Query & Resolver

<strong><em>no description</em></strong>

Let's make sure we can now also get all posts and for that I'll start on the
backend in my schema again. 

Getting that of course is a normal query, so next to login I'll add a query and
I'll name it posts, you can name it however you want. 

I don't need any arguments here, I instead can directly define my return type
and that will actually not be that array of posts as you might have expected but
actually I'll create a new type for that because remember that in the rest API,
we also did not just return an array of posts but for pagination, also a number
that specified our total amount of posts in the database. 

So I will create a new type and I'll name it post data which now has a posts key
and that will be my array of posts and I'll also have a total posts field here
which will be an integer. 

Now post data is what my query here should return and now we need a resolver for
that. 

So let's head over to resolvers and there I'll add posts, I'll write this as an
async function like this, I will actually not care about the first argument for
now,  my args but I will need the request to find out whether the user is
authenticated. 

That is actually the first thing I'll check and I'll copy the check from create
post, this if statement here and I'll add it here. 

Now if the request is not authenticated, if the user is not authenticated, I'll
throw an error, otherwise I'll later add some pagination logic but for now I
want to find the total number of posts and then all posts. 

So total posts can be found by awaiting post find, this gives me all posts and
then count documents. 

The posts themselves can be found by using await on post find like this and
again later I will also add skip and limit, for now I'll only add sort and I
will sort by createdAt in descending order, I will also populate my creator to
fetch the full user data with the name and so on because I'll need all that on
the frontend. 

So here I get my posts, now we can already return some data. 

I'll return an object and that object has to look like I defined it in my
schema, so it has to be an object with a post key and a total posts key. 

So in that object, I'll add posts and that will be the posts I've fetched here
and total posts which will be total posts. 

Now posts will not be returned like this because in there would be fields like
_id or createdAt which hold data formats that are not understood by graphql, so
instead I will add map here and you learned about map for example in the
javascript refresher which allows me to transform every element in that array. 

So here I will return a new object for every post which will generally be the
same, so I will pull out the existing elements on the posts document but then I
will override the ID with p_id toString to return a string and for createdAt . 

I will use p createdAt to ISO string and the same for updatedAt where I will use
p updatedAt to ISO string and this is now how I will transform my posts, every
single post in the posts array and therefore, the overall array. 

This is the backend, this is the schema and the resolver setup for getting
posts, now let's test this on graphiql here. 

Let me reload that page and there I will run a new query which will be called
posts and let's say there I'm interested in both the posts and total posts. 

Posts is an array of complex objects, so there I also need to specify what I
want to get out of there, let's say I'm interested in the ID, the title and the
content. 

And now I hit control enter and I get not authenticated which is correct because
I am not sending a token here. 

So that is the next step, we'll send these requests from the frontend, add our
token and then of course also render our posts. 

---