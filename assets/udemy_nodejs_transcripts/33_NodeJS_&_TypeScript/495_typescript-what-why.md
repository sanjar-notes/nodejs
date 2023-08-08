## 495. TypeScript: What & Why?

<strong><em>no description</em></strong>

<v Instructor>So, what is TypeScript</v> and why would we use it? 

TypeScript is a superset to JavaScript. 

That simply means that it extends JavaScript. 

It builds up on JavaScript. 

And unlike JavaScript, TypeScript does not run in the browser. 

Instead, TypeScript has to be compiled to JavaScript so that it runs again. 

Now, why would we then work with it? 

Because TypeScript gives us, as a developer, a better development experience
because it adds certain feature to the code which only exist during development,
but which still help us write better code and avoid unwanted errors. 

And here's an example. 

This is a function, this is some code where TypeScript can help you. 

Now, what could be wrong about this? 

Let's simply try it on our own. 

For this, you can simply open up your developer tools in Chrome, for example,
and there go to the JavaScript console. 

In there, you can also write some basic JavaScript code which will then be
executed here in the browser. 

And, for this simple example, that's all we need. 

So, in there, let's define a function now. 

A function which is named add and which takes two parameters, num1 and num2. 

Then, let's add curly braces, and now place your cursor between these braces and
hit Shift + Enter. 

This will then simply add a new line. 

Now, inside of that function, we can return the result, num1 plus num2, just
like this. 

So, that's a very trivial function for adding two numbers. 

If you now hit Enter without Shift, this code will be committed, it will be
saved, and now this add function exists here in the console. 

Hence, we can now call add with one and five and get back six. 

Seems to work. 

What if you would pass in one and five as strings though? 

Then, you get back the string 15. 

So, one and five are then concatenated to one longer string instead of being
converted to numbers, and then added as numbers. 

Now, the reason for this is that this is simply how JavaScript works. 

If you have an operation with a plus and at least one of the two operands is a
string, then both will be combined as strings, essentially. 

That's how JavaScript works. 

And this, of course, can be a problem here. 

Now, you might think that this is a unrealistic scenario because why would you
call the function with two strings? 

Well, imagine that you have two inputs in your page. 

Two inputs where you fetch some user input. 

Now, you should know that whatever data you extract from such inputs is always
extracted as text in JavaScript. 

So, even if the user entered a number in an input on your page, if you extract
that data with JavaScript, it'll be a string. 

Now, you can always convert this to a number, of course, but if you forget this,
and you pass the unconverted value to this function, you might get this
unintended result. 

Now, that's where TypeScript can help us. 

To avoid such a unwanted behavior which occurs at runtime, so when our code
executes, we can use TypeScript. 

Now, of course, we could also avoid this behavior at runtime with JavaScript. 

We could add an if check, for example, to see whether the values we received are
strings or numbers. 

That is something we can check with JavaScript, and this would allow us to avoid
such mistakes, but, of course, that means you have to write extra code at
runtime to make sure that your code works when you actually could avoid this
during development if you had strict type checks. 

So, if you simply could tell JavaScript, so to say in advance which types of
data you want, and then JavaScript and your IDE could warn you when you have
some code in your program where wrong types are fed in. 

And that's where TypeScript helps us. 

It adds strict typing. 

In general, TypeScript adds a bunch of features to JavaScript. 

It adds the types, and that's the most important addition. 

That's where TypeScript's name comes from. 

But it also unlocks certain next-generation JavaScript features, which we then
can use in our code without any extra tools like Babel. 

It also adds some non next-gen features, so some features which don't exist in
JavaScript at all, which help us write cleaner code. 

Now, all these features are stripped away once it's compiled, but during
development, those features can help us write cleaner code. 

It adds meta-programming features like Decorators. 

It has rich configuration options that allow us as a developer to fine-tune how
code should be compiled. 

And it, in general, simply gives us a lot of modern tooling and integrates
greatly into modern tooling to give us a great development experience. 

Now, in this basics refresher here, I'm not going to dive into all these areas
in great detail. 

For that, you can check out my Understanding TypeScript course. 

This course dives into TypeScript in great detail and walks you through all the
core features. 

So, that's my recommendation if you wanna learn all about TypeScript. 

Here, we're going to dive into some core basics. 

And, for that, let's actually come back to this example I just showed you now in
the context of, at least, a little bit more realistic webpage. 

---