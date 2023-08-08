## 298. Keeping User Input

<strong><em>no description</em></strong>

Now that we learned a bit about how we can validate user input before handling
it, let's also work on the user experience side of things because right now when
signing up for example, let's say you enter an e-mail address and you enter a
password but the passwords don't match or the e-mail is already taken, then we
give you that error message which is great but of course all the input is lost
and that is a horrible user experience. 

So typically we want to keep the input, we want to keep the data the user
entered and that is exactly what I want to work on next, keeping that data
around. 

Now how can we do that? 

Well for that, let's go to these controller actions where we do handle sign up
and sign in  and let's maybe start with signing users in. 

There we do return this page when we enter incorrect data and we send that
status code, this error message. 

By the way we should of course also do that for logging in now that I see that I
forgot that, status 422 should be added here too but in the end what matters
here is that we render that view and we include the error message but of course
to keep the data the user entered, we should send this data back as well. 

So what we can do here is we can send maybe old input key here, whatever you
want and that could be an object and this object could hold the email and the
password. 

So I have two key value pairs here where I essentially store the email and the
password which I retrieved from the incoming request and I send that back to the
page we render when we render it due to this error so that I can render it on
the page and output it there because what this allows me to do is I can now go
to my sign up page and by the way, I should also output confirm password which
you can retrieve from request body, confirm password here in the sign up route,
so this is another field that we enter so we should return it. 

And now when we have the invalid input, we get these values back in our view and
so now if I go to my signup.ejs file, we can basically output that data there. 

So for example for the e-mail input, we can add the value attribute which html
supports and we can output our data there, so we can use this ejs syntax to
pre-populate this with some data and the data here would be old input.email. 

If we do that and we save everything and I reload the sign up page, I get an
error though and the reason is that when I visit this for the first time through
my get sign up action, I don't render the old input, so here when I render the
sign up page I don't have old input, so what I should do instead is there we can
also pass our data out with email being equal to an empty string, the same for
password and for confirm password, so that I enter empty values for these fields
when we load it for the first time and I enter the old input for the case that
we have that validation error. 

And with that if I now reload sign up, this works and if I now do enter
something here which is incorrect for some reason, then you see that it kept the
old e-mail because we return that with the response and we then output it in our
view and of course we should do the same for password and confirm password. 

So for password I output old input.password and for confirm password, it is old
input.confirm password, so I'm outputting that through ejs syntax. 

And therefore now when I enter something invalid again, now we still get that
error message but we kept our old data which is a much better user experience of
course. 

---