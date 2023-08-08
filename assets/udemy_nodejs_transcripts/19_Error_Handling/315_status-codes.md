## 315. Status Codes

<strong><em>no description</em></strong>

Now there's one thing which I also want to cover in this module and that are the
http status codes, which codes do we have and why do we use them? 

Let me first of all start with what the codes are therefore. 

The codes are simply extra information we pass to the browser which helps the
browser understand if an operation succeeded or not. 

If you're writing an application with a lot of client side javascript or a
mobile app and you will fetch only data instead of complete html pages,
something we'll do in the rest module later, status codes also allow you to
understand if an error happened, which kind of error because you typically map
certain kinds of errors to certain kinds of status codes. 

For example you have 200 status codes, most importantly 200 and 201, these are
always success status codes, they indicate that the operation simply succeeded. 

You have 300 status codes which simply indicates that a redirection happened. 

You have 400 status codes which show you that something happened because an
error was done by the client, for example incorrect data was entered into a
form, well then we return this 422 error code if you remember correctly and we
have 500 status codes which indicate that a server side error occurred. 

Now here are some examples, you can find a full, a link with a full list in the
lecture after this one. 

For success cases we have 200 and 201, the difference is that we use 201
typically when we created a resource on the server, so in the database, it's not
a must but it's a pattern you can use and you see often. 

300 like 301 simply is a code that is used in combination with redirection to
inform us whether for example this resource moved permanently or just temporary
thing, whatever. 

The 400 codes, there we have 401 if we are not authenticated, 403 which you
could translate with not authorized so you might be authenticated but you were
still not allowed to do that specific operation, 404 for a page that's not
found, 422 which we often use for invalid input and a couple of other error
codes and for 500, the most common one is 500 which indicates hey there was a
server side error but you got also other codes for timeout and so on, again in
the next lecture you find a full list. 

Now let's quickly scan through our code. 

If we have a look at our code, let's start with the admin controller, we rarely
set a status code. 

The default then always is 200 which is fine for this case but for creating a
new product, it would be better if we not just render 422 when validation fails
which is correct but that when we succeeded, we also return 201. 

The thing just as if we succeeded, we redirect which will use a 300 code but
later when we dive into creating restful APIs which is a different kind of node
app where we don't return html but just data, there you will see the 201 code
coming back, here it doesn't really make sense. 

Now forget added product again, we're fine with 200 and we're fine with 200
here. 

If we did fetch data and we do load the page and if we try to save or update a
product, then we get our validation error with 422 and if we succeed or in all
cases here, we redirect which again will use 300 automatically. 

So all these codes here are pretty fine, pretty decent, one of the most
important things, we're in good practice at least is that we do use 422 for
validating. 

Now we also have isAuth.js where I do redirect when we are trying to do
something where I'm not logged in. 

Now again since I'm redirecting, I'm sending a 300 status code but of course we
could add status 401 here to kind of also make clear what the problem is but it
will be overwritten with a 300 code due to redirect,  so it does not make a lot
of sense and that is fine here. 

Later again when we have a restful API where we don't redirect because we don't
route around on the server, then we'll use that 400 code. 

And for that reason that we now most of the time redirect or directly render a
page, we don't set that many status codes here, we'll see them later again as I
mentioned and we see some codes at least, also in error.js where I set 404 and
500. 

And these status codes not mean that our app crashes, that's important to
understand, instead if I do enter some invalid route here, I do get page not
found and if we open the chrome developer tools with the network tab and I
reload, we see that here, this 404 code can be seen, it's also marked as read
because chrome is intelligent and detects that anything which is not a 200 or
300 code is an error but error does not mean that it crashes. 

This still renders a valid page in the end, we just pass that extra information
of hey here's the page but you see that page because something went wrong and
chrome knows this too, for example tell us in the developer tools and later when
we create that restful API I referring to, we'll also benefit from that because
there we do have a more direct interaction with our requests because we don't
render new pages all the time and then we can get useful information out of
these status codes. 

So that is http status codes and how they are related with errors, your key
takeaway is a status code does not mean that the request failed or that the app
crashed. 

We had some problem and now we're returning information with the problem to the
client and that is also a way of gracefully handling errors. 

---