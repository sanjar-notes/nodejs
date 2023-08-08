## 529. An Example Node REST API

<strong><em>no description</em></strong>

<v Instructor>So let's get started building some basic,</v> very basic node REST
API here. 

For that, I'll create a new subfolder, node and a new subfolder, deno. 

And in the node folder, unsurprisingly, we'll build the node API. 

Now it'll be a simple API. 

Nonetheless, in there, we'll have an app.js file, we'll have our routes folder
for your routes. 

We could add a controllers and a model's folder, but since it will be a very
simple API with some dummy data, I'll just go with this basic data structure. 

Now it'll be a very simple todo API. 

And I noted everyone hates todos, but I'm going to go with some todos, because
it's not so much about the fancy application, but it's about the differences
between node and Deno. 

And the easier the API is and the less amount of work we have to do there, the
easier it will be to grasp the differences and to grasp Deno's core features. 

So I have the todos.js file in the routes folder. 

I have the app.js file. 

And now of course, in node's case, I wanna use express.js here. 

So therefore I'll navigate into the node folder and run npm init to create a new
package.json file, where I'm going to confirm all the defaults, so that now in
that folder, we can run npm install to install express. 

And I'll also install the body parser to parse incoming request bodies. 

Now in app.js, we then require express. 

That's how we import in node. 

We could also import with the modern import syntax, which I cover in the modern
JavaScript module, but I'll stick to this traditional approach, which you'll see
in most projects. 

Also, I, again, disabled the Deno extension, so that I get good IDE support in
node code? 

No, actually that's not the app. 

That's the express package, of course, but we then create the app. 

That's what we do by calling express like this. 

And on that app, we then can call, listen, for example, on port 3000 to start
listening on that app server. 

And now we can register some middleware in node express with the use method as
you learned. 

Now, I will outsource some middleware into the todos.js file. 

So here we again, import express by requiring express. 

And then here we get access to the router by extracting it from express.Router
like that. 

And actually that should be lowercase because then on the router, we can
register various routes like a get route to /todos, which will get a middleware
function, with request, response, and next that should return todos. 

And by the way, if that's brand new to you, definitely go through the respective
sections in this course first, this is all node express knowledge you gained
throughout the course. 

So we have this get route. 

We then have a post route to /todos to get a new todo, for example. 

And we then also have a put route to replace a todo, for example. 

Here, I also want to get the todoId as part of the URL so that we can extract it
from there and identify the fitting todo and update that accordingly. 

It's up to you, by the way, if you wanna have a put or a patch route here. 

And we also have to delete route to todos and then also some specific todoId, of
course, and then we'll have that middleware function here as well to delete a
todo, just like that. 

And ultimately, we export the router here so that in the app.js file, we can
import the todo routes by requiring ./routes/todos.js, without the extension
actually just todos. 

This is how we import this, and now we can use this as a middleware and we could
also add some other middleware if we wanted to, we can register any middleware
whenever we want. 

So here I could console.log some middleware and I can always call next to
proceed to the next middleware in line. 

So that's how we can do this in node express. 

Of course our logic is missing here though. 

So to keep it simple, I'll just have a todos array up there, which is a very
simple array. 

And when we get a get request, I just want to send back a response with some
JSON data, where I add a todos property, which holds the todos array. 

So a very simple response. 

If we get a post request, I'll create a newTodo, which is a JavaScript object
that might have an id. 

That id could be the current date converted to an ISOString. 

And I have the todo text, which I expect to get from the request.body. 

There, I expect to have a text field. 

And in order to be able to extract that data from the body, in app.js, I also
want to import the body-parser by requiring it from the body-parser package,
which we installed. 

And I'll register the bodyParser.json middleware here. 

And this will parse all incoming requests, check if they carry JSON data. 

And if they do, the JSON data will be parsed and will be made available as a
JavaScript object on the request.body field. 

So we can create a newTodo then, and we can then reach out to todos and push the
newTodo onto todos. 

By the way, if you followed along with the TypeScript section in this course,
this API might look quite familiar to you. 

Now for updating a todo, we need to get that todoID. 

I'll store it in a constant named tid. 

And we get it from the request.params, and there we'll have a todoId param
because that's the name we picked here. 

So we can extract it here. 

And now we need to find the index of the todo in the todos array. 

So todoIndex is todos, which is our array, findIndex and findIndex takes a
function that executes for every todo. 

So here we get every todo as an argument, and we wanna return true if the
todo.id is equal to the extracted tid. 

Then we know that's the to do we wanna update. 

So then we can reach out to todos for the given todoIndex and replace the object
being stored there with a new object where I keep the id. 

So I still access todos for todoIndex here and extract the existing id, but
where I set the text to the text we get on the request.body here. 

That's how we could update. 

Now we wanna send back a response here and also for posting, of course. 

For posting, my response could have a status code of 201 to indicate that it was
successful and a new resource was created. 

And we could have a message where we say, Todo created! 

And if we wanted to, of course, we could also attach the newTodo, so that we
return the created data. 

And for updating on the response, I'll set my status code to 200 and then also
attach some JSON data where the message could be, Updated todo! 

Now for deleting, we still will need the todoId from the params so we can copy
this line. 

And then I wanna replace my todos array with a new array. 

So this array will be replaced with a new array, which should be the old array
minus the item with that id. 

So I'll filter the todos array. 

And filter takes a function that executes on every element in the todos array
and if we return true here, this element will be kept. 

If we return false, it will be deleted. 

So I wanna return true for todos where the id does not match, because if it does
match, I know it's the element I wanna delete. 

And then here, we also can set a status code of 200 and set back some JSON data
where we have a message of, Todo deleted! 

And that's a very, very, very trivial API now. 

Now with that, if we now run this API, so if we go into the node... 

Oops, into the node folder here, and I execute my app.js file, it starts
executing. 

And now we can use tools like Postman, which is a free tool. 

You can download and install to test our API. 

You can simply visit postman.com, download it there. 

You won't need to sign up to do that. 

You can just download it like this. 

And once you downloaded it and started it, you should see a screen like this. 

If you get a welcome screen, you can simply close that. 

And here you can set up new requests. 

For example, a get request to localhost:3000/todos. 

And this should fetch us all the todos. 

Now if I send this, we see that our server works. 

I get no todos, but I get a success response. 

So sending and parsing and handling the request worked. 

Now let's create a newTodo. 

For that I'll open up a new tab here and send a post request to
localhost:3000/todos. 

And now here we need to append some data. 

So under body, we can go to raw and then pick JSON here in the dropdown. 

And that will simply add some JSON data to the outgoing request. 

And there, we should set a text field because we're going to look for a text
field when we extract data from the body on the server side. 

So we should make sure that text exists here, and then I can send a new todo,
click send, and I get this confirmation message, status code 201. 

And if we now fetch all todos, we see the new todo here. 

Now for updating, it will the need todoid so we can copy that and send a new
request, a put request, because I'm waiting for a put request here to
localhost:3000/todo/ that id. 

Now the put request also needs the new data with which we wanna update the todo.


So under body, we still wanna add some JSON data, and that should again be a
JSON object, which has a text key because we're also looking for the text field
on the put request here, and there we'll have our updated todo text. 

If I now send this, this seems to work. 

We get back the success response. 

And if we get all todos, we see the updated text here as well. 

Now last but not least, for deleting, if we send a delete request to
localhost:3000/todos/ that id, we don't need to add any extra data. 

And if we send this, it seems to work. 

We get the confirmation message. 

And if we now get all todos, we're back to an empty array. 

So our API works, but that's of course, just node.js. 

Now let's see how we would build that same API with Deno and Oak. 

---