## 418. Wrap Up

<strong><em>no description</em></strong>

So in this module, we had a closer look at socket.io and I hope it became clear
what you can do with it. 

You can push information from the server to the client through that emit method
provided by socket.io and I also mentioned that socket.io is not the only way of
implementing web sockets because behind the scenes, it's that web sockets
protocol that allows you to push data from the server to a connected client. 

Socket.io just makes using that web socket protocol, that technology
particularly easy and therefore it's a very popular package. 

Definitely dive into the official docs of socket.io to learn all about the
different features it offers and what you can do with it because it's a very
powerful library, it gives you a lot of cool features, so definitely check out
the official docs to learn more about it and of course also have a look at the
other implementations you might be able to use. 

I just want you to be aware that web sockets are something that build up on
http, you establish them as you'd see in our application, as a http handshake,
so you need a running http server either set up with just nodejs or a package
like express and you can use that server to establish a socket, a web socket
connection on top of that. 

So both run simultaneously and as you see in our example app, we actually got
both going on. 

We got normal requests so to say and we take advantage of socket.io as well. 

So this is an exciting piece of technology that might be interesting for your
next application too and I hope that this module provided a nice introduction to
it. 

---