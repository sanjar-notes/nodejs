## 143. Fetching Products

<strong><em>no description</em></strong>

Now that we successfully connected our code to the SQL database, let's start
working on the project and for this, I'll remove this code in the app.js file
because this was just some testing code, not the real code we'll use, instead I
of course want to work on my models here, let's say on the product model. 

There we right now already have an exported class which we can instantiate and
where we then for example have a save method to create a new product. 

Now even though we're still fetching product from our file for now, we also have
our static methods for fetching data and there we fetch data from our files. 

Now we can do that but of course this is not really the set up I want to use. 

I will still work with static methods for fetching data but I want to fetch data
from the database and not from a file. 

To do that in my product.js file in the models folder, I don't need fs and path
because I'll not work with files and paths anymore, I don't need to construct
that path here at the top. 

We can leave the cart for now but that functionality will be broken for the
moment, I don't need my helper function here for getting products from a file
because we'll not work with files anymore, I will still create a product like
this so I will leave that code as it is, however I will delete my code for
saving here, we'll override this eventually, I'll delete my code for deleting,
for fetching and for finding by ID and I want to start with fetch all now. 

Here I also don't want to work with callbacks anymore but with promises, so I
don't need that argument, the callback argument, I shouldn't need that in any of
my functions here. 

So fetch all should now reach out to the database and what do we need to do to
do that? 

Well we need to get access to the database. 

So let's import our pool object from the database.js file, so I'll create a new
constant db and require database, whoops, not database but we'll go up one level
into util and there, database.js, without js. 

So now we get access to the pool and now in fetch all, we can execute a query
and now which query do we need to execute here? 

Definitely feel free to pause the video and write it on your own if you already
know it. 

Well here we want to fetch all products so it's the exact same query we ran
before, select everything, the star stands for everything, we could also select
just the ID and title with this syntax but I want to select everything, all
fields from products. 

Now as a side note, you could write select and from in lowercase too but I like
to keep these keywords uppercase to indicate what is core SQL syntax and what
are our dynamic values. 

So we select everything from products here and now as I said, this returns a
promise. 

Now we could add then and catch here but actually I'm interested in the returned
value in the place where I'm calling fetch all, so I will simply return the
entire promise that execute returns so that we can use it somewhere else. 

So now we can go to the place where we do call fetch all and that is in the
shop.js file in the controllers folder. 

There for example where we get the index page, we do call fetch all but right
now we still pass in a function that previously was the callback. 

Now we got no callback anymore, so let's take out that render code we'll need
that later and remove that anonymous function. 

Instead fetch all will now return a promise, so we can add then and catch, you
don't have to add both but you typically also want to have some error handling
mechanism, though we'll learn about a better one in the future, so later in this
course. 

So here I will again simply log my error and not do anything else with it but in
then, you remember we got this nested array, now we can use some next gen syntax
with a feature called destructuring where I can already pull out information of
the value I'm receiving as an argument here in my argument list. 

So here is my anonymous function which will be executed once we get data and
instead of using result or anything like that which is a nested array, I can use
the syntax here where I pull out my rows and my field data, you can name this
however you want and this will simply be the first element of the nested array
which would be our argument data and that will be the second element. 

And now we can use these two variables which simply hold these two nested arrays
and therefore I can console log them but I don't need to log them, I instead
want to render my page inside of this anonymous function, so once we got that
data and rows should be my products because my rows here are the entries in the
products table and therefore these should be my products. 

If we now save that and we go back to our running application in the server, on
localhost 3000 we shouldn't see the book here and also have no errors on our
console. 

Now we see that book because our data is retrieved from the database and
therefore if we were to go to the database and we for example add an exclamation
mark here in the title and then click apply, you always need to do that, apply,
close, if I reload my page here, it has no exclamation mark right now but now it
has, so this is really coming from the database. 

Now here's your little mini task, also make sure you're fetching data from the
database when loading the products page which right now is broken or not working
because there we still try to reach out to a file which will not work. 

Try to fix this on your own before we also start inserting documents or elements
into the database. 

---