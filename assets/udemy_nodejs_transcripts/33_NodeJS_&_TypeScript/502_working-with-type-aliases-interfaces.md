## 502. Working with Type Aliases & Interfaces

<strong><em>no description</em></strong>

<v Narrator>Now in our TypeScript code,</v> we have some repetition. 

Not horrible and definitely bearable, but we have some repetition and some code
that could be hard to read. 

For example here we have repetition, we re-use the same union type in two
places. 

Now, this is definitely okay, but you could optimize this or improve this with a
type alias. 

TypeScript has a built in type operator, which does not exist in JavaScript,
don't confuse it with type of, type is a different one. 

This allows you to set up your own type alias so you can give a different type a
new name. 

And that is especially useful if you're working with union types for example. 

We can have our num or string type for example, the name is up to you, you could
name it like this, and the value which we store in there is now a type. 

So for example this union type. 

And now we can use num or string in all the places where we previously set up
the union type. 

And you can store anything, any type in such a type alias. 

Now if you compile this, if you compile this code, this will be gone, you don't
see the type alias there because it's a pure TypeScript feature. 

But it can save you some repetition. 

You can also use the type alias to for example store your object type. 

My result, and again that name is up to you, could be this object type. 

So I can cut it from down there, and now use result down there. 

And now I'm referring to this object. 

So type aliases can be very useful. 

An alternative, at least when you're working with object types are interfaces. 

Interfaces also allow you to define the structure of an object. 

For example result object, to avoid a name clash. 

Here I could paste in that exact same structure as for my result type alias. 

And I can now use result object where I previously used result. 

Now why would you use an interface or a type alias, what's the difference? 

If you're just defining the structure of an object, you can use either of the
two. 

Using interfaces is a bit more common but it's not a must to. 

Interfaces can however also be used to force classes to implement certain
methods or functionalities, but that's beyond the scope of this basics
refresher, you do learn about it in my understanding TypeScript course though. 

So for basic type aliasing, it doesn't matter. 

So, here we have a type alias, here we have the interface. 

A last important note is that if you would add your own class or constructor
function, you could use the class name as a type as well, just as we're using
date here. 

We can use date with new date to instantiate it and get the current date time
stamp, but we can also use it just as a type. 

And that's true for any constructor function and class, no matter if it's a
built in one, or your own one. 

---