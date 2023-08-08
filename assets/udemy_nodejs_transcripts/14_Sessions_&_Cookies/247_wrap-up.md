## 247. Wrap Up

<strong><em>no description</em></strong>

That's it for this module. 

You learned a lot about cookies and sessions. 

Now about cookies, they're great for storing data on the client side, so in the
browser and since they're stored there, you should not store sensitive data in
cookies because they can be viewed by the user, that might not be the worst part
because each user can only view his own cookies but they can also be manipulated
and you don't want to let your users control whether they are authenticated or
not by simply switching some cookie value. 

Now you can configure cookies in a broad variety and often you won't do that, at
least not directly by setting that header instead you'll use something like the
session package which also uses a cookie but more on that in a second but you
can configure them, for example to expire. 

By default they will expire when the browser is closed and such cookies that
expire when the browser is closed are called session cookies. 

Now this term can be confusing, session cookies are not cookies necessarily used
to identify a session, a concept to which I'll come back in a second, they're
just called session cookie because they only survive as long as you are using
that page in the current browser. 

You can also set an expiry date or an age after which the cookie will get
invalid and that is thing called a permanent cookie, it's not permanent in the
sense of lives infinitely long but in a sense of it does not necessarily go away
when you close the browser, it will still be there when you reopen the browser,
it will be invalid deleted once it expired. 

Now cookies work well together with sessions but they're not limited to using
with sessions, keep that tracking cookie in mind as an example. 

Sessions are another great concept, you use them to store data on a server not
on the client and therefore since they're on the server and they can't be viewed
or manipulated by your users, they are great for storing sensitive data that
should survive across requests because that's important too. 

You could store data in requests as we did it earlier in this course but then
the data is lost for every new request, with sessions the data survives. 

Now you store anything in sessions, you could store your shopping cart there but
often you use them for authenticating users, for storing user data in there or
the authentication status in general. 

Now a session needs a cookie to be identified and that's not the session cookie
which is simply a cookie that dies after you close the browser, you can use a
session or a permanent cookie for that actually and on express session, the
package we used which sets the cookie automatically by the way there, there if
you remember you could configure the cookie when registering the session
middleware. 

So we're not talking about that here instead you just have a cookie that is used
to identify a session and that is important because otherwise you have that data
on your server, that is great but how do you know to which user it belongs? 

Well for that you need the cookie. 

This is how sessions work and how to use cookies and since the session is also
stored on the server, you can choose from different storages, you could use a
MySQL storage, you could use file storage or as we did it here, you could use
mongodb to store your session data. 

So these are sessions and cookies, crucial concepts which you might not always
control and use directly but often indirectly, for example with authentication,
something which we will come back to the next module where we will implement a
real authentication workflow with sign up, logging in, logging out, storing real
user data, creating users and all that fun stuff. 

---