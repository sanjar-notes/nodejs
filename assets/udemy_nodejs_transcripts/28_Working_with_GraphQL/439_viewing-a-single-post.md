## 439. Viewing a Single Post

<strong><em>no description</em></strong>

So let's make sure we can also fetch a single post and for that, I'll go to my
schema again because on the schema is where I will work and so here, I will add
a new query, post which will get an input, an ID of that single post I want to
fetch and will return a post in the end. 

This is how my query should look like in the schema definition. 

Now let's of course also add a resolver for this single post and for that, I'll
go to my resolvers.js file, add it down there, use the async function syntax
like this and in that function here, just as in the function up there, I'll get
arguments and the request object, with object destructuring I can get my post ID
or whatever you chose as a name here, so in my case just ID out of that request
arguments object. 

I get the request object as well and first of all, I can check whether the user
is authenticated. 

So I will copy this check and add this here and then as a next step, I will add
the logic to retrieve a single post and for that, I'll get my post by awaiting
post find by ID for the ID I get as an argument. 

Now I will also populate the creator here so that we have all the user data and
not just the ID and thereafter, I'll check if we did not find a post in which
case I'll create a new error, no post found and also set a code of 404 and throw
the error but if we make it after or past this if check, we know we have a post
and then I'll return an object where I get all the data from that post and then
again I overwrite the ID because I can't return object IDs, so post_id to string
and the same for createdAt because I can't return dates, createdAt to ISO string
and updateAt will also be changed to ISO string. 

With that in place, I have everything I need to fetch a single post I'd say,
let's now go back to the frontend and wire that up and there, I'm interested in
a single post in the well single post page here. 

In there, in componentDidMount I'm sending my request and I'll again adjust the
url to go to localhost8080/graphql, the method here will be a post request. 

For the headers I add my content type application json header and I will need to
prepare my graphql query here which is as before an object with a query key and
then the query is surrounded by these back ticks and in there, well I want to
reach out to my post query. 

I will send my ID, so my post ID I get up there, should be surrounded with
quotation marks and regarding the fields that I'm interested in, well thereafter
I use the creator name, the title, the image url, the date, the createdAt date
to be precise and the content, so I want to fetch that. 

I want to fetch the title, content, image url, creator and for the creator, only
the name and then also createdAt. 

That is what I'm interested in and this is now what I will append as a body to
my request, so json stringify and add this graphql query here. 

With that, we are sending that request as you learn before, handling the error
there will not really work, we want to handle that error after we parsed the
response data and then we can check for errors, so I'll copy that logic from
feed.js into single post.js, here where I check if we have any erros and then I
throw an error. 

If we have no errors, we just need to drill into the response and for that, you
must not forget how your schema looks like. 

We'll have data, then we have that name of the query which is post and then we
can access our different post properties. 

So here we access res data.data and then indeed, .post, .title and so on. 

So just .data has to be added to all these places where I extract some data and
with that, I should be able to load a single post. 

Save that and make sure your backend is saved and click on view and looks like I
have an error in my url, yes this colon needs to go and now let's click view, I
get user login failed. 

That is the wrong error message I copied there, fetching post failed but somehow
it failed so  let's quickly check what's wrong. 

Yes there is a syntax error in the query, we need to have surrounding curly
braces around the overall query. 

So edit your query to have an opening and closing curly brace right at the start
and end and thereafter if you click on a single post, now you'll load the post
data there. 

So this is now working, what's missing is a possibility to edit and delete posts
and of course to work with the user status. 

So let's work on that next. 

---