## 407. What Are Websockets & Why Would You Use Them?

<strong><em>no description</em></strong>

Let's start with the status quo, how does our application we build thus far work
and with that, I'm not just referring to the rest API but to the shop we built
before that too. 

How do typical node or node express applications work like? 

We got our client, we got our server. 

The client would be our browser, mobile phone or something like that, the server
is of course essentially what we build, our node application. 

Now thus far, we always send a request from the client, we waited for this
request on the server, we set up some routes to handle different kinds of
requests and once we're done doing something on the server, for example reach
out to a database, we send back a response to the client. 

So first request then response. 

Now that is how our application works thus far and this is how most web
applications work and by the way, we're now not going to replace this with
something totally new which we'll then use all the time, this is a fine pattern
because a lot of resources on the Internet should be available by this pull
approach. 

So you pull information from the client, you tell the server that you want
something, this is a typical approach and is a fine approach but sometimes you
have a different requirement. 

What if you want to send something from the server to the client, so what if
something happens and you want to inform the client? 

Let's say you're building a chat application, user A on PC A or on his mobile
phone sends a message to user B. 

Now obviously they're not sharing the same device, they might be in two totally
different places on the world. 

Now user A sends a request to the server that contains the message and the
server stores the message in the database and the server can return a response
to user A but user B, the person with whom user A chats does not send a request
to the server asking for the message or at least that is unlikely to happen. 

You could certainly use some patterns where you send a request every second to
see if there are new messages but you'll then hammer your server with requests
where most requests will not yield new messages. 

So instead it would be nice to have some push way of informing user B about the
new message and that is exactly the scenario we're looking at here. 

What if something changed on the server and we actively want to inform a client?


Well then we can use web sockets instead of http. 

Now http is the protocol we used thus far where we send a request and we get a
response. 

Web sockets build up on http, they are established via http, they use a
so-called http handshake to upgrade the http protocol to the web sockets
protocol and the web sockets protocol, that simply talks about how data is
exchanged, right. 

So this protocol is something you don't have to manage actively, the browser and
the server communicate through a protocol and the used protocol defines how the
communication can happen. 

With http, it's request response, with web sockets, it is push data or actually
it's both. 

We can also send data from the client to the server, this is still included but
most importantly and that's the feature I really want to highlight here, we can
push data from the server to the client. 

And you can and you typically will use both together in one and the same node
app, so it's not like you have to decide, do I build an app with web sockets or
do a build one with http. 

You still have a lot of places where you want to use that request response
pattern, for example if you are sending a message or if you're creating a user,
these are operations where you do send some information from the browser to the
server. 

So there, the request response scenario makes perfect sense but if you have some
active notification you want to get to your users, then you also want to
integrate web sockets. 

Now let me show you how to add web sockets to your project in the next lectures.


---