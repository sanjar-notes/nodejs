## 290. Why Should We Use Validation?

<strong><em>no description</em></strong>

So why would we want to add some data or input validation to our application? 

Well if we have a user interacting with our website, then we typically have a
lot of forms on any web application we build. 

In our example project for example, we have a form for signing up, we got one
for signing in and we got one for adding products and the bigger your
application is, the more data you will need from your users at some point of
time. 

So we have that form with which our user, our visitor of the website interacts
with. 

Now in the end when this form is submitted with a post request as we controlled
it in our form, then a request is sent to our backend and by the way you could
also configure it to send a get request but the key thing here is a request with
the form data is sent and we're already doing this in this course because this
is a crucial task in any web application. 

Now on our backend so our nodejs code, we then typically interact with a
database or maybe we write the data into a normal file but in the end we take
that data which we receive and we want to store it. 

Now this is exactly the part which can be dangerous or problematic though. 

Right now in the app we got no kind of data validation, so if a user in our
current application would try to login with something that is not a valid email
address, we would allow that, we're not preventing the user from entering
something incorrect. 

The same is true for adding a product, we don't care about what the user enters
and this is what I want to change in this module. 

We'll add some validation as an extra step right at the start of our nodejs code
so right at the start when we handled a request on the server, definitely before
we store it in a database. 

And this validation can then either succeed and allow the data to be written to
the database or to a file or allow it to be handled by the rest of our node code
or we reject the input and then basically return some information to the user
prompting the user to correct the error. 

So this is what we will work on in this module and I will show you how to
validate and how to provide a good user experience. 

---