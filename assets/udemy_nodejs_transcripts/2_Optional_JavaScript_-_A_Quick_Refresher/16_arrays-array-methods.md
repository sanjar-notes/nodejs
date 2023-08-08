## 16. Arrays & Array Methods

<strong><em>no description</em></strong>

Besides objects, another crucial data structure in Node.js or in JavaScript in
general are arrays like hobbies. 

An array is defined with square brackets, and in an array you can have any data
you could normally use to. 

You can use strings in there like sports and cooking. 

You can't have numbers in there and you don't have to use one at the same type
in the array. 

Here we are mixing text and numbers. 

You could have arrays with just text, just numbers and so on too. 

Of course you can use Boolean values and you can even store objects in there or
other arrays. 

That is all possible. 

Now here I'll have an array of text though, and you can use four loops to go
through that. 

With this syntax, for example, with the four off loop where we store each
element for each iteration in that hobby variable. 

And now if we do that, we would execute console.log two times because we have
two elements and we're looping through all of them and I'm outputting the
current value we're currently looking at because this will change for every
iteration. 

Going through it from left to right, we'll output that for every iteration. 

So now if I run this, we see sports and cooking printed in two lines because
this executes two times. 

So these are arrays for off loop is interesting. 

And it's also interesting that in JavaScript we got a lot of built in methods we
can use on arrays. 

So on hobbies on that array. 

If I add a dot, my ID suggests a lot of methods I can use on arrays in
JavaScript, and all these methods help me go through the elements of the array,
manipulate them, get a subset of that array, whatever I need. 

Often you'll see a map, for example, which allows you to transform an array or
transform the values and map will actually return a new array. 

So it will not edit the old one but give you a new one. 

And we can print that new one here, actually. 

And just to show that the old one was not edited, we can print that right below.


And now MAP always takes a function where you define how to edit that array or
how to edit the elements in the array. 

That function will be executed on every element in the array, one after another,
and you return the updated version of the element. 

So here we would get our hobby. 

You can name this however you want. 

And here I'm using an arrow function with one argument only hence no
parentheses. 

And in here I'll return the edited version. 

For example, here I could take my old hobby string. 

And simply add. 

Hobby and a wide space in front of that. 

So I'm simply constructing a new string which keeps the old hobby name, but adds
hobby cold and white space in front of it. 

And yes, since we only got one statement in that arrow function with a return
statement, we can get rid of the curly braces, get rid of return and just return
like this. 

This would be the equivalent. 

And now if I clear this and I run as I see the old array was not edited, that is
my second output here. 

It's coming from this console lock where I console lock the original array. 

But the result of my map here is a new array where I have my edited items with
hobby added in front of every item. 

And this is something you'll see me do quite a bit in this course. 

Use that map method. 

And as I mentioned, it's only one of the many methods provided here. 

Always check out the docs on MDM to learn more about all these methods. 

Link can be found attached to this video and make sure that you understand how
they work or that when we use one of them in this course, you can quickly look
that up in case it's not clear what exactly that does though of course I will do
my best to explain it when we use it. 

But these are arrays, very important data structures and some very important
methods you can use on arrays. 

---