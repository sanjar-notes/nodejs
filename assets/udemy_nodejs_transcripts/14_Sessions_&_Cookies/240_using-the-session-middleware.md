## 240. Using the Session Middleware

<strong><em>no description</em></strong>

So we added the session middleware, let's now start our server again and let's
use the session middleware and how do we use it? 

Well we can use it in our auth controller in login instead of setting that
cookie, we can reach out to request and then the session object, this is added
by the session middleware, this session object and here we can add any key we
want, for example is logged in but you can name this however you want and set
this to true. 

Now if you save that and you go back to your browser, go to the login page
maybe, reload and get rid of that logged in cookie, you can simply delete it
here. 

Now click login and what you should see is that a new cookie was added here,
this connect SID for a session id cookie, if you expand the value here, you'll
see some strange string and that is what I meant, this is this encrypted value
so to say. 

And this is now the cookie, by default it's a session cookie so it will expire
when you close the browser. 

It's a session cookie that will identify your user here, your running instance
of this website you could say where you are browsing around, this will identify
you to the server and to this session and I can prove this to you. 

If we now go to the get login page here and I console log requests session here
like that, let me then go back and click on the login page here again and go
back to our server and there you see the session object is logged. 

Now let me also output is logged in here by accessing that, go back, login
again, it's undefined because I added the this code only after submitting this
for the first time, so let me save this again and now simply click that login
button here again and now you will see if you go back to the login page, you see
true here because now indeed in the session is logged in is stored. 

And we can go to a different page and come back to login and these are all
individual requests which technically are totally individual from each other,
totally separated and still we see true here because we still store this in the
session on the server side by default, just in the memory not in the database
yet and the session is identified for this browser because we have that cookie. 

And I can prove that to you by starting another browser and this will
technically be treated as a totally different session and environment, could be
a totally different machine. 

So I am on localhost 3000 here and if I click on login here, you see undefined
and that undefined is coming from the login request I just sent because this
browser, this user, technically this is a totally different user even though I'm
the same but it's a different browser, different user, this user does not have
this cookie set for him, does not have an active session on the server. 

And this is how we can store data that persists across requests as you saw, I
clicked around and still that was sent, the true value was sent when I came back
to log in, so this is saved across requests but not across users, as you can see
this is a different user, I go to login, I have undefined down there and that is
the power of using a session. 

It still needs a cookie to identify the user but the sensitive information is
stored on the server, we can't modify it and that of course will be super
important for authentication and what we see here already is the core mechanism
behind authenticating users in the web. 

There are other techniques too, for example when building a rest API, something
I'll come back later but this is a core thing on how authentication generally
works especially when rendering views as we are doing it with ejs and this is
what we will build up on in the authentication section where we then also dive
into things like validating credentials, logging users out and fun stuff like
that. 

---