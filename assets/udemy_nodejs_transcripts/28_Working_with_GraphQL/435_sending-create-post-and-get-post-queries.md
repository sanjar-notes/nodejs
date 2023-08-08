## 435. Sending "Create Post" and "Get Post" Queries

<strong><em>no description</em></strong>

<v Maximilian>So let's use that query here</v> from the front end. 

And for that, I'll go to my React application, of course. 

There, the Feed.js file, and here we have to scroll up a little bit to load
posts. 

There we have some pagination logic, which we can ignore for now. 

And then I'll write my GraphQL query here which is a JavaScript object where I
have a query which now is that multi line string. 

And in that multi line string I now will start with curly braces right away. 

And in there, just as I did it in GraphiQL, and therefore we can, of course,
again, copy that. 

I'll look for posts. 

This is the name of my query. 

And in there, this happens to return this post data object which has posts and
total posts. 

And for every post I'm interested in the ID, title, content, image URL, also
creator and also created at, creator again as a complex object and there I'm
interested in the name. 

So this is the data I need to render my posts efficiently. 

Now to run that query, let's change that URL down there. 

And you know which URL that is. 

It's localhost:8080/graphQL. 

The method will be post, of course, headers is the token, but also the content
type, which should be application/json. 

And of course, I need to add my body here and that body will be stringify with
the json package, and that will be that GraphQL query I wrote up there. 

And please note again, that we see the entire flexibility of GraphQL doing its
job here. 

We're fetching exactly that post data we need. 

We don't fetch things like the creator email which we don't need. 

We don't fetch the updated at field, which we don't need. 

We only fetch what we need and we actually don't even need the image URL here,
now that I think about it. 

We're not rendering that image on that starting page. 

So really, we only fetch what we need and we use GraphQL to its fullest
potential here. 

But back to our request. 

I'm now sending this request. 

Now, again, handling errors like this will not succeed. 

Instead, we wanna handle it as we did down there. 

We don't need to check for validation errors though because in this query we
can't send incorrect data. 

So we'll simply check if we got any other errors and I'll then say fetching
posts failed and otherwise we'll have our posts and we can't access them on
resData posts though, as you know. 

Instead, if we have a look at our schema our post data will be found on data
then posts because that's the name of the query. 

That will be an object of this type with another field of posts in there. 

And then we drill into our post data. 

So here the posts, the final posts can be found on resData.data.posts.posts. 

This is the query, and this is then the posts field in the return data of the
query. 

And then we can let React do its job. 

For the total posts it's all the resData.data.posts, and then it's not total
items, but total posts. 

I renamed that on my backend. 

If we now save that and we go back to our React application, we can already see
it. 

That error is coming from the user's status. 

But behind that, we see our posts are getting rendered. 

We see the user name, so that is all working. 

And now let's also add the code to add a new post to this page immediately,
before we then also add pagination, and then also have a look at how we can get
our image onto the server. 

So let's quickly add the code. 

To add a new post immediately, we do that in the Feed.js file off the front end
code in the finishEditHandler. 

And there we scroll down to the place where we create our post object. 

We're not actually doing anything with that thus far so that's time to change. 

So there with this post, I prepared some code which you can now use. 

You can just copy it in and replace this prevstate statement with the attached
code and thereafter, go back to your application and add another cup, for
example, also hot and hit accept, and you see that cup here too. 

Pagination is not working but it'll take care about that later. 

For now, we can add that and we can load our posts in general. 

---