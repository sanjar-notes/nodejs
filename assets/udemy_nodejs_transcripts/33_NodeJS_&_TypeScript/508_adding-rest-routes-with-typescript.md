## 508. Adding REST Routes with TypeScript

<strong><em>no description</em></strong>

<v Teacher>Now let's define how a todo should look like.</v> And for that we can
create a type alias or since a todo for me here at least will be an object, we
can also define an interface Todo. 

And actually, I don't wanna define this here, but I'll create a new folder, the
Models folder, and in there my todo.ts file, where I now to find this interface
and where I also export it. 

Now if you add the export syntax in front of something like this, it's no longer
the default export. 

For that, you would need the default keyword, but instead now it's a named
export. 

And I will show you how to import named things in a second as well. 

Now we can define our todo type here. 

And for example, make it clear that we want an ID which is a string, let's say
and the todo text which should also be a string. 

And now with that exported, in the todo's routes file, we can simply, import
todo in curly braces from going up one level, and then into the Models folder
and then the todo file. 

And as you also saw before, you can omit the file extension here when importing
from .ts or .js files. 

Now we need these curly braces here because now we're dealing with a named
export. 

And for named exports, you need to import with this named import syntax, which
simply uses curly braces, and then between them the name which you wanna import.


If we had the default keyword here, just as we're having it in the routes file,
then we could omit the curly braces when importing this and just pick any name
of our choice. 

And that's just the default ES Modules, Import Export syntax, nothing TypeScript
specific. 

It's just supported by TypeScript. 

You can learn all the details about this syntax and about modern JavaScript in
general in my JavaScript Complete Guide course of course. 

So that's the todo model. 

Simply an interface which I defined. 

We're importing this in the routes file, and therefore now we can make it clear
that our todos here is simply an array full have todos, with this array type
syntax here. 

So now we're returning this on the get route. 

We also wanna expose a route for adding a todo, so let's say that's slash todo
for an incoming post request. 

And there we of course, also get a request, a response and this next function. 

And here we wanna add a new todo to the todos array. 

So my new todo here simply is a new object, but I will set the type of it to
todo to force TypeScript to force me to add the correct data to dissolve object.


Because for example, an empty object as I have it here, would not be allowed
because this does not match the todo type I defined here in the Todo model. 

That's the whole idea of TypeScript. 

Forcing yourself to write clean and clear code where you don't omit data. 

Because typically, if you omit data, that might just be a mistake, and we use
TypeScript to avoid such mistakes. 

So we can now set the ID property here, and set this for example to, the current
date converted to an ISO string, and set the text to some data we extract from
the incoming request. 

And for that, of course, we need to parse the request body. 

We wanna extract any data that's attached to the incoming request from its body.


And we have learned that we can use the body-parser package for that. 

Thankfully, we already installed this. 

So in app.ts we can now import it. 

We can now import bodyParser from body-parser. 

And we can then register a new middleware where it call it bodyParser.Json like
this. 

Now you saw that here I got all the completion, even though we haven't installed
the types package for body-parser. 

Now, that's actually some extra convenience added by TypeScript and this IDE
here. 

They even analyze JavaScript files. 

So even if a library is not using TypeScript, they analyze the JavaScript code
in there, and see if they can infer which features you are allowed to use there.


And to a certain extent, such inference can be made even with just a JavaScript
code. 

So for example, here TypeScript and my IDE were able to find out that indeed
there is a JSON method exposed on the body-parser object into JavaScript source
code off that library. 

For perfect TypeScript support, where it understands everything, including all
arguments types you might be able to provide, I still recommend that you always
install types packages for the libraries you're working with. 

So here, I'm going to install the types package for the body-parser library. 

Just for this extra TypeScript safety, even though I will admit that for the
purpose we're using it here, we wouldn't need that. 

Nonetheless, with that, I registered this middleware. 

And now we're able to parse incoming JSON request bodies, and use that data in
our other middleware. 

So for that, back here in the routes folder, for the text, I will set my
request, body, text. 

So I simply expect that on the incoming request body, we have a text field that
holds the text we wanna add. 

Of course, you might wanna add validation. 

And you learned how to do that throughout the course. 

And with TypeScript, it's really the same code, you just might wanna install the
extra types package for the validation library. 

But I will not implement all of that here because I just wanna focus on the core
TypeScript essentials in this module. 

Generally, the code you write, as you can see here, is not different from the
code you wrote before. 

You can just add the extra types like this todo type, and then gain a lot just
by doing that. 

Anyways, with that we added the new todo. 

Now we can reach out to the todos array and push the new todo into it. 

So now with that we added this and we added our post route. 

Let's now continue with a route for replacing a todo and for deleting a todo,
before we then test this and we talk about the general folder structure. 

Which gets a bit clunky with all those extra JavaScript files. 

We'll come back to that later. 

---