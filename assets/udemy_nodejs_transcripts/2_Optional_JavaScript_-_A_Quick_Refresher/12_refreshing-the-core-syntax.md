## 12. Refreshing the Core Syntax

<strong><em>no description</em></strong>

For that, let's just play around with JavaScript and I'm going to brand new
empty folder, which I opened with my IDE Visual Studio code, and in there I'll
create a new file and I'll name it played out. 

JS The name is totally up to you though. 

Now let me start with some core language features, variables and functions. 

And again, you should definitely dive into a core JavaScript resource like the
ones I linked in the second lecture of this module if you are brand new to
JavaScript. 

So I by now do expect you to know what variables functions are. 

I also expect you to be aware of what if statements or loops are. 

These are all core things you got to have set by now because they are crucial
for JavaScript, no matter if you're using it in the browser or on the server. 

So for variables you might know desc syntax. 

With the var keyword you can have one name and for example store max in their
right. 

This would be a variable. 

And now you can use that, for example, to simply output it like this. 

And if we now run this file with Node.js by running node play Dodges, this is
the command we have to write in a terminal, navigate it into that project
folder. 

So into that folder where I'm having this play this file, then I see Max down
there, right? 

So that is some JavaScript code. 

We can also create a number variable H, which now would be a number. 

It's not in close to quotation marks. 

So this first one is a so called string. 

This is a number. 

We can also add a third one. 

Has hobbies and that would now be a boolean. 

These are some core types JavaScript nodes true false are booleans numbers are
well numbers. 

They can also have decimal places. 

These are strings. 

And now here I can also define a function with the function keyword summarize
user. 

This is how you create a function JavaScript and there we could return
something. 

Functions can return values with the return statement. 

They also can get input like user name, user age and user has hobby. 

You can name these arguments as these things here are called however you want. 

These are now local variables only available inside of the function, not outside
of it. 

And then you can return. 

Name is plus username. 

Plus, let's say, some text with a comma, a white space. 

Age is wide space user age plus and the user has hobbies and then user has
hobby, something like that. 

Now here I'm simply returning some text which I'm manually concatenating by
hardcoded strings and the dynamic values I'm getting as an argument. 

Now we can also console.log the result of summarise user we call a function by
adding parentheses after the name and now we just have to pass in data we expect
here as arguments. 

So we need to pass in three arguments here the name The Age and has hobbies. 

So the three variables I defined up here, we could have directly accessed them
in the function. 

Two, By the way, we don't have to take the way of accepting arguments, but this
is a pure function which does not depend on anything from outside the function,
but gets all the data it works with as part of the arguments, which is a nice
way of writing functions. 

And now if I execute this well, then we get this output here. 

Now, this is just a summary of the features you should be aware of. 

As I mentioned, I just want you to know, or I just want to be sure that you know
how we work with variables, how we work with functions, how we call functions,
and that you understand how parameters or arguments in the function are used in
there and only in there. 

We couldn't use user name outside of their because of something called scoping
in JavaScript. 

We can then call a function like this and pass in the data. 

We could hardcoded the data here or refer to variables which have to be
available in the scope of this statement, which is the case for these variables,
since they are global variables and these are variables and functions and how we
interact and these are some core features you have to be aware of. 

Let's now dive into something more exciting in the next lecture. 

---