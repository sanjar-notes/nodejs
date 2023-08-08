## 15. Working with Objects, Properties & Methods

<strong><em>no description</em></strong>

Now let me get rid of that existing code. 

You find a snapshot of the code we wrote thus far attached to the last lecture. 

And let me write some new code. 

An important thing you work with or important data structure you work with in
JavaScript are objects. 

You could have something like the person object and you create an object
typically with curly braces and then in there you have key value pairs. 

You define the key by simply typing. 

Well, whichever key you want to use, let's say name, then you have a colon and
you must have the colon. 

And after the colon you have your value, in my case, a string max. 

And then with a comma you can add another key value pair, age 29. 

Now this is an object and I can lock person here. 

If I now execute pledges, we see that object being printed here. 

Now objects allow us to group data together. 

You can also not just have variables in there, so to say, but you can also have
functions in there, for example, a grid function. 

And there you can simply have an anonymous arrow function or an arrow function
general as a value after the colon. 

And then in there you could have console.log. 

Hi. 

I am. 

And then the name and this would now be accessed with this keyword instead of an
object. 

You have to use this to typically. 

And there is something special about this, which I showed in that video I linked
before in an earlier lecture. 

But typically this refers to the surrounding object and now we can use the dot
notation. 

So dot to access properties or methods, so variables or functions inside of that
object. 

So we could now use this name. 

And now I can use that person and call greet with the dot notation and executing
it as a function. 

So the dot notation is important on this, which refers to the object or on you
referring to that object which is stored in this constant here. 

And now if execute this again, I'm saying, hey, I'm undefined. 

Now, why is that? 

Well, the reason for that indeed, is what I taught you about arrow functions. 

This now here refers to the global scope to the global node runtime scope and
not to this object to have it refer to that we either have to use the old scroll
function like this. 

Now, if I repeat that, I'm saying, Hey, I'm Max. 

Or we use a slightly different approach or syntax here in an object, and that is
you don't use an arrow function, but you use it like that. 

So you omit the colon, add the parentheses after the key name, and then without
a function, keyword or anything like that, you add your function body. 

And now this is a method of this object. 

And you see, Hi, I'm Max two now. 

So this is something important and this is the syntax you'll see me use
throughout this course without the colon parentheses right after the key and
then the function body. 

---