## 497. Assigning Types

<strong><em>no description</em></strong>

<v Presenter>Thus far, we have some basic code here,</v> which works with
numbers and strings. 

Now we wanna avoid that strings can pass in. 

And for this in TypeScript files, we can set types, we can set types on
variables, we can set types on parameters, in a bunch of other places as well. 

And here we can add types to those parameters. 

To make it clear which kind of value will be accepted here, we add a type to a
parameter as well as to a variable by adding a colon after the variable or
parameter name. 

And then after we add the type we wanna use. 

Now TypeScript knows a bunch of Core Types which are simply built into
TypeScript. 

For example, the number type, integer numbers but also floating point numbers. 

Also negative numbers of course, these are numbers and for those we have to
number type, we have to string type if you want some text with single or double
quotes are also with the template literal syntax with the backticks. 

Sometimes we want true or false and for that we got the Boolean type. 

The Boolean type accepts just these two values true or false. 

We also tend to find object types. 

To accept an object like this, for example, we dared and also have the choice
between accepting a general object type, or if we want to specifically describe
how the object should look like which properties it should have and which types
those properties should then have. 

We can accept array types, for example, an array of numbers there, we also can
define if any content is allowed, or if it for example, must be numbers. 

And we got a bunch of other types as well. 

But let's stick to those basic types here. 

And here, we clearly want a number. 

So we just add number here, after num1, and after num2, it's the same colon
number and now something in interesting happens. 

My IDE already complains here, it basically tells me that the argument of type
one as a string is not assignable to a parameter of type number, because a
string is not a number. 

If I compile this code, I also get this error here, you'll see I get the error,
that about the same error as before. 

Nonetheless, it did compile the code. 

You can also configure TypeScript to not compile if it has such an error. 

The default is that it does compile. 

And here that's good, because that actually gives us another piece of important
information. 

In the compiled JavaScript code, that colon number thing here is gone. 

Because as I mentioned before, it's a pure TypeScript feature. 

It doesn't exist in JavaScript. 

It's only there during development to give us exactly that error, which we see
down there. 

That's why we have this feature. 

We only need it during development, because it allows us to catch bugs like this
and get rid of such lines. 

Now, that's TypeScript in a nutshell. 

And this might sound trivial, but that's its core feature. 

The essence of TypeScript is that you are very clear about the types of data you
work with in different parts of your app. 

And that overall leads to better code and less bugs. 

---