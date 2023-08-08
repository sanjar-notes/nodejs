## 36. Blocking and Non-Blocking Code

<strong><em>no description</em></strong>

So what is wrong with this write file sync line here? 

Well it's the sync keyword. 

I earlier mentioned that there also is a write file method but we use write file
sync, the sync here stands for synchronous and this is a special method which
will actually block code execution until this file is created. 

Now working with files is available in two modes, here is the synchronous mode
and we block execution of the next line of code until this file is done. 

Now for this short of a text we enter, this is super fast and we won't even
notice it but think about a huge file, a couple of hundreds of megabytes or even
bigger, if you do something with that, read it, copy it, whatever it is and you
block the code execution, then the next line and all the other code will not
continue to run until that file operation is done and even new incoming requests
of other users would not be handled until that file operation is done and you
don't want that, therefore you should not use that syntax here. 

You can if you know you'll only have a very short file operation but even then,
it's better to use this write file method here which actually does not just
accept the path and the data but also a third argument and that is again such a
callback, so a function that should be executed when it's done. 

So here again just as with create server, nodejs implicitly registers an event
listener for us. 

So here, I pass another function and this callback here actually receives an
error object which will be null if no error occurred but if some error occurred,
missing permissions or anything like that, you would get it here and you could
then handle it gracefully by returning a different kind of response, an error
response showing to the user that an error occurred and otherwise return a
normal response. 

Now here  I won't do error handling and there is really nothing that could go
wrong here, we'll of course dive into error handling a bit more later in the
course but I will move my normal response code in there because this response
should only be sent if we're done working with the file because that is
ultimately the action we want to do upon our request, right. 

So now we actually have our event listener with some method or function that
will be executed once we're done parsing the request and in that function that
will be executed sometime in the future, we have yet another event listener,
this nested function here which will be executed once we're done writing the
file and this is actually pretty standard for nodejs. 

You have this event driven architecture where you basically tell nodejs please
do something and it will then go ahead and offload that process to the operating
system which does use multi-threading and so on and will then continue its event
loop to listen for event callbacks and always just dispatch tiny actions like
that to never block the code execution and then always just come back once an
operation is done by the operating system and so on. 

So this is what nodejs does here and why it is high performant because it never
blocks your code, it never blocks the server, it just goes ahead and tells the
operating system do that, do this and then eventually comes back and does
something in the callback, like send a response which is not a blocking
operation because this is super fast, just a couple of headers and off you go. 

So I hope this is clear and with that let's restart this by quitting the server,
re-running node app and going back to just slash nothing, let's enter hello
again here and send. 

And in message.text we see that, again concatenated with an extra character, not
something we have to worry about right now. 

So you see write file also works but this is the way you should use it due to
the asynchronous nature of nodejs which I hope now became clear because it is a
crucial concept of nodejs and one you absolutely have to understand. 

With that, let's wrap this module up with these core basics and let's from now
on to move to a more easier route where we will make our life simpler and not
write all this nitty gritty detail code on our own but it is super crucial that
you understand what's going on here. 

---