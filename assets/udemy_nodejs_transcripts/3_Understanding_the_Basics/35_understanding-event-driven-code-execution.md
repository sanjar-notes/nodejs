## 35. Understanding Event Driven Code Execution

<strong><em>no description</em></strong>

We already achieved a lot in this section, and I know that all this code looks
kind of intimidating and no worries. 

It will become much easier, but I find it super important to learn it the hard
way first so that you never forget what's happening behind the scenes. 

Now, one crucial thing which I know that people often struggle with is that the
order of execution of your code here is not necessarily the order in which you
write it. 

For example, this here will actually execute after this code, so it will even
execute after we already sent a response. 

This has two important implications. 

For one, sending the response does not mean that our event listeners here are
dead. 

They will still execute, even if the response is already gone. 

But it also means that if we do something in the event listener that should
influence in the response, this is the wrong way of setting it up. 

We should then also move the response code into the event listener if we had
such a dependency. 

But it also means that it's super important to understand that with request on
or code like HTTP create server. 

These are some examples where no case uses a pattern where you pass a function
to a function and node will execute these past in functions at a later point of
time, which is called asynchronously. 

Now, it's not always the case that a past in function is necessarily executed at
a later point of time. 

But no case uses this pattern heavily and throughout the course. 

I'll, of course, let you know when this is the case and when Node executes
something asynchronously. 

In such cases, no charges won't immediately run that function. 

Instead, what it does when it first encounters this line is it will simply add a
new event listener internally. 

It manages all these listeners internally. 

In this case, for the end event on the request, which will be triggered
automatically once no chars is done parsing the request. 

So this is something no trace does for you. 

And it will then call that function for you once it is done. 

So in the end, you can think of this like no charge as having some internal
registry of events and listeners to these events. 

And a function like this is such a listener and when sort of something happens,
so when Node.js is done parsing your request, it will go through that registry
and see I'm done with the request, so I should now send the end event. 

So let's see which listeners I have for that. 

And it will then find this function and any other functions you might have
registered for that and will now call them. 

But it will not pause the other code execution and that is so important to
understand. 

So for example, here now since I moved return response and into this function,
the flow is like this. 

It will now reach this if statement and if these conditions are met, it will go
inside of it. 

It will then register these two handlers and not immediately execute these two
functions. 

Instead, the functions are just registered internally in its event emitter
registry and then it will jump straight away to the next line. 

And therefore right now if I would restart my server, save the code and restart
my server here. 

You will see that if I enter something here, I actually get redirected to this
page or not even redirected. 

As you can see, there is no 300 status code. 

Instead, it just loads this page because it executes these lines because as a
now mentioned multiple times, it will not execute this right away and this
return statement will therefore not quit this overarching function here. 

Instead, it just registers this callback and immediately moves on to the next
lines and it would eventually execute this line. 

But that is already too late, which is also why we get the cannot set headers
error here because it already moved along and executed this code when all of a
sudden the parsing of the request finished and it executed this code and tried
to again send a response which obviously is too late because it already did
here. 

Now, I know that this is hard to wrap your head around, but it is a crucial
concept that you can register code functions which run sometime in the future,
but not necessarily right now. 

And therefore the next line of code, this code here can run or will run before
this code, simply because this is just a callback to be called sometime in the
future. 

And this setup is important because otherwise node would have to pause until
it's done, pause until it wrote the file, and if it does that, it will simply
slow our server down and it's not able to handle our incoming requests or do
anything of that kind until it's done. 

And that is not what we want. 

We don't want to block our code execution. 

We always want to be in that wait for new events, loop the event loop and then
only execute code once it's due to be executed and never block that event loop
for too long of a time. 

And this is why we have this setup and this has one implication for this line
and for this line. 

The implication for this line is that we reach it too early. 

So to avoid this, we should actually return here. 

We simply return requests on so that this gets executed, but the line thereafter
doesn't. 

And the important application about this line will be discussed in the next
lecture. 

---