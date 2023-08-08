## 151. Connecting to the Database

<strong><em>no description</em></strong>

So back in the project, we first of all have to install sequelize and just as we
installed all the other packages, we'll do this by running npm install --save
because this also is a production dependency, it's a core dependency of our
project and then the name is sequelize, like this. 

Now important, sequelize needs that MySQL 2 package which we already installed,
so this MySQL 2 package we installed in the last module needs to be installed. 

If you skipped the last module or anything like that, make sure to also install
MySQL 2. 

Now with that, we got sequelize installed and now we can do a couple of cool
things with it. 

The first step always is that we create a model with sequelize, well and also
that we connect to the database of course. 

Now therefore the first step is that when I connect to MySQL database with the
workbench which we also used in the last module already and in there, I will go
into my node complete database and delete the products table by right clicking
on it, drop table and then simply click drop now, I do this because I now want
to use sequelize to manage my tables. 

With that let's go back to our project and now let's go into the database.js
file in the util folder, there I now want to write some code to connect
sequelize to the database. 

Now sequelize uses MySQL 2 behind the scenes, therefore sequelize behind the
scenes will do something like this but we won't write this. 

Instead we will import sequelize and I'll store it in a sequelize constant, you
can name this constant however you want but I'll name it with a capital S
cecause I actually import a constructor function or a class here so I'll import
sequelize like this and then I'll create a new sequelize instance by calling new
sequelize, like this. 

Now sequelize, here the constructor function needs some options. 

You can see we have to configure it with the database name with a username to
connect to it, a password. 

So here I will connect it to my database, so to my schema name which is
node-complete, node-complete with my root username which is root and with my
password which is nodecomplete in my case, use the root password you assigned. 

Now we can also pass a fourth argument, an options object and in there you can
see, I saw this menu or get this menu with control space, you can see we can set
up a bunch of stuff, for example the dialect, we can set this to MySQL to make
it clear that we connect to a MySQL database because different SQL engines or
databases use slightly different SQL syntax and you can dive into the official
sequelize docs to learn all about it, a link can be found in the last lecture of
this module. 

The one thing I want to set for now is the host, by default it would use
localhost so we don't need to set it but I will explicitly set this to
localhost. 

With that, we're creating a new sequelize object and it will automatically
connect to the database then or to be precise, it will set up a connection pool
just as we did it manually in the last course module. 

So I can now export my sequelize object here which is essentially that database
connection pool however managed by sequelize giving us a lot of useful features.


With that, we got the connection set up, let's now focus on working on the
models. 

---