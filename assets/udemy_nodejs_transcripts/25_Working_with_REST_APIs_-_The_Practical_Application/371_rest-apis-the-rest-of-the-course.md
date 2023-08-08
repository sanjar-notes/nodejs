## 371. REST APIs & The Rest Of The Course

<strong><em>no description</em></strong>

Before we start working on the project, let me quickly have a look at rest APIs
and the other knowledge you gained throughout the course, is that now all
redundant? 

We learned about things like setting up our node and express app, routing,
handling requests responses, request validation, database communication, file
handling uploads downloads, sessions and cookies and authentication, these are
some big topics we covered throughout the course. 

Now how do we have to adjust our knowledge now that we build a restful API
instead of a view based application? 

Well regarding the general setup, we already saw that in the last module there
are no changes we need to do, we still set up a normal node and express server. 

Regarding the routing, we also have no significant changes, we just use more
http methods, more http verbs now, that's the only difference in the end. 

For handling requests and responses, you already learned that now we work with
json data instead of views, so that is a difference. 

We render no views anymore, we have no views folder anymore, we don't use ejs
handlebars or anything like that, instead we only exchange data. 

So that is a change but as you learned in the last module, this is also not too
hard to implement. 

Now if we want to add validation for incoming request data, then we will not
have to change anything. 

We still can add validation for example with express validator which we used in
the validation module of this course and the way we use it and the logic behind
it does not change a single bit. 

Database communication, so working with database, be that a SQL or NoSQL
database also does not change, this happens on the server side in a controller
action typically and the logic we write there, the code we write there is not
affected by the data we exchange or by the fact whether we render a view or if
we send around json data. 

When we talk about file uploads downloads and so on, there's also not much that
changes. 

On the server side nothing changes actually, on the client side the logic
changes a little bit and I will show you how we can implement file upload and of
course also serving files in this module. 

Now for sessions and cookies, there we have changes because we will not use
sessions and cookies anymore with rest API and the reason for that simply is
that you learned about these restful principles or these rest API principles and
one of them was that each request is treated separately, it is looked at
independently from previous requests, so we have no connection between the
client and server, we have no shared connection history to be precise and
therefore, we manage no sessions on the server because the rest API does not
care about the clients or whether that client connected to the API before and
therefore authentication will also have to change. 

We'll use a different authentication approach and I'll show you which approach
this is and how to implement it in this module too. 

So overall, there are not too many changes. 

Some changes, he biggest changes are related to sessions and therefore
authentication and I will show you how to implement them but the rest will still
work the same you learned it and therefore all the knowledge you gained
throughout the course is of course everything but redundant, it's still super
important. 

And with that let's dive in, let's see which project we'll be working on and how
we can work on it. 

---