## 449. Deploying Different Kinds of Apps

<strong><em>no description</em></strong>

Now obviously in this course we built a couple of different applications, to be
precise we built an application with server side rendered views and that
includes the possibility to return just html pages or as we did it, to use a
templating engine like ejs and obviously we build two APIs, . 

we built a rest API and a grapghql API. 

Now how do we deploy these two types of applications, one with views and one
without views? 

First of all we have to keep in mind that how the application behaves, what it
does with incoming requests and which data it accepts and returns, this is all
our logic, this is all code we wrote. 

In the end when we look at it from a technical perspective, in both kinds of
applications, we start a normal node server and we use a node framework, in this
case the most popular one, express and therefore these types of applications
have the same hosting requirements. 

We don't have to make a difference here because in the end when we move our code
to a web server, then there we also just want to do the exact same thing we did
locally. 

We'll start our node server and wait for incoming requests and therefore we
don't have to differentiate between these kinds of applications, when it comes
to deployment we simply deploy our code, start the node server and we are good
to go. 

---