## 50. Logical Errors

<strong><em>no description</em></strong>

Now the third kind of error I want to discuss is the logical error and that is
often the most difficult one to fix because it will not cause an error message,
your app will just not behave the way you expect it to. 

Let's see here in the routes.js file where we parse our body, we're retrieving
the message here and that is of course nice but let's say I actually do have the
first element being stored in message here and keep in mind the second element
which we previously had is the actual message the user entered because we're
splitting that key value pair we're getting automatically and now we're actually
storing the wrong element. 

So now if I save this and my server restarts due to nodemon, I can enter some
test here and if I do this and I open my message text file, I actually see
message there. 

Now this is a logical error because we got no error message but the app is not
behaving the way we want it to. 

Now of course we know that we used the wrong index here because I just changed
that but let's say you worked on that code for the first time and you just use
zero here because you forgot that this should be one, so you didn't change that
back on purpose but you really made this mistake. 

Now it's not super obvious to see and how can you now work on such errors? 

Well with the help of the nodejs debugger which actually has a great integration
into visual studio code which I strongly recommend using. 

Let me show you how that debugger works then. 

For this, let's quit that process and let's select the app.js file now, that's
important and now go to debug here in visual studio code in the menu and choose
start debugging or use the keyboard shortcut you see there. 

Now with that, you have to choose an environment and there you should use nodejs
and you will now see that extra bar here at the top which allows you to control
the debugger, you see the red bar at the bottom that indicates that you're in
debugging mode and you actually also have a debug console here where you now see
that the debugger is attached and listening. 

Now what does this mean? 

This means that now you actually can look into your code as it's running but to
really do that, you need to set so-called breakpoints. 

So let's go to the route.js file and let's say we assume it has something to do
our error here with the wrong text being stored with this code snippet because
ultimately, that is where we write it to the file. 

So what you can do is you can set a breakpoint in visual studio code by going to
the left of the line numbers until you see that red dot and clicking there. 

Now we got a breakpoint there and what will now happen is that with that
debugging process running, don't quit this, you can quit it by clicking the red
square but let's leave it running, if you now submit some text here, it should
automatically jump back and mark this line like this, highlighted yellow and
kind of put this yellow arrow around our breakpoint. 

This means that the code execution now stopped here, it did not continue, it
stopped and it stopped so that you can look inside of it and actually you can
now analyze your code in the moment it's running. 

For example you can hover over your variables to see what's stored inside of
them, so for example you see that the parsed body is this string which we're
splitting in the yellow highlighted line. 

You see what's inside of the body you passed to concat, that it's an array with
a buffer of length 12 for example. 

You can even expand this to look into it a bit more and find more details about
the buffer, in case you're interested here. 

You also can go to view and then debug here, this gives you a special debug mode
where you see the key variables you have available in your code right now,
message is undefined because we stopped in that line where we would set it but
it stops before it executes the line, so therefore message is still undefined at
this point  but parsed body for example does hold the value, well it has which
you can also see if you hover over it. 

You don't just see local variables which are available in this function but
block variables too, this is the variable which is always available outside of
this function, it's this variable and you can also look into that therefore and
you can generally click around to see some global values and the values they
currently have stored and a couple of these things. 

You also can define watchers here, for example you can click a plus here and
then watch message and hit enter and now you will always see that here, you also
see it up here but if you ever close that, you can define some variables you're
particularly interested in and watch them whilst you go through your code. 

And you also see your breakpoints down there, you see all the breakpoints you
set, you can uncheck them here to not stop execution the next time they are
reached and so on. 

You also see the call stack which looks very cryptic but what in the end just
shows how the process went through your code and you can click on these
different parts to see where actually this code which belongs to the code that
was executed can be found and not all of that is code you wrote, a lot of that
is core nodejs code. 

Ok so that's the debugger in a nutshell. 

Now to work it and to continue with your code execution, you can use that panel
here at the top. 

You can resume code execution with the play button but we don't want to do that
instead we want to step through our code step by step so that we can see when it
fails or where it goes wrong. 

And you can do that with this button which steps to the next line basically or
with this button here  which doesn't just step into the next line but actually
even goes into functions like this one. 

So if you click here and again, now all of a sudden you're in the write file
function defined by nodejs and you can step out of there with this key. 

Now you see if you continue here that this wasn't too helpful but that we can
now navigate like this in our code. 

So now let's make this more helpful and for that, let's try this again and use
that debugger properly now. 

We'll do this in the next lecture. 

---