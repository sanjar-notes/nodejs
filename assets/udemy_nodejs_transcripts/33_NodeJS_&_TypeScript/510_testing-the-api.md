## 510. Testing the API

<strong><em>no description</em></strong>

<v Instructor>To test this entire API,</v> we first of all need to compile it. 

And we can just run TSC for that, since this will compile all the TypeScript
files in this project. 

So you see that this completes without errors. 

One important note, is that in the models folder, you'll see the todo JS file is
pretty empty here. 

And the reason for that is that interfaces are a pure TypeScript feature. 

Which helps TypeScript during compilation, but which generate no actual code. 

Because this feature doesn't create anything that would exist in JavaScript. 

Therefore, we essentially have an empty file here without anything in it in the
end, if you take a closer look. 

But our code still works, because that todo interface is only used as a type
definition in the other files. 

Like here, for example. 

And that's a feature which doesn't exist in JavaScript anyways, that's what I
mean, it only matters during compilation. 

We disregard all those JavaScript files, and we can now just run them as we're
used to. 

So here I can just run Node app JS, and this will spin up our Node Web Server. 

And we can now test our REST API with Postman, as we did it before in this
course as well. 

Which in case you haven't seen it before, you can download from Postman.com. 

It's a tool that can help you with testing REST API's. 

And with that opened, we can send requests to our running web server. 

Which I started with Node app JS, and that's important Node app JS, not app TS,
but app JS. 

We can only execute JavaScript code with Node. 

Node is not capable of running TypeScript code. 

It's only capable of running JavaScript code. 

Therefore, we needed to compile the TypeScript code to JavaScript first, to then
run the JavaScript code. 

So that we during development can use TypeScript, but Node still executes
JavaScript. 

So with that up and running, we can now send the request. 

I'm running on localhost 3000, So therefore, to localhost 3000, we can send a
GET request like this. 

And this gives us all the todo's And you'll see I get back a response, but of
course we have no todo's yet. 

So let's send another request, a POST request to create a new todo. 

To localhost 3000/todo. 

This once's a request body, which should be raw and then JSON. 

And in that request body, if we take a look at that route, we try to extract the
text. 

So we should make sure that this text exists there. 

So here I'll set a text field in this JSON data I attached to the outgoing
request. 

And that could be my first todo. 

Make sure you write valid JSON here, with the opening and closing curly brace,
and then your properties between double quotes, and then on the right side of
the colon, your values. 

And if we send this, I get back to 201 response with the todo that was created
and the new todos array. 

I will now also send a second todo, by just sending the request again with
changed data. 

And if we now send the GET request again, we now see that we got those todos
here. 

Only in memory of course, so that data will be lost whenever we shut down this
server. 

But to play around with TypeScript and get those basics, that's enough. 

Throughout the course you'll learn how you can work with files and databases and
so on. 

So let's now try the other requests as well. 

Let's set a PUT request to localhost 3000/todo/. 

And now we need a todo ID. 

So now we'll just grab this ID here, for example, and add that to the URL. 

And then add a body which should be of type JSON of course, where I add a new
text. 

So here I'll say, updated todo as a text and send this, it works. 

And if we now fetch all todos again, we of course see the updated todo here as
well. 

Now we can simply copy that URL and send a last request, a DELETE request here
to that same URL. 

So localhost 3000/todo, and then the ID of the todo. 

No data attached, just a DELETE request. 

If I send it, I get back my success response. 

And of course, if we get all todos, we see that it was deleted. 

So the API works. 

And that's now an API built with TypeScript and Node. 

Now, I'm not entirely done with it yet though. 

Let me quit the server with Ctrl + C. 

And let's dig a bit deeper into this TypeScript Node project, and what we can do
with it. 

---