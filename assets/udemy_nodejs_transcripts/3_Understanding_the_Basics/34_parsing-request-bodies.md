## 34. Parsing Request Bodies

<strong><em>no description</em></strong>

So time to parse the incoming requests and get the data that is part of the
request because that data should be whatever we entered here. 

Now how do we get access to that? 

Well we get requests url and request method, you might think there is something
like request data but there isn't. 

Instead the incoming data is basically sent as a stream of data and that is a
special construct javascript in general knows but nodejs uses a lot, now what is
such a stream of data though? 

There is a connected concept, buffers and we'll have a look at both here. 

So let's take our incoming request as an example, there also are other streams
like for example when working with files, we can also work with streams but
let's stick to requests here. 

Our stream here is basically an ongoing process, the request is simply read by
node in chunks you could say, in multiple parts and in the end at some point of
time it's done and this is done so that we theoretically can start working on
this, on the individual chunks without having to wait for the full request being
read. 

Now for a simple request like the one we're working with, this is not really
required, we only got one input field data, it doesn't take so long to parse
that. 

But consider a file being uploaded, this will take considerably longer and
therefore streaming that data could make sense because it could allow you to
start writing this to your disk, so to your hard drive where your app runs, your
node app runs on your server whilst the data is coming in, so that you don't
have to parse the entire file which is of course taking some time and you have
to wait for it being fully uploaded before you can do anything with it. 

But this is how node handles all requests because it doesn't know in advance how
complex and big they are. 

So you can start working on the data earlier, the problem is with your code, you
can't arbitrarily try to work with these chunks. 

Instead to organize these incoming chunks, you use a so-called buffer, a buffer
is like a bus stop. 

If you consider buses, they're always driving but for users or customers being
able to work with them, to climb on the bus and leave the bus, you need bus
stops where you well you can track the bus basically and that is what a buffer
is. 

A buffer is simply a construct which allows you to hold multiple chunks and work
with them before they are released once you're done and you work with that
buffer. 

Now that's pretty abstract but it's pretty easy to work with fortunately so
let's see how that works in practice. 

When receiving a posted message before sending the response and before writing
to the file, we want to get our request data, right and we do this by going to
our request and registering an event listener. 

We haven't done that thus far but as I mentioned, node uses these heavily. 

For create server, it implicitly creates one for us, now we do this on our own
by using the on method. 

Now on allows us to listen to certain events and the event I want to listen to
here is the data event, you see my IDE even gives me some help here and tells me
which events I can listen to for a request. 

So here I want to listen for the data event, the data event will be fired
whenever a new chunk is ready to be read, you remember that buffer thing, this
is basically helping us with that. 

Now here we have to add a second argument which is that function that should be
executed for every data event, you remember create server, it had a similar
concept. 

There we defined a function that should be executed for every incoming request,
now we're defining a function to be executed for every incoming data piece. 

So here I'll again using an ES6 arrow function, you could also use the function
keyword without that arrow then and as you can also see on data, this listener
receives a chunk of data. 

So here we receive a chunk and this chunk is something we can work with here and
now we have to do something with this chunk to be able to interact with it. 

For this I will create a new constant here and I'll name it body because I'll
try to read the request body, you can name it however you want but it is the
request body we're working with. 

Now the body should be an empty array and now in that function here in the data
event, I'll take my body and push a new element onto it. 

By the way if you're wondering how we can edit a constant value, this only means
that we can never re-assign a new value, so we can never use body equals
something again but with push we're changing the object behind that body
element, that body object, we're editing that data in that object not the value
itself, not the object itself. 

It's a bit strange to wrap your head around but this is in the end how it works.


So we can now push a new element into this array to make it non-empty and we
push our chunk here. 

Now nodejs will execute this so often until it's done getting all the data out
of our request, that can be once, that can be multiple times and we can even log
this to see how app, how often it does this and what's inside of this chunk. 

Now we need to register another event listener and that is the end listener,
this will be fired once it's done parsing the incoming requests data or the
incoming requests in general. 

Here it will again execute a function we define as a second argument and in this
function, we can now rely on all the chunks being read in and they're all stored
in the body now. 

Now to interact with this and don't forget the comma after end, to interact with
that, to work with all these chunks, we now need to buffer them. 

Remember that bus stop concept, we get all these chunks we now need to do is
something to be able to work with them, to basically have one place where the
bus stops and we can interact with it. 

So here I'll now create a new constant, parsedBody and there I will use the
buffer object which is available globally, made available by nodejs and I can
concat my body. 

So this will in the end create a new buffer and add all the chunks from inside
my body to it. 

And then on this buffer which I got here, parsed body is now a buffer, there I
can call toString to convert it to a string. 

So this is a utility method offered by nodejs where we do something to our
buffered chunks, remember the bus is now waiting in the bus stop so to say, the
buffer is our bus stop and now we do something with it, here we convert it to a
string and this only works because I know that the incoming data will be text
because the body of that request will be text. 

If it were a file, we would have to do something different but it is no file and
I know that it isn't because we're writing the code, we know what we will
receive, right. 

So this is the parsed body and this is now finally what we can work with, so
let's also output the parsed body. 

And this was a lot of talking so let's simply have a look with the server, with
control c and restart it and then send another request with some message here. 

And now if you have a look at what's being logged, you see two elements. 

The first one is coming from this console log and you see that is a chunk, that
is a chunk we can't work with but now the parsed body receives or yields this
line and that is something we can work with and it's message equals something
because we named our input here message and as I said, that form will
automatically send the request where it takes all the input data and puts it
into the request body as key value pairs where the names assigned to the inputs
are the keys and the values are what the user entered and that is what we have
here, a key value pair separating the key from the value with an equal sign. 

Now and with that, we can now work with that and finally store the input in our
file and we can do that here in request on, request on end to be precise by
creating a new constant, message, taking the parsed body and splitting it on the
equal sign and then taking the element with the index one which is the second
element in the resulting array which is the element on the right of the equal
sign. 

And now we can move write file sync into the end function, we don't want to
execute it here because this will actually run before this function is called
because here we just register a function to be called in the future, it's not
executed immediately, remember node doesn't wait and pause, it will not block
the script execution, it just registers this as a to-be-executed action and then
right away continues. 

So if we have something that depends on the incoming data, we have to move it
into the event listener too so that it's also part of the to-be-executed code
sometimes in the future and doesn't run too early and now we can write message
to the message.txt file. 

Let's now restart this file one more time and enter hello here and hit send and
now if you look into message text, we see hello, you see the exclamation mark
was encoded. 

Now that is something we can worry about later but in general, this worked just
fine. 

And if you're now totally frightened by how complex nodejs is, this is the raw
logic, we'll later use expressjs which hides all that raw logic but to
understand why we use that, you first of all need to understand what is
happening and why using tools like expressjs which will make all of this much
easier are great. 

So with that, we've got our basic logic down, let's now dive again into that
event listener and writing files thing because there is something really
important you have to understand. 

---