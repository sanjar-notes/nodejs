## 246. Two Tiny Improvements

<strong><em>no description</em></strong>

So we learned a lot about how we work with sessions and cookies and how we can
use it to store data and what potential issues are if we store mongoose model
data in there because we don't store the full mongoose model but only the data
but not the magic methods, so we have to recreate that mongoose model, we have
to re-fetch the data. 

Now one thing I just noticed is in the views, if I go to my product detail,
there this add to cart of course also should only be rendered if I am
authenticated, so I'll grab that link from product list and replace this here to
make sure this works correctly because previously, if I clicked on details even
though I'm not logged in, I did see my button there, now if I login and I go to
the, whoops, details I see it here, I don't see it if I'm logged out. 

Now one other thing you might notice is if you do login like this, you sometimes
might end up in a scenario where after logging in, the view didn't update
accordingly. 

Now I fail to reproduce this at the moment but you might see this, that you
login and still some items are missing and you need to reload the page to get
there. 

The reason for this is that in auth.js when I have post login here, I do set my
session and when I then redirect, when I send a response, the session middleware
goes ahead and creates that session and that means it writes it to mongodb
because we use the mongodb sessions store and it sets the cookie. 

Now the problem we can face here is writing that data to a database like mongodb
can take a couple of milliseconds or depending on your speed even a bit more
milliseconds. 

The redirect is fired independent from that though, so you might redirect too
early. 

Now to be sure that your session has been set, you can use request session here
and call the save method, you normally don't need to do that but you need to do
it in scenarios where you need to be sure that your session was created before
you continue because here, you can pass in a function that will be called once
you're done saving the session. 

You'll get an error here if an error exists, most of the time that should not be
the case and then in here, you can safely redirect and you can be sure that your
session has been created here. 

So now with that, if I log out and I login again here, now this will only
continue once that session has really been created. 

Normally you don't need to call that but you need to call it if you need that
guarantee which typically is the case when you do redirect for example because
in such scenarios, the redirect will be fired independent from the session being
saved and therefore the redirect might be finished and the new page might be
rendered before your session was updated on the server and in the database. 

That's something to keep in mind and that is why I wanted to show you this
method too. 

---