## 19. Destructuring

<strong><em>no description</em></strong>

Rest and spread are important syntax to know. 

Now I want to dive into another important feature and that is the structuring. 

Now let me comment out this code down there and let's begin with Object D
structuring. 

I got my personal object and now let's say we have some code where I only need
to name. 

So I have a new function print name, let's say. 

And that actually takes the full person object because for whatever reason we
write wrote it like this, or we simply have a function where we are able to get
multiple arguments or a full object because some third party package always
gives us that person. 

We can't change that. 

So we get the person here and I only want to console.log person that name. 

Now that is totally fine of doing it like this. 

I can now execute a print name here. 

Now I need to pass person here now to avoid naming confusion. 

Confusion? 

You can name this here however you want. 

So here we could name it person data. 

And inside here we use person data. 

So that function does not use that person. 

It just expects any person data. 

We then call that function and pass in that person as an argument. 

And now if they execute that file, I see Max here. 

This is stemming from this line here. 

Now, of course, we can absolutely do it like that. 

And we always get person data because again, let's say this is a function which
is actually called by some third party package, which is a pattern you see quite
a bit throughout this course. 

Now, therefore, we can't change the data we get, but in this function here we
are only interested in the name. 

We can then use a syntax or a feature called Object D structuring where we add
curly braces here in the. 

Argument list and we then specify the property of the incoming object. 

We are interested in name. 

That is this property we have here. 

Then this will be pulled out of the incoming object. 

The other properties will be dropped for this function and it will be stored in
a variable named name, which we then can use in there. 

So now if I execute this again. 

I also see Max, but now we're using this de structuring syntax and we can pull
out the FF too if you want to. 

Or the grid function. 

So that all works. 

And that is just a syntax we can use that allows us to write a bit of a more
understandable code where we are very clear about what we need from the incoming
object and which then gets stored in a local variable that we can just use in
this function. 

And you can of course not just use the structuring inside of a function, you can
always use it outside of there. 

You can create a new constant here, for example, and then the syntax will look
like this curly braces equals person, curly braces on the left side of the
equals sign or something. 

We don't see that often in JavaScript because typically it's wrong, but for the
structuring it's correct. 

And then here we can have the name and the H and this will create two new
constants which hold the values stored in name and H. 

So these names here have to match the property names of the person and now we
can console, log name and h like this. 

If I now re executed file. 

This output here is coming from this console log and the values we're outputting
here are retrieved via object D structuring. 

Now, there's also not just object restructuring. 

You can also restructure, erase. 

So if we go back to the hobbies. 

What you have here. 

Well, then, if we would want to structure that. 

We can also create a cost. 

You could also use led, by the way, the same for the object restructuring. 

If you plan on changing it, you could use a cost for hobby one and hobby two
wrapped in square brackets. 

And then assign this to hobbies. 

And now if you console.log hobby one and you console log hobby two and you
execute that file again, you see the two hobbies being printed there. 

Please note there are no square brackets around them in the console log because
we're not logging in array here we are logging. 

Q Individual values, which we got via. 

Air raid restructuring. 

Unlike the object restructuring here, you can choose any names you want because
in a race your elements have no names. 

They are instead pulled out by position. 

So this will always be the first element. 

This will be the second element in objects. 

You pull them out by name, by property name. 

So that is the structuring and this is also something used in this course. 

It simply allows us to access elements in objects or arrays quickly by their
name or position and to drop. 

And that does not mean delete. 

They're not getting deleted. 

They're just not used in our function or whatever we're writing. 

So to drop the data, we don't need in that specific code snippet we're working
on. 

---