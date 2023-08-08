## 237. Configuring Cookies

<strong><em>no description</em></strong>

So we can manipulate cookies so storing sensitive data is not ideal but I
mentioned that for example for tracking users, it's a popular instrument and why
is that? 

Because as you can for example see with the cookies I have here, the cookies
don't only have to relate to your page. 

A cookie can also be sent to another page and that is a common instrument in
tracking where you have that so-called tracking pixel on pages which is simply
an image url with no real image but that image can be located on let's say
Google's servers and you have a cookie on that page which is also sent along
with that and therefore Google can track on which page you are and how you are
moving through the web even if you're not on their websites because some data is
stored in your client and obviously you could delete it therefore which is why
you can block such mechanisms too but it is stored there and it is sent with
every request to Google, so they can track you without you being on their
servers, so storing that information on their servers would not work but storing
it on your computer will work because obviously that can be sent on every page
you visit. 

So that is something where this could be interesting if you want to track your
users, that is a very common thing to do and you can also configure cookies. 

We set a value but actually you can set more things than just the value, here I
set my cookie by adding that key value pair. 

Now obviously we could add multiple cookies, multiple key value pairs, we can
also add a semi-colon after the key value pair and for example set expires to
some expiration date, this date would have to follow a certain format, the http
date format, I'll link it attached to this video here. 

So you could set a certain date when this cookie will expire because remember if
you don't set this, it will expire once you close your browser. 

Alternatively to expires, you can set max age written like this and this is a
number in seconds, how long that cookie should stay around, so we could set this
to 10 for example and now if I click that login button here, I got logged in and
now you see the expiry date also changed here, the expiry date if I decrease
that, the expiry date here basically is today and now it already is expired and
if I reload that page, is logged in is therefore gone. 

So this is something we can do and this is of course interesting if you want to
control for example how long you want to track a user or we will actually use
that together with authentication later, you could use this to also control how
long an authenticated session stays active for a user, you might know that from
your online bank where you timeout after a certain duration. 

You can also add a domain to which the cookies should be sent and here we again
are on that tracking thing again. 

You can add secure just like this without an equal sign, just secure, this means
this cookie will only be set if the page is served via https. 

Now I can't demonstrate this here because our local development server is not
using https but we will eventually use https later in the course where I will
show you how to set this up, so now you can already see however that I get an
error if I try to reload login because I try to extract the value which is not
there. 

So for now let's simply comment this out and set this always to false so that I
can just show you how this cookie is now not set, if I reload and I click here,
you don't see the cookie here because I added secure and it would only be set if
we are serving the page via https and you can also set this to http only. 

Now if I do that and I go back to login and I click here, it is set but now it
has this checkmark here in the http column and that means that now we can't
access the cookie value through client side javascript, so in the scripts
running in the browser. 

This can be an important security mechanism because it protects us against
cross-site scripting attacks now because now your client side javascript where
someone could have injected malicious code can't read your cookie values and
that will be important later with authentication where a cookie will not store
the sensitive information but an important part of authenticating the user. 

So this can be an extra security layer because now the cookie will still be
attached to every request that is sent to the server but you can't read the
cookie value from inside the browser javascript code. 

Obviously as you can tell, as a user in the developer tools, you can still read
it but then again it's your own cookie and you will not store information like
hey I'm logged in there because that would be easy to manipulate and you can't
protect against that. 

These are the key values you can set here and this gives you a lot of
flexibility. 

That being said, often you will not directly set your cookies because you rather
use some packages like for example for authentication that will manage setting
the cookie for you. 

And that is something which I'll dive into in the next lectures where we dive
into sessions, what sessions are, how they can help us with storing sensitive
information across requests and how cookies still are important when using
sessions. 

---