## 410. Establishing a Connection From the Client

<strong><em>no description</em></strong>

We want to go to our react app and there, I'll quit the development server too
and here, I will also install a new package with npm install --save and that
will be socket.io-client. 

So it's a different package name, it's socket.io-client because it is the code
that will run on the client, hit enter and this will install that package into
our react project. 

Now once this is done, go to the feed.js file in your react project and there at
the top, first of all import with that frontend import syntax that differs from
the backend syntax and you can learn more about that in my react course. 

But there, import open socket, you can name it however you want but this will be
a function that opens a new connection, a new socket, import open socket from
socket.io-client, so from that package you just installed. 

So this exposes a function on the client too and this is a function that allows
you to connect. 

Now let's go to that componentDidMount function here where we load our first
posts and so on and after we loaded these posts here, after this line, let's
call this open socket function and now you need to define the url of the server
where you've established your socket.io server and that of course is our backend
server address. 

So it's http localhost 8080, nothing else is required and please note you do use
http here because web sockets build up on that and now this function which is
provided by socket.io will do all the heavy lifting behind the scenes. 

And if we now save that and we restart our frontend too and the backend is
running as well, let's wait for that development server to restart so that our
application here in the browser will actually reload. 

And now this should have already executed this open socket code because the page
did reload, so if you now go to the backend, you indeed see client connected
here because now we got an established connection between a client and our
backend application through socket.io and all the other normal http requests
will still work as before. 

Now let's use that connection for something useful and let's see what we could
do with that socket.io connection that would make sense in our app here. 

---