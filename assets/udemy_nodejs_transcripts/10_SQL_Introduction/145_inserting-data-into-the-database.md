## 145. Inserting Data Into the Database

<strong><em>no description</em></strong>

Adding products is also very simple. 

We got our admin.js controller where we do interact with the product in the way
of creating it, here post add product, we create a new product and call save and
I essentially want to leave that code as it is with one tiny change. 

So first of all, we have to go to the product.js file in the models folder and
there, the save method is not doing anything at the moment. 

Now what it should do is it should reach out to the database and save the data
there, so again I'll use my db constant, the one up here which gives me access
to my database pool, to my connection pool and I'll call execute to execute a
query. 

Now with SQL, we saw select for getting data, for inserting data there is the
insert into command and there, we then define the table where we want to insert
something and I'll use the products table here followed by brackets where we
list the different fields we want to insert value into. 

So we have the title, the price, the image url and the description and
important, you need to make sure that the fields you define here match the field
names you defined in your table, in the database, you don't need to specify the
ID because that should be generated automatically by the database engine. 

Now we're not done, this only defines where do we want to insert something, the
what is missing, we now need the values keyword followed by brackets with the
values. 

Now to safely insert values and not face the issue of SQL injection which is an
attack pattern where users can insert special data into your input fields in
your webpage that runs as SQL queries, we should use an approach where we just
use question marks, one for each of the fields we insert data into separated
with commas and then there is a second argument we pass to execute with the
values that will be injected instead of these question marks, so the order of
the elements we add here to this array is the order of arguments here. 

And we don't do this on our own because this MySQL package we're using here will
then safely escape our input values to basically parse it for a hidden SQL
commands and remove them, so now this is an extra security layer. 

And here I want to insert this title because the first question mark will be
inserted as a value for title, so the first element here should be the title,
second one will be the price, so here we should have this price followed by this
image url and this description. 

This allows me to insert elements there and again I will simply return the
promise that execute yields. 

That allows us to go back to the admin.js file, to the controller and on save, I
can then add then and catch again, in catch I'll just log the error but in then,
I don't care so much about the result, I just want to make sure that I only
redirect inside this function, so only redirect once the insert completed. 

Now with that, we can save all our files and if we now try to insert a second
product with some dummy url which of course will not work, 9.99 and some
description and we click add product here, we are redirected and this is looking
pretty good and if we have a look at our database and click that refresh button
here, we see our entry, so our new entry with an auto-generated ID. 

So this is working, we now are able to also insert data into our database. 

Now as a next step, let's make sure we can click the details icon here and
therefore retrieve data for a single document or a single entry in our database.


---