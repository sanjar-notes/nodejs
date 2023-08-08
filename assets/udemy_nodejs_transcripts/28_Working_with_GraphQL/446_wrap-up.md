## 446. Wrap Up

<strong><em>no description</em></strong>

That was a lot of content on graphql and as I mentioned, you could fill an
entire course just on graphql and indeed there are courses on it. 

The official docs on graphql.org are a great place to dive deeper because
they're really good and there you can learn more about all the features graphql
offers, including its more advanced features. 

In this introductory module, I hopefully gave you a good overview over the
graphql core concepts and how you build a graphql API with node and in this
case, with the expressjs framework. 

You learned that graphql allows you or is a technique to build a stateless
client independent API, just as we did it with the rest API but that it offers a
higher flexibility than the rest APIs typically do because you expose a custom
query language to your client. 

A graphql API is made up of queries which you would compare to your get requests
in rest APIs. 

Mutations, that would be your post, put, patch and delete requests in rest APIs
and possibly all subscriptions, something I didn't cover in this module. 

You use these constructs to exchange data and to manage data and the important
and characteristic thing about graphql APIs is that they only expose one
endpoint to the client and that is a post request to /graphql typically, it has
to be a post request though, that is something you can't avoid and all requests
are directed there and then in the request body of that post request, you use
the graphql query language to describe the query you want to execute or the
mutation you want to execute. 

The server parses that incoming query expression and then calls the appropriate
resolvers to execute the logic you wrote and return the appropriate data or do
the appropriate manipulation. 

Graphql and that is also important is of course not limited to reactjs frontend
applications, you can use it with any frontend application, be that a mobile
app, a single page app with any framework or whatever you have, it's not limited
to react. 

Now when we compare it to rest, then we have to understand that rest APIs are
not strictly worse, they might still be the perfect solution for your next
project. 

They are especially great for static data requirements so where you don't need
that additional flexibility and then you have a very clearly structured and
explicit way of defining your endpoints and defining the possibilities your API
offers. 

So for file uploads or scenarios where you simply don't need that flexibility
because you always get the same kind of data, there rest APIs might still be the
perfect solution. 

In other scenarios, graphql might be better because you get a higher flexibility
due to that exposed full query language your client can use and I also want to
highlight that both rest and graphql APIs can be implemented with any framework
and actually even with any server side language. 

You are not limited to nodejs and on nodejs, you are of course not limited to
express and that is really important. 

The core concepts you learned here and a lot of the logic you applied will
actually be the same no matter which framework you use or no matter which server
side language you use. 

---