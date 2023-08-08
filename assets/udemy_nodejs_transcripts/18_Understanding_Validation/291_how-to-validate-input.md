## 291. How to Validate Input?

<strong><em>no description</em></strong>

Now how do you validate user input? 

Well obviously we got our user entering some data into a form, we got our server
where we want to handle that and now we got a couple of places where we can add
validation. 

For example we can validate on the client side with the help of javascript, so
before any request is sent, we can write some javascript that for example
watches the inputs for key events, so for the user typing and then checks the
input whilst the user is working on the form and then you can display an error
because you can use javascript to change the dom at runtime, you can display an
error right in the browser before anything is sent to the server. 

Now this can greatly enhance your user experience and it is something which I
discuss in my dedicated javascript and javascript framework  courses like my
react course, my angular course and it's totally optional, that is important. 

It can definitely improve the user experience and therefore you might want to
consider using it but it is optional because since we use client side
javascript, so javascript code that runs in the browser, the user can see that
code, the user could change that code and the user can of course disable
javascript. 

So this is not a protection that secures you against incorrect data being sent
to your server, this is not a secure solution, it's only there to improve the
user experience because of course there you can validate and you can show a nice
error message and keep the old input so that the user doesn't have to re-enter
that email address where the @ sign was forgotten but it's only for a user
experience thing, it's not really secure. 

So your next option is to validate on the server side. 

Now this is what we'll focus on in this module and in this course because this
is of course what we do with nodejs. 

We have to do that because this code can't be seen or changed by the user, the
user can't disable us using that code because it happens on the server, not in
the browser and this is the crucial part where we have to add validation, where
we really have to filter out invalid values, so this is a must have, it's
absolutely required and it is what we'll focus on. 

And this then ensures that we only work with valid data in our node app and
ultimately if we do plan on storing it, that we do store correct data. 

Now also important, for some database engines and for most database engines
actually, like for example mongodb, there is also a built in validation which
you can turn on, I do cover that for the example in my mongodb course if you
want to learn more about that. 

It's also optional because this can be a last resort but if you have good server
side validation in place as you should have, then this might not be required
because there is not really a scenario where invalid data could reach your
database because you filter it out in that server side validation already ready.


No matter which approach you have if you validate on the server side and or in
the database, though or is not really an option you should validate on the
server side at all means but no matter what you choose, in the end this can of
course fail and then you should always return an error message, a helpful error
message if possible and never reload the page but always keep the data the user
already inserted because that of course is a horrible user experience which we
all know that you enter something incorrect and you get back hey this password
is not known or this e-mail address is unknown and you have to enter it all
again. 

So this is another part on which I'll focus in this module, that we provide a
good user experience. 

And with that we know how to do validation at least in theory, time to turn that
into practice. 

---