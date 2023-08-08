## 235. Setting a Cookie

<strong><em>no description</em></strong>

So we found out that using a request for storing this is not ideal because the
request is dead after sending a response, which alternatives do we have? 

Well one alternative would be some kind of global variable. 

You could use a global variable which you store in an extra file and which you
export from that file and which you then change and that variable would actually
survive your request cycles but since that variable would be shared across all
requests, it would also be shared across all users and that is exactly where
cookies can help us. 

With cookies we can store data in the browser of a single user and store data in
that browser which is customized to that user which does not affect all the
other users but can be sent with requests to tell us hey I already am
authenticated and that is exactly what we will do here. 

So instead of just redirecting here, what we can do is we can set a cookie and
we set such a cookie simply by setting a header. 

So we set a header on our response and we set a header here by first of all
defining the name of the header and the name is set cookie indeed, that is a
reserved name which well sets a cookie and then you have the value of that
header and the value for set cookie in its simplest form is simply a key value
pair where you define any name you want and any value you want. 

So you could have something like logged in or logged in, makes it easier to read
equals true, this would set a cookie and I can show this to you. 

If you now save this and you go to the login page and you click post here or
click login, open your developer tools and in the chrome developer tools, you
can go to the application tab and there to cookies and if you expand this, you
should see your current address here and if you click on that, you will see some
cookies. 

Now some cookies will be set by third party plugins, chrome extensions and so on
but you will also see logged in and the value true, you should see that at least
and that is the cookie we just set. 

Let me zoom out a bit here, there you see the domain to which it belongs, the
path, when it will expire and this state is in the past because it's a so-called
session cookie, it will basically expire once you close the browser and come
back, you see the size and some other information to which I will come back in a
second. 

So this cookie is now set and now this cookie is not only set but the browser by
default sends it to the server with every request we make, so if I click on
products here for example, we go to the network tab, this is the request which
was sent to the products page and there if we have a look at the headers and we
scroll down to the request headers, you see that a cookie was sent. 

The first one comes from an extension but here this is our cookie, so it was
sent to our server and now since we have that, every request will have that
cookie attached to itself and therefore this data is sent with every request and
now we can use that. 

Let's start simple, let's say in the get login page here. 

We can have a look at our headers, let me console log request get and then you
enter the header name which is cookie because remember in the client side dev
tools, you saw that the cookie header was sent with the request and now if you
go to the login page or reload that page if you are on it, I reloaded it a
couple of times, you see this output. 

Now we can ignore the first cookie but this is our logged in cookie and now we
could extract that value for example by splitting on the semi-colon and then
taking the second value in that array, the array index starts at zero so one
gives us the second element and now if I reload this, you see I get logged in
true here, you could trim that to remove any excess white spaces, we could split
this again on the equal sign, this is obviously a very complex way but if I do
this again and then I use the second value, then I should get the true or false
value. 

So now if I reload this, I get true here, so obviously this is a very complex
way but should be quite readable and then I can extract my is logged in
information from the incoming request header, I'm getting the cookie header, I
make sure that I get the second cookie that is sent which happens to be our is
logged in cookie. 

If you only have one cookie being sent by the way, then make sure you extract
the first value, so whatever or wherever is logged in is located for you, if you
only have one cookie, use the first one with zero, if you've got multiple ones,
use the third one and so on and then I extract the true value and now I have
that is logged in information which I can pass to isAuthenticated. 

And with that on that page, if I now reload it, hey here are our two options in
the menu because now we do enable that again because now we store that
information across requests. 

So now even if I navigate away to another page or I don't extract that cookie 
yet and I come back to login, there I do extract it and it is always sent with
every request, so it is a cross request data storage. 

Still there is a big disadvantage and do you know which one that is? 

---