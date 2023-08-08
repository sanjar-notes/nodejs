## 511. Using Type Casting

<strong><em>no description</em></strong>

<v ->I want to start with some extra TypeScript features,</v> which you can
utilize. 

Maybe you saw that when I accessed the request body or the request params, I get
auto-completion as long as I work on the request object. 

For example, there I get help and I can understand that there is a body
property. 

But what I then access on the body itself is really flexible. 

I can access anything there because the TypeScript does not understand what will
be in the body of the incoming request. 

And the same for the params. 

You could argue that it should be able to understand what's in it because we
encode it here, but that's not how TypeScript works. 

It's not able to analyze your averacode to understand what should be in this
params object. 

Long story short, params as well as body, in the end here, is of type any. 

That's the type of body and that's the type of params. 

Well, params is actually a params dictionary. 

But that's essentially just an object with key value pairs, where any keys are
allowed. 

The problem with that simply is that we don't get the best possible TypeScript
support here. 

If I wrote texts here, nobody would warn me about this mistake. 

And we're using TypeScript to avoid mistakes like this. 

Of course TypeScript can't anticipate which kind of data we get on incoming
requests, but we as a developer should know which kind of data we get there. 

We can let TypeScript know about this. 

And now to make TypeScript aware of our knowledge of how a request body should
look like, we can alter this a little bit. 

We can set the body here, equal to request body, and then use type conversion
with the ask keyword to convince TypeScript that this is of a certain type. 

And now we can define a type of our choice that reflects how a body, how a
request body for this route, should look like. 

So for example, here, we set this to an object type, where we know that there
will be a text property which would be a string. 

And now if we use this new body down there, we can access text on that, but if
it access texts, I get an error. 

Of course we can generalize this. 

I can extract this type and create a new type alias up there. 

Request body, set this equal to this object type, and then use this request body
type alias for my conversion down there, and also in any other places where I
expect something. 

For example, here, where I expect to get data, like this. 

I can utilize this body in all the places where I access request body to get
that extra type safety, and avoid typos. 

And of course we can do the same with the params. 

We know how the params will look like, so I could add a type alias here, request
params, but with that we could register another object type here on this type
alias, and add the todo ID, which is also a string. 

And then we can use the exact same pattern on the params. 

So here I got my params, which is request params as RequestParams, and now I can
use params here, and again if I now have a lower case I, for example, I get a
warning via TypeScript. 

So now we have this improved TypeScript usage here. 

And of course we can do the same here for deletion. 

Now, of course you can define multiple aliases for bodies and params if you have
different routes with different kinds of bodies and params. 

Here, I just always happen to work with the same kind of request body and the
same kind of request params, but you could have multiple, differently named type
aliases here, to use this pattern in different routes. 

With that, we improve this code even more. 

And now, we're really taking advantage of TypeScript to force us, as a
developer, to write better code. 

---