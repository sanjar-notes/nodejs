## 18. Understanding Spread & Rest Operators

<strong><em>no description</em></strong>

In modern JavaScript, there are two important operators you also should be aware
of, since I'll be using them throughout the course as well, and that are the
rest and spread operators. 

Now specifically, the spread operator is one we'll use quite a bit. 

Let's say we want to implement the pattern where when we add a new hobby, we
don't edit the original array, but we create a new array with all the old values
and the new value. 

This is actually a pretty common pattern called immutability, where we never
added existing values, but where we always replace them with copies plus the
changes. 

And that is all the pattern I'll use quite a lot in the course. 

The idea behind that is that we avoid errors because we always have this clear
approach of copy, then add it and don't edit existing objects which might lead
to more unreadable code. 

Now to copy an array, let's say here I create a copied array. 

We got a couple of possible techniques. 

One of them is to use the slice operator. 

Now if I output copy the arrays down there and I run node pages, I see sports
and cooking. 

So I did indeed copy it. 

Slice simply copies an array. 

We can pass arguments to narrow down the range of elements we want to copy. 

With no arguments. 

We copy the entire array. 

Now instead of slides, there is also a different technique. 

We can create a new array with square brackets and we could add hobby stair. 

Right. 

Now what happens if we execute this? 

What will we see in the console? 

Well, if I hit enter, we see. 

Well, it looks like a copy on first sight, but actually it's an array with a
number array in it. 

So the outer array has only one element and that's the inner array. 

So it's not a copy, it's just a new array where the first element is the old
array. 

And with that I mean the exact same object, not a copy of that. 

So we just created a. 

Nested array here. 

That, of course, was not what we did want to do here and here. 

We can use the spread operator. 

The spread operator are three dots. 

We can add in front of an array or of an object. 

And these three dots are an operator, just as the plus or minus are. 

And they do one thing. 

They take the array or object after the operator and pull out all the elements
or properties. 

So all the elements of an array are all the properties of an object and put it
to whatever is around that spread. 

Operator. 

In this case, we got square brackets around the spread operator and therefore
all the elements which are pulled out of the existing array are added to the new
array. 

And therefore, if I now run this file again, whoops, and I save it before
running it again, now we see this was the output of the old approach, the nested
array. 

Now we got no nested array anymore. 

We got one array and this is now a copy of the old one because we take the
spread operator to pull out these elements and add them one by one to the new
array. 

So this is something you'll see we do a lot to copy existing arrays or objects
there. 

It would work in the same way we could have our copied person by using curly
braces, then the spread operator, the three dots, and then the old person. 

And now if I console.log, the copied person here. 

And I execute this file again. 

This is our copied person here because I'm pulling out all these elements from
that object and I add it to a new object. 

So this works for both objects and arrays, and it is a syntax I'll use quite a
bit in this course. 

Now this is the spread operator. 

I also mentioned the rest operator, and the rest operator is essentially the
opposite. 

Let's say I have a function which I'll name to array. 

It's an arrow function. 

And there I expect argument's arc one arc to arc three. 

I want to return an array that contains these arguments. 

Whoops. 

And I should add a equals sign here. 

So I want to return an array that contains these arguments. 

I can return square brackets here, of course. 

And then the first element will be ARG one. 

Then I have ARG two as the second element and arg three as the first element. 

Now I can console lock to array and I pass one, two and three as the free
arguments to that function. 

If I now execute pledges, we see an array with one, two and three, these three
elements. 

So this is working, but this is totally not flexible. 

What if we want to pass four arguments? 

Well, we could call it like that. 

JavaScript actually allows that, but of course it doesn't get added because we
only work with three arguments here. 

What we could do is we could use the so called rest operator there. 

Dot, dot, dot and then just arcs. 

And this will actually take all the arguments. 

How many we might specify. 

That doesn't matter and it will bundle them up in an array for us. 

So here args will be an array and I can just return that actually. 

And now if I re execute this with two array getting four arguments, you see now
I have my array with four arguments here. 

So the rest operator looks just like this. 

Bread operator three dots. 

And it's the place where you use it that defines how you call it. 

Are you using it to pull elements or properties out of arrays or objects? 

Then it would be the spread operator. 

Are you using it to merge multiple arguments into an array and you use it in the
argument list of a function. 

Then it's the rest operator. 

It's the same operator by the syntax or from a syntax perspective, the name
differs depending on the place where you use it. 

I'll not use that syntax a lot in this course, but it's still nice to know. 

But being able to pull out elements or properties, that is something you should
understand because that is a syntax. 

You'll see me use quite a bit throughout the course. 

---