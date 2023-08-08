## 181. Creating the Database Connection

<strong><em>no description</em></strong>

We connected to mongodb and this is nice but it also means that we can't do
anything else right now, the rest of the app is not working anymore and of
course it should work. 

So let's get there step by step and let's start by re-adding the admin routes,
so let's add this middleware again and for this, I also need to import admin
routes again and if we now have a look into our admin controller, here we do of
course use the product model, in the product model if we have a look into that
does rely on sequelize of course because we define the product model with the
help of sequelize. 

Now that is all something which we won't do anymore instead we now want to use
mongodb. 

So to get there, I will remove these two imports up there and instead in here, I
want to create a new class again because I'll create my own model again and this
is something we did before already in the pure MySQL module. 

So I'll create a product class here, like this and of course I will also export
this, so module exports will still be my class here. 

Now in that class, I'll have a constructor and in that constructor here, I want
to store the title, price, image url and description of the product when it gets
created. 

So here I will simply get the title, the price, the description and the image
url and then in the constructor I'll say this title equals title, this price
equals price, this description equals description, well and so on, you know the
game, so here image url equals image url. 

Now we can create a new product in javascript, a new object which follows this
form and now to save it in the database, I will also add a save method here, so
a function which can be executed on this class and in here, I now want to
connect to mongodb and save my product. 

Now to do that, to be able to connect, I'll need to import mongodb or mongo
connect, so I'll import mongo connect from my utility folder and there from the
database file. 

So I will simply import that method, the function I created here where you pass
a callback to, where we do connect to mongodb inside and then we basically
execute the callback and return the connected client so that we can interact
with it. 

However if we would do this, we would have to connect to mongodb for every
operation we do and we would not even disconnect thereafter, so this is not
really a good way of connecting to mongodb since we will want to connect and
interact with it from different places in our app. 

So it would be better if we could manage one connection in our database and then
simply return access to the client which we set up once from there or to the
different place in our app that need access. 

And to do that, I'll tune my set up here a bit. 

Let's tune it together in the next lecture. 

---