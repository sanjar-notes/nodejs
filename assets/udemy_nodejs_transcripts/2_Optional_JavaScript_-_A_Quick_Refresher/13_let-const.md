## 13. let & const

<strong><em>no description</em></strong>

Now that I had a quick look at the very basics and the core terms, you have to
know let's dive into some next gen JavaScript syntax you'll see throughout this
module or throughout this course. 

War is a keyword that creates a new variable, and actually it's a bit of an
outdated syntax. 

From now on, we'll use Led instead of war and let also creates a variable. 

The scoping behaves a bit differently, but we can ignore that for now. 

Here, check out some next gen JavaScript resource like my ES6 course or of
course all of them free resources to learn all about let. 

But the core reason for using lattice that we now also have another way of
creating a variable. 

And with that I mean a variable which never changes, which actually is the case
for all three here. 

But let's say we actually do assign a new value to H here, but we never change
name or has hobbies we could absolutely use let. 

There is nothing strictly wrong with that. 

But to be clearer about our intentions in the code and we know that we'll never
change let. 

Name and has hobbies. 

We can also use a new keyword available in JavaScript and that's the const
keyword. 

This creates a so called constant and this makes clear that we never plan on
changing the value of name or has hobbies. 

We do plan to change it of age and that is why we have led and that is the
reason why we have two different keywords for creating variables. 

Though again, these are not really variables. 

There are constants either const or let, depending on whether you plan to change
this or not. 

So now if I execute this, it works in exactly the same way as before. 

But by the way, if I would try to set a name to Maximillian here and I do run
node places again, I actually get an error now that I try to assign to a
constant variable. 

So this actually already shows us the idea behind concept and you want to use
concert as often as possible to be as clear about what happens in your code as
possible. 

And if something should never change, make it a concert so that you get an error
if you do accidentally change it. 

So here I'll revert this change. 

But I wanted to show you how let and cons to work. 

---