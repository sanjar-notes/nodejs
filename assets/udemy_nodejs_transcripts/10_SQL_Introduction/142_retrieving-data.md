## 142. Retrieving Data

<strong><em>no description</em></strong>

So we're executing a query here with execute on our pool, on the products table
we just created and I added then and catch. 

These are functions we can chain onto the result of the execute call, so they
will execute on whatever this gives us back and this whatever is some so-called
promise. 

Now a promise is a basic javascript object not specific to node, it's also
available in javascript in the browser which allows us to work with asynchronous
code. 

Instead of using callbacks which we could also use with the MySQL package,
promises allow us to write more structured code because instead of having a
nested anonymous function here as a second argument, we simply have a then block
which will then get the anonymous function to execute. 

Now the advantage is we can also write it like this and now we have very
readable code instead of having a nested code here and that nested code
especially becomes a problem if we have more and more asynchronous tasks
depending on each other. 

Now we also don't just have then, we also have catch and this also has a
function which executes in case of an error, so for example if the database
connection fails or something like this. 

We get the error object here and this is just a modern javascript syntax where
we get one argument and then we handle it here and I can simply log it with the
console so that we at least see what the error was. 

Now we hopefully end up here and we probably get an argument here too, let's
name it result for now and let's also log result here then and now let's see
what we get. 

If I run npm start to bring up that server again, this immediately executes
because it's part of the app.js file and if we have a look at this, we see this
is the object we got back and in this object, we essentially also see the data
that was retrieved here. 

The data we do get back has a format of an array with a nested array where the
first nested array seems to depict our data, the rows it fetched and the second
array seems to hold some metadata about the table we fetched it from. 

So result basically is an array with two nested elements,  so we can also logout
results 0 and result 1 here and if we now save this and therefore our server
restarts, we have almost the same output but now it's not a nested array but
here we have the first object we retrieved, the row we got and then this ends
here, here is the closing square bracket and then here we get the second log, so
this is the result one with the metadata. 

This is what we get back and this should allow us to work with our data. 

Now obviously we don't just want to work with dummy data but let's now see how
we can adjust our models to interact with our database instead of local files. 

---