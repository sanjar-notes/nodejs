## 362. Understanding Routing & HTTP Methods

<strong><em>no description</em></strong>

Now that we learned what the core idea is and how we transfer data and that data
is king in a rest API, let's have a look at the routing, so how do we
communicate between client and server? 

So we get client and server and on the server, we got our server side logic, we
reach out to databases and so on. 

Now we send a request from the client to the server and how do we do that? 

Well in a traditional web app as we built it thus far in the course, we did it
of course by simply adding a link on our html page for example or we had a form
with a button and we defined the form action and the method. 

Well it's not that far off for rest APIs. 

We still send the request to a combination of http method, also called http verb
and a path on the server. 

So what we defined thus far still will be used kind of, we still define such
paths, on the server, on the server side routing where we wait for incoming
requests and we also define certain http methods we want to handle for these
paths so that not all requests can reach all paths. 

These requests would be sent from the client through, when working in the
browser, through asynchronous javascript, so with the fetch API for example or
with Ajax and on mobile apps and so on, we also get special clients. 

The core thing here is we in the end still send normal requests, these are
totally normal requests that just don't expect any html response and we send a
combination of http method and path and this is how we communicate with our
server. 

Now in the rest world or in the API world, we like to call these things here API
andpoints, so when you hear me talk about an API endpoint, I'm talking about the
combination of a http method like post and get and the respective path. 

These are the endpoints we defined on our rest API and we defined a logic that
should execute on the server when a request reaches such an endpoint. 

Now talking about http methods, there are more methods than just get and post. 

I did mention this before in the course but when working with the browser only
and not with javascript in the browser but just with forms and links, then we
only have get and post available. 

These are the two methods the browser natively knows or the browser html
elements know so to say. 

When using asynchronous requests through javascript or when building mobile apps
and so on and using their respective http clients, you have access to more http
methods and we actually already saw that in the asynchronous requests module of
this course. 

Besides get which is responsible for getting a resource from the server and post
which is responsible for posting a resource to the server which means create it
on the server or append it to an existing let's say array of resources, besides
these two methods which we re-used a lot throughout the course, we have access
to put which we would use if we want to put a resource onto the server, which
means we want to create it or overwrite an existing resource, posts will never
overwrite or should never overwrite. 

We also have access to patch which is used for updating parts of an existing
resource, so not overwrite it entirely necessarily but update parts of it. 

We have access to delete which allows us to delete a resource on the server and
also there is a special options http method which we will use too in this module
indirectly though, it is sent automatically by the browser and I will come back
to it. 

This basically is a request which the browser will send automatically to find
out if the next request it tries to do, for example delete something, if that is
actually allowed and I will come back to that. 

So these are the http methods we will work with and the methods we typically
work with when building a rest API especially the first five ones, the orange
ones are important. 

Now let me also highlight that in theory, you can do whatever you want when a
request with a certain method reaches a certain path. 

So for the rest world, we should use a post request to create or append a
resource. 

No one is stopping you from deleting something on a server because ultimately,
you only define a method path pair on your server side and then you run any code
you want and what happens in that code is not restricted by the method that was
used to execute that code. 

You can restrict it yourself and you want to implement the rest API that follows
these ideas here but you don't have to and that's just important to highlight. 

It's common and it's a good practice, it's a best practice to use these methods
in this way because then anyone who's using your API clearly knows what to
expect to happen on the server for a given method but in theory no one is
stopping you from doing something else. 

So these are the http methods. 

---