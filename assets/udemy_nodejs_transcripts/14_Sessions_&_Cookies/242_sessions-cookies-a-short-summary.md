## 242. Sessions & Cookies - A Short Summary

<strong><em>no description</em></strong>

So now we had a look at how we can use sessions and what the advantage of a
session is and we also of course learned about cookies, what a cookie can be
used for and how it plays together nicely with a session to identify a user, a
client and then store the sensitive data on the server, so in the session and
that difference between the sessions server side and cookies, client side is
really important to understand and you also learned how to set a cookie and how
to use a session. 

Now by the way if you're wondering how that session cookie, this cookie here,
how this is set, well this is done automatically by express session so by that
middleware we're configuring and that's also why you can add cookie related
configurations here because this middleware automatically sets a cookie for you
and it automatically reads the cookie value for you too, so it does all the
cookie parsing and setting for you. 

Now with that, you actually rarely need to manage cookies on your own because
that session cookie and with that I don't mean a cookie which gets lost after
you close the browser but that cookie that identifies a server side session,
that is the most prominent, the most common use case for cookies besides
advertisement, tracking which you typically don't implement on your own but you
use third party tools like Google for that. 

But that session cookie, so that session identifying cookie is an important
thing and sessions on the server are often used for authentication but as I
mentioned, you could use them for any kind of data you want to store. 

We happen to store the information whether the user is logged in but you could
be storing the carts, the shopping cart of the user here or anything which
belongs to a user which should be shared across requests as I highlighted. 

---