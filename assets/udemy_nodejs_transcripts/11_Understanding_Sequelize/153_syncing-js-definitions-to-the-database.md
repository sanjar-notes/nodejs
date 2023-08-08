## 153. Syncing JS Definitions to the Database

<strong><em>no description</em></strong>

We define the product model and I mentioned that we can now work with this model
to create new products and so on but for this, we of course also need a product
table in our database and there right now we got no tables because I deleted the
products table earlier in this module. 

I also mentioned that sequelize can create these tables for you and it indeed
can. 

Now to create tables for you, you just have to tell sequelize to do that and
I'll do that in the app.js file. 

In there I want to ensure that all my models are basically transferred into
tables or get a table that belongs to them whenever we start our application and
if the table already exists, it will of course not override it by default though
we can tell it to do so. 

Now in my app.js file which is the file execute when I do start my program, I
want to import from the database file as I did it before, I'll just rename it to
sequelize because I do import my sequelize object with a lower case s because
I'm importing from my own utility database set up file and then towards the end
of this file, let's say here, I want to call sequelize and then there's a
special method, the sync method. 

The sync method has a look at all the models you defined and keep in mind you
defined your models in your model files by calling sequelize defined on that
same sequelize object, so it is aware of all your models and it then basically
creates tables for them. 

That is what sync does,  it syncs your models to the database by creating the
appropriate tables and if you have them, relations. 

So here I will call sync and then I can listen to the result of this, let's see
what we get back as a response here or what we get back as a value here and we
can also of course catch potential errors that occurred and if an error occurred
here, well then we can essentially also log that and I only want to let's say
start my server if we somehow made it into then, let's see what this gives us. 

If I now run npm start here, it starts up and we see there is some log output. 

If you scroll up quite a bit because we got back a complex object, you see that
this is a default log thrown by sequelize, it executed this SQL query for us
without us writing this query. 

It created a table if it did not exist yet which it named product, products and
that is that automatically inferred name because we named our model product, it
automatically pluralizes that and then it assigned a couple of fields there
which it configured according to our model definition. 

And then this is the return value we get back, basically our sequelize object
you can tell and if I now quit this server with control c, clear the console and
rerun npm start, you'll see it runs this again but it does not overwrite the
existing table because we have that if not exists check in there automatically. 

So we can run this again without issues and our server starts up even if this
table already exists, we still make it into then. 

Now I will comment out that result log because I don't want to have this long
object every time, in the console every time we start this. 

So now I just get MySQL query here and if we now have a look at the workbench
and we right click on our database and click on refresh all, we see that under
tables, we get a products table and if we inspect that with this icon, we see
all the fields we defined and that is added by sequelize to new fields, created
at and updated at. 

So it automatically manages some timestamps for us, we could disable this but I
actually like this feature, so we get these automatically managed fields too. 

This is how we sync our tables to the database and what sequelize does for us,
and with that, we're now ready to use that. 

---