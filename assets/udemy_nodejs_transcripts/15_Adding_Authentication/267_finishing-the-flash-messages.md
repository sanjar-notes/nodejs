## 267. Finishing the Flash Messages

<strong><em>no description</em></strong>

So I added a message box in the last lecture, you can download the finished
version of the entire project attached, I simply added css classes to my div
which surrounds the message and then I worked on these classes in the main css
file, I added user message and user message error and also added some user
message entry to my desktop sys classes. 

So you can add this manually from the attached code, now one thing you'll notice
is that even if you load the login page regularly, you'll see an empty box here.


So even if no message is flashed, it looks like error message is not set to
undefined and therefore let's quickly go to auth and let's simply console log
request flash error to see what's in there that's causing this to not be
undefined basically. 

So if I reload this page, I see it's an empty array and if I do enter something
here, you see it's an array of messages. 

So in the end what do we want to do is we want to extract our message here is
equal to request flash error. 

Now if message length is now greater than zero, then I know I have a message in
there, so now I'll actually turn this into a variable by using let here and then
I can set message equal to message the first element because I want to retrieve
that otherwise I'll set message equal to null and now down there, we can use the
message and pass that as an error message. 

If we now save that, don't have the box here, if I do enter something invalid,
we do see the error message though but if I go to the login page regularly
without an error, I don't see it. 

So this is now how we can use these flash messages and output them in a nice
error box. 

Now here's also a challenge for you, find some other places in the login and
sign up screen where it would make sense to flash other messages onto the
screen. 

We'll do it together in the next lecture. 

---