## 14. Understanding Arrow Functions

<strong><em>no description</em></strong>

Let Them concert are two relatively new features in JavaScript and now we're
cool. 

New feature are arrow functions. 

We can rewrite this function as an arrow function by first of all, creating a
new variable or constant. 

Since I'll never set a new value, I'll use a constant and I'll give that the
name of my function. 

So summarize user. 

The value which I then assign after the equal sign is a function. 

Now, we could already have done it in the past with this syntax. 

This is another way of defining a function. 

The part on the right side is the so called anonymous function because we don't
set up a name after function, but we make it a named function implicitly by
storing the anonymous function in that named constant. 

So we can always call that constant, which holds a function as a value, and we
call the value with the syntax. 

And therefore this is like a named function here. 

So this would have worked in the past too. 

It is a way or a different way of defining a function, but we can now also use a
new syntax where we remove the function keyword and instead we add an arrow
between the argument list and the curly braces. 

And this arrow is simply a equals sign and a greater than sign. 

This also creates a function. 

It's a bit shorter since we save the function keyword and it runs in the same
way as this function ran before. 

Now why would we use this syntax? 

Except for the reason that it's a bit shorter? 

Well, that is already a nice reason. 

But also there's one key difference regarding the this keyword which JavaScript
knows and attached, you find a link to another video, an article I created where
I dive into the this keyword and how arrow functions help us with it. 

The attached article and video actually uses the browser, but it's the same for
Node.js, so this will be helpful to you have to know what JavaScript objects are
for that. 

But again, that is some core knowledge I require you to have for this course. 

In this course I will pretty much only use arrow functions. 

So this syntax for defining a function should be something you understand for
this course that this is the name of the function. 

And then here we have the arguments and then we have the function body. 

Now a little side note, there is also a shorter syntax of writing this or a
couple of shorter syntax. 

Let's say I have a number of function which I'll name add and there I get two
arguments A and B and I just return to some of them. 

So the addition then you could right return A plus B of course. 

And that allows us to run console log add with one plus two. 

And if I now run node play JZ, we see three here as a result, if you only have
an error function with one statement, which happens to be the return statement
or which you are fine returning, well then you can omit the curly braces, you
can omit the return statement and you have to admit it and you just use the
function like that. 

This simply is the same syntax as before with the curly braces and with return,
and this function will now always return the result of this statement here. 

So now if I execute this again, we still see free. 

Now, if I would adjust this function to, let's say, always add one. 

Then I have just a as an argument, let's say, and I return a plus one. 

Now I could call this but console logging at one to, let's say one year. 

So the result should be two. 

And I can, of course, execute this. 

And indeed I see to hear. 

Now in such a case. 

You already saw my audio formatting removed the parentheses I had there
previously, because if you only have one argument and that's the case really for
that case, only if you have one argument only then you can just have the
argument name here without parentheses and it will work just as it will work
with parentheses. 

So both works here, but you typically use the syntax without the parentheses. 

And again my ID or the formatting remove them for me. 

If you have an arrow function with no arguments at random, then you have to
specify an empty pair of parentheses. 

Though you can't have just a white space, you have to have that empty pair and
then you can have your code there, which obviously uses no arguments because
that's exactly what I want to show here. 

So here I could have. 

At random called Like This without any data passed in. 

And now we see three here from that result. 

So these are arrow functions and they're different syntax and you will see them
throughout the course and you should recognize that syntax and understand how
they work again for a reason why to use them, check out the attached article
plus video. 

---