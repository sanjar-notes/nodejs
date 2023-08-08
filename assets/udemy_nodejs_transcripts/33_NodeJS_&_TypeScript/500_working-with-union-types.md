## 500. Working with Union Types

<strong><em>no description</em></strong>

<v Presenter>So now we added the configuration.</v> Now let's say, we actually
want to make add a bit more flexible. 

It should work with numbers, but it should also work with strings. 

Of course I wanted to ensure that it works with numbers to show you why
TypeScript is awesome, but still, this could be a use case that you have in some
app you are building. 

You want to allow both numbers and strings because maybe here, we want to have a
string result as well. 

And there, I want to be able to call add with the string values. 

And I want to get that concatenated result. 

So I want to have that concatenated string of numbers. 

Now, currently we are only accepting number here. 

We could change this to any. 

Now any kind of data is accepted. 

But as a downside, we can now, for example, also console.log add, and add true
and false together. 

Now I don't want to accept Booleans, I want to accept strings and numbers. 

That's where we can use a feature called the Union Type. 

Often in code, you will have code that works with more than one type. 

Now in that case, you can define multiple types, like number and string
separated with that single pipe symbol here. 

This is a Union Type. 

It means number num1 is either a number or a string. 

And we can do this here for num2 as well. 

Now we get an error here because of that Union Type thing because even though
the plus operator does work with both number and string, TypeScript at the
moment at least doesn't understand this. 

And even though this here is a strange error because the plus operator of course
would work for both numbers and strings, it is also often the case that you
accept multiple types, but you wanna run slightly different code depending on
the type of data you get. 

So that's actually great that we can do this here as well. 

And we can do this with a traditional if check. 

We can check if the typeof num1 is equal to number, and this is regular
JavaScript code now. 

This is not TypeScript code. 

The typeof operator exists in JavaScript and it gives us back the types as
strings, number and so on. 

So we can check if num1 is a number and if num2 is a number, and if it is we
return num1 plus num2 else if typeof num1, is let's say a string and typeof num2
is a string, then let's say we wanna return num1 plus and then maybe some white
space in between, you don't have to add it though. 

I'm just doing it here so that we see a difference besides the different result,
I guess. 

Well, and else, if we have mixed types, it theoretically would work, but in this
case, we maybe just want to force a conversion to a number so that if we get a
string and a number mixed, we always convert both to a number. 

If we have two numbers, we add them like this. 

If we have two strings, we add them like this. 

This is a so called Type Guard, because we run different code based on different
types we're getting for our values. 

And now you'll see that down there, I'm not able to call this for Booleans
because this is neither a number or a string, and I'm only allowing these two
kinds of types with my Union Type here, hence, we have to remove this. 

And then we can compile this again. 

It compiles without errors. 

And in the generated JavaScript file, of course, the Union Type is gone. 

The if checks are still there though, because as I mentioned that is regular
JavaScript code. 

And of course, we don't want that code to magically go away. 

In the end it does yield different results. 

So if we now return here and I enter five and 11, you see we get both 16 as well
as our concatenated string. 

So Union Types are another key feature. 

---