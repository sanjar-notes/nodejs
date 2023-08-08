## 509. Finishing the REST Routes

<strong><em>no description</em></strong>

<v Instructor>So there are two more routes</v> which I want to register here and
the first extra route is a put route to /todo/:todoid. 

The idea is that requests reaching this route simply replace a todo. 

So here we also get our three arguments but now in here I wanna override that
todo. 

A todo, which I identify by this todoId. 

So the tid for todoId can be extracted from req.params and then they're simply
.todoId, which is available because we got this here. 

And with that, I want to find the index of that todo in my todos array so we get
our todoIndex here. 

We're reaching out to todos, and there we can call findIndex to find the index
of some element and this takes a function which executes on every array item, so
on every todo item therefore. 

I want to return true if the todoItem I'm currently looking at has an id that's
equal to my extracted tid here, so to this todoId I extracted from the URL. 

That will give me the todoIndex of the todo I want to update. 

I'll now check if todoIndex is greater or equal than zero, otherwise we didn't
find a valid index, and if it is I want to continue, otherwise, I will return a
response where I set the status code to 404 because we weren't able to find a
todo with that index, and I sent back a message where I say "Could not find todo
for this id" or whatever you want to return. 

In this if block however, we know that have a valid todo. 

So here I want to reach out to my todos for that todoIndex and replace the todos
stored there with a new object. 

Now again, here are types of complaints if I just would keep the code as it is
because an empty object is not a valid todo and that's great, that's exactly the
support we want. 

So here we can now set the id to either a brand new id or we keep the existing
todo's id to just update the text. 

That's what I'm going to do by reaching out to the existing todo and then there,
I'll just get the id and keep that id and just update the text to the request
body text, which I now got on the incoming request. 

With that, we updated the todo and then I wanna return response status 200 and
also reply with a message where I say "Updated todo" and maybe I'll return all
my todos here. 

Side note, I forgot to return a response here in the post request. 

Of course I want to do that here as well. 

Set the status code to 201 to confirm that something was inserted and then maybe
a message of "Added todo." Return the new todo which we did add and maybe even
return the overall todos array if we want to. 

Of course, it's up to you which kind of data you want to return. 

Side note, you need to add the return keyword in front of this response here to
avoid that this response and code runs as well. 

We only want to send back one response and therefore we need to return to avoid
that this code executes as well. 

And with that, we added the put route. 

Now it's time for the delete route. 

So on the router, we can register a delete route, maybe for /todo/:todoId, so
similar to the put route, just with a different word. 

There we also get the request, response, and this next function. 

Then in here, we of course want to update the todos to get rid of one. 

For that, I'll convert my todos array from a const to a variable with the let
keyword to ensure that we actually can override it with a brand new array
because I want to get rid of a todo by creating a new array which is the old
array minus the deleted array. 

For that, we can simply set todos equal to todos.filter to filter out a todo. 

For that, it runs a function on every todo and if we return true in that
function, we keep the todo. 

If we return false, we delete it. 

I want to return false if the todoItem.id is not equal to the request params
todoId because if this is equal, I know it's the todo I wanna delete so I want
to return false for that match, hence this exclamation mark here, to make sure
that the new todos array does not contain the todo with this todoId here. 

And that's all. 

Now we can send back a response where we say "Deleted todo" and maybe if you
want to, return the entire array of todos. 

So that's a very simple REST API with four routes which allow us to get, create,
update, and delete our todos. 

Now, let's also test this and see whether everything works before we then work a
little bit more on the project structure and how we split our code and before I
also share some other information about TypeScript. 

---