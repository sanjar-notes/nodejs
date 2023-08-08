## 51. Using the Debugger

<strong><em>no description</em></strong>

So I still have my debugger up and running and now that I gave you a brief
overlook of how it works, let's actually send another message here. 

Hit send, it breaks again because I didn't remove the breakpoint and let's now
fix that error we have. 

I showed you how we can navigate, so let's click this line here or this button
to move to the next line. 

Now it registers this code and here you also see that it doesn't immediately
execute this function because if I click that button again, we jump to the end
of this function here and that makes a lot of sense because as I mentioned, this
function is just registered by nodejs to be executed in the future once the file
is read. 

So for now, code execution will continue with the other lines. 

Now the problem we want to solve is not inside of here though but if you want to
get notified once a part in here is reached, you can simply add a breakpoint
there, resume execution and it will break once it reaches that, so once that
callback is triggered because the right file operation is done. 

But our problem of course is the message, right, and the message is not
available here anymore, so this analysis is actually not useful to us. 

So let's remove that breakpoint and resume and let's again run this one more
time and now let's not resume execution but look into message and we see message
is message and that looks wrong, we see that parsed body is message equals and
then our value. 

Now since this is what we stored in the message constant, we now can tell pretty
clearly that our error has to be stemming from that part here because we clearly
have our value in here but then we seem to be extracting the wrong piece. 

Now split also does its job and you can even use the console here to for example
run some commands, you can run parsed body split equal sign here and see what
this returns, so you see you get an array with message and tist because I
mistyped test. 

Now this clearly tells you ok so split is working, I'm in theory getting all the
values I need, so the only thing that can be wrong now is the value I'm
extracting here and indeed we see that message, holds message which is
incorrect, message the first element in the array so I seem to be extracting the
wrong element from the array and indeed we are extracting the first one when we
should be extracting the second one here. 

So let's now change it to a one and now we get this error fixed. 

Obviously this is a bit of a constructed example but this is just to show you
how you can use the debugger to go through your code step by step, that you have
to keep in mind that node doesn't execute line after line but as I explained
multiple times now that it registers callbacks which are executed sometime in
the future and which should therefore also have to control with breakpoints if
you want to look into them. 

And with that, you should have some powerful tools for finding and fixing errors
in your code. 

---