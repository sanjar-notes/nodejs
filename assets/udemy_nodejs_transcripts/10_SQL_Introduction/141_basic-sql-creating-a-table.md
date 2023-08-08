## 141. Basic SQL & Creating a Table

<strong><em>no description</em></strong>

So let's finish that setup of the products table which I need for my first
little demo code. 

Here in the table editor so to say, in the workbench, we can define how a
product's entry should look like. 

For that we first of all define the name of a field, ID and the data type and
for the ID, an integer is fine. 

We can also check that it should be the primary key by which records in this
table will be identified, that it must not be null, that it should be unique,
that should definitely be the case, if it should hold binary data which is not
the case, if it's unsigned so if it holds no negative values which should also
be the case because that should be an integer starting at 1 and then
incrementing, here if it is zero fill and for us important, if it's
auto-incrementing and that should be the case because every new record should
receive that automatically and it should be a higher number than in the last
record. 

Now a product also typically has a title and there I'll use a var char which is
basically a string, I'll just define that it may be up to 255 characters long
and longer titles will simply be cut off, so that's something to keep in mind. 

It must also not be null, so we have to have a value in there but I don't need
any other setting here. 

For a product, I also want to have a price and here I want to have a double so
that we can enter decimal places, this must also not be null. 

I also want to have a description which now will not be a var char but will be
text and if you're wondering which data types are available, that is exactly
what I meant, you should definitely consult a full SQL course to learn more
about the available data types and how to work with them. 

So here I got my text which is simply a longer text than the var char which has
a limitation and I will have an image url which I'll also set to var char 255
which means longer urls also won't work. 

With that I defined how my product should look like, you can leave everything
else as it is and then on the bottom right, I then click on apply here. 

It shows you the SQL statement it will execute and you could execute this on
your own, for example in node of course to always create this new table, here
we'll do it in the workbench, so click apply, close and now on tables, you see
the new products table and if you click this icon here on the very right, you
can see the entries in there. 

By the way, you also see the SQL query that was executed to look into that and
that's pretty similar to the query we're executing here. 

So now that the table is set up, we just need to enter one dummy data so that we
have something to fetch and I will simply add a book here, whoops, with a price
of let's say 12.99, description this is an awesome book and also an image url. 

Now if you've got problems copying a value in here, you simply have to type it
manually, copying also didn't work for me, of course you can also enter some
dummy value and just live with no image being displayed. 

Now let's also enter an ID here though that should be auto-generated if you
don't do it, click on apply on the bottom right, apply here, close and now if
you again click on this icon here next to products and the left column, you'll
see that now this one element was added here. 

Now that we get a book in here, let's go back to our node code and there, we can
now chain then and now this is something provided by the fact that we're using
promise here when exporting the pool. 

We now get back promises when executing queries like this with execute and
promises have two functions, then and catch. 

Let's explore them in the next lecture. 

---