## 269. Wrap Up

<strong><em>no description</em></strong>

So that's it for this module. 

I'll actually dive into some other authentication related things in the next
modules, for example we'll add password resetting but these are the basic things
you need to know about authentication. 

You learned what authentication means, that it means that not every visitor of
your page can view and do everything, that authentication has to happen on the
server side to ensure that users don't trick you into thinking they are
authenticated and that you therefore use sessions to store the authentication
status and that you can protect routes by checking that session controlled login
status right before the request reaches your controller action or the code in
general that is executed in a route. 

Now authentication obviously also is strongly tied to security and providing a
good user experience and therefore passwords should absolutely be stored in a
hashed form. 

If you store them in plain text, if your database gets compromised, the
attackers have full access to your user accounts. 

Additionally csrf attacks, cross-site request forgery attacks are a real issue
because your session can be stolen there so to say and therefore you should
implement csrf protection as shown in this module in any production ready app
you're planning to ship. 

Now for a better user experience, you can look into flashing data or messages as
we did it in this module into your session store, flashing means that this data
will be removed from the session automatically by the package we used once we
used the data and we can use that data to persist data across redirects because
redirects technically trigger two different requests or we have the old request
we redirect and then a new request starts and if we want to share data across
request as you learned, we need to use a session. 

So these are the general authentication related things you need and with this
knowledge, you already get very very far. 

Now in the next module, we'll have a look at how we can send mails from inside
our node application because we'll need that feature to then enhance our
application a little bit regarding the authentication so that we can also add a
password resetting mechanism. 

We'll do this in the module thereafter but in the next module, let's first of
all have a look at how we send mails. 

---