## 498. Type Inference & Type Casting

<strong><em>no description</em></strong>

<v Instructor>Okay let's now wire up our function</v> to our formula. 

For that, I'll add IDs to those inputs, num1 and num2, so that in our app.ts
file, we can get access to those elements. 

Num1Element is for example, accessed with document getElementById, num1. 

That's some default JavaScript code, which we can run in TypeScript. 

And that's the next important takeaway. 

TypeScript builds up on JavaScript. 

This means that any JavaScript code, works in TypeScript files. 

You can learn TypeScript by simply sticking to what you know and then you add
types step by step, maybe you find some place where you can use some advanced
TypeScript feature you heard about. 

But in a nutshell, you can always just write JavaScript code and it will work
because TypeScript builds upon JavaScript. 

All JavaScript code is supported in TypeScript. 

Therefore, we can use this regular JavaScript code for selecting the
num1Element. 

We can duplicate this to get access to the num2Element. 

We can get access to our button element by reaching out to the button with
document querySelector and selecting the first button which we find. 

And then we can add a listener, an eventListener to button element by calling
addEventListener on it. 

Add a click event listener. 

And to find a function that should execute when the button is clicked. 

Now something interesting you see here, is that my ID knows that I can call
addEventListener on the button element. 

To ask this might be clear, we know that we select a button and we know that the
button DOM element has the AddEventListener method. 

But why does my ID notice in the end because of TypeScript, because it knows
that when we select a button with querySelector, what we'll get back is an
HTMLButtonElement. 

If I hover over a button element you see here, that's something which is called
the inferred type. 

We didn't define this type explicitly. 

I didn't add colon HTMLButtonElement here, though I could. 

But we don't need to do this here, because TypeScript is able to infer types. 

And it's really smart regarding that. 

it's able to find out which type of value will eventually be stored in this
constant because of this code here. 

And that's pretty nice of course. 

So it knows will eventually have a button in there and that's why it knows that
we can call addEventListener. 

Now here inside the event listener, I now want to extract the values from num1
and num2 element. 

So here I got my num1 are reaching out to num1Element. 

And then there I want to access the value property. 

Now my ID does not like this here. 

The reason for that is, that not every HTML element has a value property. 

Input elements have value properties, paragraphs for example, don't. 

So we need to convince TypeScript that what we get access to here will be an
input. 

For the button, it knew that it's a button because we query select by the button
tag. 

Here, we select by ID, so TypeScript has no chance of knowing which kind of
element it will have those IDs. 

But we can do something else related to types which is called type costing. 

If we as a developer know with certainty that something is of a certain type, we
can use the special ask keyword which is added by TypeScript to tell TypeScript
that what we select here will be off that type. 

And here it will be off the HTMLInputElement type. 

We can do this on both these elements. 

Now these types here, HTMLInputElement, HTMLButtonElement. 

These are general types which are built into TypeScript so to say. 

You can always use them just like you can use number ends on. 

These are some general DOM types which are available in TypeScript. 

And with that now, we can access value here, because now we know that there will
be a value property on this DOM object. 

We also get num2 with num2Element.value. 

And now we can call add, or we can get our result by calling add and passing in
num1 and num2. 

And now again, TypeScript saves our --. 

This is the bug I mentioned earlier, which would be easy to introduce. 

You get the value entered by the user. 

And since user enters numbers here, you expect that you get numbers here. 

But value actually always returns a string here. 

That's the return type of this property. 

It's the type of value stored in this property. 

And this is always under all circumstances, a string. 

Now here we need numbers. 

So here, the fix is easy, we converted this. 

But now we are forced to make that conversion and we can't forget or overlook
it. 

And that's all TypeScript is about in a nutshell. 

We are forced to write cleaner code. 

Well, and then I can console log the result here. 

With all of that, let's again run TSC app.ts, this compiles to code. 

If we have a brief look at the code, you'll see the -- operators gone, all the
types are gone. 

So does this JavaScript code we could have written on our own, but this is no
code which was checked in advanced during development here in our TypeScript
version. 

And now if I reload here, and I enter five and 11, we get 16 and not unintended
115 or 511, because now we were forced to add this type conversion here. 

---