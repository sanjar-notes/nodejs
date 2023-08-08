## 251. What is Authentication?

<strong><em>no description</em></strong>

So what is authentication? 

Well we obviously got our user using our application, interacting with our views
and we get the server and also the database with which our server works, these
are all things we worked with in this course already. 

Now in our application, we might have different routes, different actions a user
can do, we might be able to view all products, to create and manage products or
to place orders, now obviously we can do more things in our application but
these are just some examples. 

Now the idea behind authentication is that not all these actions are available
to every user of our application and now here's one important thing, with user I
don't mean logged in user, I mean simply a person visiting our page, visiting
localhost 3000 in our case here, later of course the domain under which we
deployed it. 

So I'm not talking about logged in users but really just people using our page
and such anonymous users who are not logged in should not be able to do all
these things, they certainly should be able to view all products just as you are
able to view all products on Amazon.com even if you're not logged in, we want to
allow this in our shop too. 

But there are other things like for example here creating products, managing
products and placing orders which should only be available to logged in users
and not to every visitor of our page because in order to buy a product, you need
to be logged in and in order to create a new product, you also need to be logged
in because in our application, we of course connect a product to the logged in
user, we match the two things and this is what we need authentication for. 

We need to be able to differentiate between anonymous users who are not logged
in and logged in users and we need to provide a flow, a view and the backend
logic that allows people visiting our page to sign up and then to sign in and
then we can use sessions as I showed it to you in the last module to store the
information whether a user is signed in and well let him interact with the page
across requests. 

This is the idea behind authentication, now how is it implemented? 

---