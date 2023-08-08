## 238. What is a Session?

<strong><em>no description</em></strong>

So we had to look at cookies, what is a session? 

Well we have the same set up as before, user using the frontend our view is
interacting with our server where we have our node application code. 

We send a request and we do login and again let's assume we do send the valid
credentials there, we're not validating them in this module because I want to
focus on sessions and cookies. 

So now instead of storing the information that the user is authenticated in the
frontend which was a bad place as we learned, we'll store it in the backend with
a so-called session and a session is a new  construct which we haven't used
before. 

With that I'm not meaning that we store it in the request because we already saw
that this will not work and I also don't mean that we store it in some variable
in our express app because that would be shared across all users and all
requests, we only want to share the information across all requests of the same
user and that's really important, the same user so that other users can't see
your data, can't assume your role, can't tell the server that they are
authenticated, only you are authenticated. 

Now for that, we need to store it on the server, we'll start by storing it in
memory which is then pretty similar to storing in that variable but eventually
we'll move to a different session storage, the database and we need one
important piece of information. 

A client needs to tell the server to which session he belongs because the
session will in the end just be an entry stored in memory or stored in a
database. 

Now we're not matching this by IP address or anything like that because that is
a bit hard to maintain and can be faked and all that fun stuff, so we're not
doing that instead we'll use a cookie where we will store the ID of the session.


Now obviously you can still change that and assume a different ID if you want to
but that will not work like this because actually the value we store will not be
the ID but the hashed ID, hashed with a certain algorithm where only the server
can confirm that it has not been fiddled with so that you didn't play around
with it and tried to create a different one. 

So this will be a secure way because you basically store the ID in an encrypted
way where only the server is able to confirm that the stored cookie value
relates to a certain ID in the database and therefore we got a safe value stored
in the cookie which you can't, you can change it but you will not assume a
different session, a session can be matched and that session can then contain
the confidential data which you can't change from inside the browser, that is
the idea here. 

So sessions are stored on the server side, cookies client side, sessions server
side. 

Now let me show you how to implement a session. 

---