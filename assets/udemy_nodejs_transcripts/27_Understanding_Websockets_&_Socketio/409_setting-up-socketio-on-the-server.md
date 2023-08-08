## 409. Setting Up Socket.io on the Server

<strong><em>no description</em></strong>

We want to use socket.io and we have to add it on both the server and the
client, so both on the node app here and on the react app because client server
will communicate through web sockets, so we have to establish that communication
channel on both ends, on the frontend react and on the backend, node. 

Now let's start on the backend here and for that, I'll quit my development
server here and I will install this socket.io package with npm install --save
socket.io, let me hit enter here and this will install the package into our node
project. 

Now how do we use it? 

Well let's go to app.js, so to the first file that runs when we start our server
and there, we should set up our socket.io connections we want to expose. 

Just as we set up our routes there in the end, we forward requests to our routes
and you could of course also do the socket.io set up in a different file but
I'll do it here but just as we set up our routes for the normal http requests,
we can also set up our socket.io channels and keep in mind, socket.io uses a
different protocol, web sockets and therefore web socket requests will not
interfere with the normal http requests which are sent by default by the
browser. 

So how do we set up socket.io here? 

Well once we connect to our database, when we start up our server, there I also
want to establish or I want to set up my socket.io connection. 

I'll create a new constant, io and I will require the socket.io package here. 

This package or the thing we are exporting here actually exposes a function
which requires our created server as an argument. 

Now the listen method here does actually return us a new node server, so we can
store that in a constant, this is the node server we spun up, it's stored here. 

We have to pass that to a function returned by require socket.io, so we add
parentheses here to execute that function that is returned by socket.io and we
pass the server to it. 

This sets up socket.io and I mentioned that web sockets build up on http, now
since this server here uses http, we used that http server to establish our web
socket connection that uses that http protocol as a basis you could say. 

Now this gives us an io, a socket.io object which does set up all the web socket
stuff behind the scenes for us and which we now can use. 

Now we can use it to define a couple of event listeners for example, for example
to wait for new connections, so whenever a new client connects to us. 

So then we execute a certain function where we get the client, the so-called
socket that did connect as an argument or the connection as an argument to be
precise, so this is the connection between our server and the client which
connected and this function will be executed for every new client that connects,
so not only one time but as often as required, as many clients as connect. 

So here I will print client connected and right now if I run npm start, we'll
never see client connected in the console, we don't see it here because we
established all that on the server side, we now got a waiting socket connection
or port you could say but we got no client which would connect and that of
course is the next step we have to do. 

---