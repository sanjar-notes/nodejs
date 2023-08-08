## 412. Sharing the IO Instance Across Files

<strong><em>no description</em></strong>

To be able to re-use one and the same io object that manages the same connection
that is exposed, let's create a new file. 

I'll name it socket.js, the name is up to you though and in that file here, I
will create a new variable which I'll name io and then I'll export with the
nodejs export syntax, an object, in that object I want to have two methods, two
functions. 

The init method and this is how you define a function in nodejs syntax, you have
that key here like in a normal object then a colon and then the value and the
value here is a function which receives the http server as an argument and in
that function body, I'm using an arrow function here of course, in that function
body, you require socket.io, so just as we do it in app.js here, we require
socket.io and we pass the server to the function that gets exposed by the
exported object or by that exported package. 

So here I also execute this function and I pass in that http server I expect to
get here as an argument. 

Now the result of that is our io object which I'll store in that io variable
here and then I can return io like this in the init function. 

In app.js, I can now require /socket, so my own socket.js file and there I will
call init, this function I just defined in there, so this function, I call that
and there I still pass my server because in that function I expect to get that
server. 

The other code here does not change, it stays the way it is. 

In socket.js I now just add another function, so another key value pair in that
exported object, so let's add a comma and then I'll name this get io, the name
is up to you just as it was for init by the way. 

Here I don't expect any arguments but in the function body, I'll check if io
does not exist, so if this variable is undefined in which case I'll throw a new
error, socket.io not initialized or something like that. 

If I make it past this if check, I know that io has been initialized and then I
will just return it. 

Now with this, we're managing the connection in this file and we can import this
file in all the places of our app where we need to be able to interact with io,
like our feed.js controller. 

So let's continue with that next. 

---