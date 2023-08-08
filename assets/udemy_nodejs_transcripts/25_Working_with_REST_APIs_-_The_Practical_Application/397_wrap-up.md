## 397. Wrap Up

<strong><em>no description</em></strong>

That's it for this module. 

You learned that when moving from a classic node application which I don't mean
in the sense of how you built it in the past, so simply just an application
where you render  the views in the server, that is a classic application because
it is what we started with in this course. 

So if you move from such a node application to a rest API, you'll learn that
most of the server side code does not change, you work with validation files and
so on in exactly the same way as you did with well the classic approach. 

Only request and response data changes because there you send json data, you
don't render any views. 

You also got more http methods available which you can use to construct your
endpoints, your API endpoints and the most important takeaway is that the rest
API server does not care about the client. 

The requests are handled in isolation, so every request is treated as if it
would arrive for the first time. 

So we don't use sessions, the server, the rest API does not store any sessions,
it does not store any client data. 

Now that has important implications for authentication. 

Due to no sessions being used, the authentication works differently. 

Each request needs to be able to send some piece of data that proves that the
request is authenticated and that is this json web token which we generated and
worked with in this module. 

It's a common way of storing some authentication information in a token, a piece
of data which you send to the client, which you store on the client and then
which then gets attached to every outgoing request to a protected resource. 

Json web tokens are signed by the server and only the server can validate them
by using a private key which is only known to the server, hence you can't fake
or manipulate tokens on the client and that's it for this module. 

We now had a detailed look at building rest APIs, a common form of node
application which you need and a lot of scenarios and now you have already a
very broad toolset which allows you to build extremely versatile and powerful
node applications. 

We're still not done with the course though, there's more to come. 

---