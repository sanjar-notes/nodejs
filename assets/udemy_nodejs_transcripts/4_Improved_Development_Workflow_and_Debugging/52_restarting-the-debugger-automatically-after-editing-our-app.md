## 52. Restarting the Debugger Automatically After Editing our App

<strong><em>no description</em></strong>

Now we worked with the debugger a bit and after this lecture, you'll also find a
lecture with a link to a more detailed explanation of the debugging capabilities
Visual Studio Code gives you. 

Don't learn them by heart but feel free to explore them to get the most out of
the debugger for you. 

Now there are two things I want to show you or I want to draw your attention to,
one is something you already saw. 

Let's add a breakpoint again and again submit this, I already showed you that
you can execute code here in that debug console at the bottom, so you don't see
the console logs here, you can also execute code here. 

For example you can type variable name here, so something which is available in
your code at this point of time, in general something which you can find in
local or in block here or in global, so the things you find here like message,
you can also type that down there and hit enter to print its value. 

And this is of course not really useful for printing because you can see the
value on the left too but as I showed you for parsed body, you cannot just print
the value, you can also run operations on it that will not affect your code as
it's running but that will allow you to look into it or try out some
transformation before you add it to your real code. 

So whatever you run down there does not affect the code you run up here but it
is nice for you to understand your code. 

The other thing I want to show you is that for now at the moment, if we change
something in our code here, let's say we add a blank line, our debugger doesn't
restart but with nodemon we actually have a package that does allow us to
restart. 

So it would be nice if the debugger would also restart if we change our code
otherwise it just behaves differently than the rest of our app and we have to
restart it manually. 

Now to restart it, let's go back to the explorer view for a second, we have to
go to debug and then add a configuration for nodejs. 

This adds the .vs code folder with the launch json file and this allows you to
configure debugging for this project and how it behaves. 

You can click on add configuration to see some demo settings you can add but you
can also just type in there and one setting you can add is restart and you can
set it to true, you just have to make sure that you also add some other fields. 

For example you have to make sure that nodemon is used and for that, you set the
runtime executable not to node which would be the default but to nodemon here. 

So now it'll use nodemon and it will restart the debugger when a change is
detected, so that not just the server is restarted but also the debugging
process. 

Here by the way in this configuration, you can also define that it should always
start with the app.js file so that you can even have the routes.js file selected
while starting debugging and it will still go for the app.js file which is more
convenient than always selecting the file you want to debug first before
starting the debugger and you always have to pick the app.js file because that
starts your server. 

So you can't say I'm going to look into the routes.js file so I'll start with
that, it always has to be the app.js file because you always have to start the
entire server, so here you can define that it will always pick that no matter
which file you have currently open. 

You can also change the console where things are logged to to the integrated
terminal which is the normal terminal. 

With this if you save all of that and you now start debugging, it fails though
and the reason for this is that it will not use the local nodemon but it looks
for it globally. 

Now to add it globally, you have to run an install nodemon -g and now important,
on Mac and Linux you might need to add sudo in front of this, on Windows you
don't, to get the right permissions to install this. 

With that you might be prompted for your password and now it will install
nodemon globally which makes sure that if you ever run nodemon in the terminal
now, it will not fail with a not found error but instead it will find it and
therefore now you can also run this debugger here which will use the global
version and you'll see it now opens terminal, starts nodemon and if you now add
a breakpoint somewhere and submit this again it still works as before, just
important, you now see the terminal here logs all the things. 

You can still use the debug console to output messages though, so you can still
work with this as I showed it to you, so this is not stopped from working, this
still is something you can use but in the terminal, you get the normal output
and you have to use the terminal because if you now change something, it
restarts the debugger and node and these are two separate processes and if you
stop the debugger, nodemon has to quit separately or has to exit separately and
you do this by hitting control c here and this couldn't be done in the debug
console which is why you have to funnel this to the terminal. 

So that's just something to keep in mind, you have to stop that process
separately which you can do from the terminal which is why if you are using that
nodemon process, you should use the integrated terminal and you can read more
about that in that detailed visual studio code debugging article but now you
have a setup where you have a debugger attached to your program that will
restart if you edit something, where the server will restart if you edit
something and where you have now all the tools you should need to debug your
node app and hopefully solve any errors you get. 

Now one important note, for the rest of the course I'll mostly use npm start and
not have the debugger attached all the time, I will only use that if there is
some error I want to particularly debug with the debugger and want to find with
the debugger. 

So you can use it as a default, always on option, I prefer to not to use it to
not have that extra panel and so on but to really just use the server and work
on that. 

---