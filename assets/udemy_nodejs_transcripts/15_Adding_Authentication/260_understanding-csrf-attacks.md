## 260. Understanding CSRF Attacks

<strong><em>no description</em></strong>

Now that we have our authentication flow and route protection in place, let's
talk about security and there, about csrf attacks. 

Csrf stands for cross-site request forgery, now what is this? 

This is a special kind of attack pattern or approach where people can abuse your
sessions and trick users of your application to execute malicious code. 

This is how it works, you have a user in your application and now let's assume
this is a visitor who indeed is logged in, you have your server side code and
your database with which you interact. 

Now the user interacts with your frontend views, so the pages you render back
and you get a session for that user and of course the cookie that belongs to
that session, so everything you knows. 

Now the user can do intended things like for example send money to B, if you are
building a banking app or in our application, order some products with his own
shipping address if we had such a checkout process. 

Now in a csrf attack scenario, your user is tricked onto a fake site and this
can be done for example by sending a link in an e-mail, that site can look like
your own page but it technically is a different one. 

Now on that site, there could be a link leading to your page, to your real page
executing some request there, of course you could include a form for example
which sends a post request to your page, so to your own node server where you
added some fields to send money to another person, to C in this case instead of
B. 

To the user, this is pretty invisible because he saw a page that maybe looked
like your page or clicked on a link that instantly redirected to your page but
with behind the scenes some data being sent there that does something the user
would not want to do normally. 

Now why does it work? 

Well since you got valid session for that user if you send something to your
site, to your servers, your session is used for that user and therefore that
behind the scenes data that the user never sees that configures the money
transferal or the order in a certain way that is not ok to the user, this part
is invisible to the user but the valid session gets used for it because your
server is used and therefore this is accepted. 

This is an attack pattern where the session can be stolen so to say, where you
can abuse the fact the users are logged in and you can simply trick them into
making requests which they might not even notice and obviously we want to
protect against this attack pattern and how can we protect now? 

Well the idea is that we want to ensure that people can only use your session if
they are working with your views, so with the views rendered by your
application, so that the session is not available on any fake page that might
look like your page but that aren't your page. 

And to ensure this, to add this feature, we will use a so-called csrf token. 

Now let me show you how this works in the next lecture. 

---