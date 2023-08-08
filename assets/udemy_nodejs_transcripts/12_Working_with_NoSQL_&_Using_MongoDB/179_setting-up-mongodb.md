## 179. Setting Up MongoDB

<strong><em>no description</em></strong>

Now that you had a brief introduction to what mongodb is and what NoSQL
databases are, let's install mongodb, . 

let's set it up and let's use it for our project here. 

Now to install mongodb, you can either do that locally on mongodb.com, you can
click on get mongodb, download the installer or the tools when you click on
community server here and follow the installation instructions and this will all
work and it will give you a locally running mongodb server. 

Now I would go for a cloud solution here because it's the more realistic
environment we would use for deployment anyways and it's really easy to set up
and it's free and that will be Atlas, so mongodb Atlas. 

So I got here by clicking on get mongodb and then choosing atlas. 

Now again this is free, you don't need a credit card or anything like that, you
just need to sign up and you can spin up your own in the cloud best practice
managed mongodb server which is a great environment for practicing because this
will follow all the best practices. 

So sign up here, now once you did sign up you should end up on a page that looks
something like this. 

Maybe you need to create a new project first, give it any name you want and then
you should be on that page or you can build a new cluster, you might also end up
in that wizard right from the start. 

Now here you configure a mongodb cloud cluster, so basically a mongodb server
and therefore a mongodb database or multiple databases, as many as you want
running in the server. 

You can generally leave all the default settings, make sure that you choose a
region where a free tier is available, behind the scenes mongodb uses one of
these cloud providers but you don't need to be signed up with them or anything
like that, so you can choose anything you want here, then you choose the cluster
tier and there you should use the free one and zero where it says free and then
this will not cost you anything. 

Under additional settings, you can well leave all the defaults, you can't change
them anyways in the free tier but that's fine. 

You can change the cluster name if you want and then you can click create
cluster and this will now create a new cluster, we'll take a couple of minutes
which you then can connect to later and which you then can use as your backend. 

Now one important note, you might see that I have some cost here in this account
and this is not coming from the setup I'm showing you here, I was simply using
this for some other set up in the past which did cost something, this does not
cost you anything. 

Now whilst this is getting set up, you can already click on security here and
there you will probably not have as many users as I do. 

Now make sure you add at least one new user and I already did this which and
that's important, which has read and write access to any database. 

You can turn it into an atlas admin but more realistic is this here because this
will later be the role which our nodejs application assumes which should be able
to read and write our databases but not to administrate them because we'll not
do database administration through nodejs, that would be something our database
admin does and therefore not our app. 

So make sure you create such a user, you can also sign your own password or
auto-generate a secure one, make sure you do save that because you'll need it
later and then also make sure you have a look at IP whitelist. 

There you see all the IP addresses that are allowed to connect to your mongodb
server, now I already got a bunch here that will probably be less for you. 

Now one thing you should do here is you should add a new IP address and add your
current IP address since the node app runs locally on your machine, your node
app will have this IP address. 

Later when you deploy the node app this should of course use the IP address of
your server where you deployed it to but here you can use your local one so that
you can connect and your node app can connect to that server. 

That's of course a good security feature because this makes sure that no
unauthorised access can happen to your database, so your database is now locked
down both from a IP perspective but also from a user perspective. 

And now we can wait for it to set up to finish and I'll be back once it did
finish. 

Now the set up did complete and now we can connect to our mongodb server from
inside our node app and for this we can click on connect here and choose a
connection method which in our case will be an application. 

Now here we can check I'm using this driver and we get this url which we'll need
soon but first of all we need to install the mongodb driver, in our case for
nodejs. 

You can click on an example down there but I will simply show it to you in our
project. 

---