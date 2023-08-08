## 458. Using a Hosting Provider

<strong><em>no description</em></strong>

Now that we learned a lot about how we prepare for deployment, let's finally
deploy and for that, I will use a hosting provider called heroku, you can simply
google for it, you can get started with it for free, it's a very popular one but
let me also say that there are dozens, hundreds, thousands of hosting providers
you could use and it's impossible to cover them all, so I will try my best to
show you the general steps of deployment and to explain how it works in general.


So heroku is what I will use here and I will show you how to deploy to heroku in
detail, I already created an account, you can do that by simply signing up,
again that is free but first of all let me explain what heroku is and how we
generally work with these hosting providers because we use a hosting provider
here, heroku is a hosting provider. 

The alternative always is that you build your own computer and you set it up
such that it is connected to the Internet, that you expose the right ports and
that people can send requests to your computer which might be running in your
room and that is not a solution I recommend unless you really know what you are
doing otherwise it's very likely to be insecure, not scalable at all, if your
app is doing really well then you will quickly need a new computer, a second
computer, a third computer and it only gets more complex and expensive and
therefore, we typically use hosting providers like heroku but also like AWS for
example. 

There we take our code and we deploy it onto managed spaces on their computers,
also often called virtual servers and this means that these providers have very
large and powerful machines in their data centers and you typically don't rent
an entire machine, though you could do that but a part on that machine, so a
part of the hard drive and some resources which are then provisioned for your
managed space and your code runs totally separated from the other apps which
might be running on the same computer on the same server, your app runs
separated from them and now you of course want to connect your app running on
that virtual server with your users. 

Now typically you don't directly connect your space on that machine to your
servers, though that is also possible on some providers but instead a lot of
providers manage a lot of the heavy lifting for you and they give you their own
managed servers you could say in front of your server where you can conveniently
add ssl encryption, compression, logging or load balancing which means that when
you have multiple virtual servers because your app is doing really doing well
and you need more resources, that in such a case incoming requests are sent to
servers with available capacities in an efficient way. 

So that is all handled by so-called managed servers which are typically
invisible to you which you don't configure but which are part of the hosting
provider package you could say and you just use a nice user interface provided
by the hosting provider to set up how your app behaves regarding ssl or
regarding logging and so on. 

Now this all runs in a private network which means that your own virtual server
and your code is not directly exposed to the web but it's exposed to that
managed server which then in turn talks to the web and therefore to your users
through a public server gateway and that essentially is like a door where
requests can come in there and then forwarded to your server, to your virtual
server and the responses are also forwarded. 

So this is how this works, this is how most hosting providers work, that is what
happens behind the scenes, just important for you to know, not really a lot of
stuff you have to do on that. 

Now that is the behind the scenes stuff, now let me show you how heroku works
and how we can deploy with it and of course that's just one example, you can use
any hosting provider you want for your application. 

The general way of deploying your code does not really change. 

---