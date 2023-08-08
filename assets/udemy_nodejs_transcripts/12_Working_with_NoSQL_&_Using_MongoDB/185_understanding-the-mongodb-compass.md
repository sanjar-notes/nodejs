## 185. Understanding the MongoDB Compass

<strong><em>no description</em></strong>

Now in the last lecture, we did insert a product into our mongodb database which
is awesome. 

Now I also want to see it and before we actually fetch it in our node
application, let me show you another tool called compass. 

If you click on get mongodb on mongodb.com, you can choose that and you can
download and install it for free as well. 

It's available for Windows, MacOS and Linux and once you get that installed, you
can start your compass application on your machine and this essentially is a
tool that gives you a graphical user interface to connect to your database and
to interact with it. 

So let's wait for it starting up here and once it did start up, you can connect
to it. 

Now to connect to it, let's go back to our mongodb cluster and click connect
here and then click connect with mongodb Atlas, choose your operating system and
then copy that url down there. 

Now one cool thing is if you now quickly close compass again and you restart it
after you copied that url, it should tell you that it detected a connection
string and if you click yes, it will insert the most important pieces here for
you. 

Now you still need to choose how you want to connect, so make sure your username
is correct and also enter the password for this user, you need to do this
manually. 

All the defaults can be left as they are and you should be able to now connect
to your database and here it is and interesting enough, you are to be precise,
you are now connected to the database server and here you see a couple of
databases, two default ones which you don't need to touch and which you
shouldn't touch but then also your own one, shop. 

And the shop database here actually has a products collection as you can see and
if we look into that products collection, in there we can see the documents that
are stored in there and here is that one document we inserted, so it is one
product we added in the last lecture. 

Now you can also insert documents and edit them inside of compass and check out
the official compass docs to learn all about the features you can use here. 

I just want to use this as a nice visual support so that we can see our data
before we fetch it in our node app. 

That being said obviously the data is not that useful to us here, so let's go
back to nodejs and write some code so that we can use the product data on our
shop pages again which we commented out at the moment. 

---