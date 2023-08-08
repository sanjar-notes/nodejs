## 538. Finishing the Deno MongoDB CRUD Operations

<strong><em>no description</em></strong>

<v Instructor>So, time for the final two methods.</v> Let's start with updating.


Here, we're extracting our todoId and data from the request body. 

And, previously, we then updated a todo locally in our todos array. 

Now, we're working with a database now, so, of course, the idea is that we
replace that logic with a new logic. 

So, let's delete that code here. 

And now, before we send back a response, let's get access to our Db with getDb. 

Let's connect to the todos collection. 

The same collection we used for storing todos and for fetching todos. 

And, on that collection, with MongoDB, we can execute a updateOne method. 

And this method does what the name implies. 

It updates one document. 

Now, updateOne takes two arguments. 

The first argument is a filter that allows us to find that one document which we
wanna update, and the second argument will then be our update instructions. 

So, let's start with the first argument. 

You should pass an object here, and then you can define a key, for example, the
id, and then the value that key should have in the database to identify this
document which you wanna update. 

So, here, of course, I wanna use the id I got here. 

However, this will be an id as a string, and MongoDB uses this ObjectId thing
internally. 

Thankfully, converting a string to such an ObjectId object is simple. 

We just use ObjectId, what we're importing from the Mongo module here. 

We're just using this as a function, and we pass our string id to it, and this
will convert it to an object. 

Now, we'll also need to change one thing. 

ObjectId always wants a string, and this tid could actually be undefined, as you
see here in the tooltip. 

The reason for that is that TypeScript doesn't know with certainty whether we'll
be able to find a todoId in the params. 

Well, since we wrote this code, we, of course, know there will be a todoId if
this route is reached, and, in TypeScript, we can add a exclamation mark here to
really make this clear that this will never be undefined. 

That this will always be a string, therefore. 

That's a tiny adjustment we'll need to make here. 

Otherwise, we'll get an error later. 

With that, we can add the second argument, which are our update instructions. 

And here, we can use a MongoDB specific syntax, and you can learn more about
MongoDB in my MongoDB course by the way, and that syntax is $set, and then we
define the key value pairs where we wanna set a new value. 

And here, at the end, I want to set text to a new value, and I want to set it to
data.value.text, so to the text I have on the incoming request body. 

That's the code we use to tell MongoDB to update a document accordingly. 

And now, just like the other MongoDB operations, this returns a promise, so we
can await this. 

Here, I'm not even interested in the result of that because I, thereafter, just
set back a response like this. 

Now, for deleting, it's quite similar to updating. 

Here, we can replace this code, call getDb, and then reach out to our todos
collection. 

And there, we now have a deleteOne method, which deletes one document, and just
like updating, this needs an identifier. 

It needs a description of how to find that one document. 

For that, we can copy the exact same logic as we're using it on updateOne for
the first argument, and copy that into deleteOne. 

And now, here's the error I talked about earlier about this tid potentially
being undefined and TypeScript not liking that. 

And, again, as before, we know with certainty that this will never be undefined,
that this will always be a string, so we can add the exclamation mark here to
make this clear, and, with that, the error is gone, and this will now delete one
document. 

I also want to await that, and, for this, we need to convert this into a async
function, and I then return this response. 

So, now, we got all that logic implemented. 

That means that we can now got rid of that todos array here. 

And if we now save all of that, and we rerun this back-end application, we
should have an app where we can reload it, and we still fetch the todos. 

If I edit a todo, you see that's being updated here. 

And if I reload, that still is there, which means it was stored in a database. 

And if I delete this, it's also gone now. 

Now, of course, you could add a loading spinner here on the front it ends on,
but this is not about the front-end. 

It's about the back-end. 

And if I restart the app, the data is still gone. 

If I add a todo again, and then edit it like this, and I then restart, the data
is still there, which proves that it really is stored in a database. 

So, that's Deno, and how we can connect to a database like MongoDB with help of
the Mongo third-party module. 

---