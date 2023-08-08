## 496. TypeScript Setup

<strong><em>no description</em></strong>

<v Tutor>So let's see how that types thing works.</v> For that, let me create an
index HTML file with a base HTML skeleton like this and in there, I'll not spend
too much time on the styling. 

I'll simply add an input of type number, and a another input of type number, and
a button where I say add. 

and when we click this button, the two values entered into these two inputs
should be added up, and should be output in this paragraph below the button. 

Now again, this will be a very ugly and simple page, but it's about TypeScript
here. 

Now let's add a little app.ts file, .ts because we're going to write some
TypeScript code in there. 

Now we need to install the TypeScript compiler. 

Now with Deno we didn't need to install it but now we do need to install it. 

Because we're not going to execute this code with Deno , I want to execute it in
the browser instead, and as I mentioned, the browser doesn't run TypeScript. 

So we need to convert TypeScript to JavaScript, and for that, we need to
TypeScript compiler. 

As a side note, Deno also needs to convert it, there decompiler, the TypeScript
compiler is just built into Deno. 

But we can install the compiler standalone by following the instructions we find
on typeScriptlang.org, and the instructions are very simple. 

In the terminal on our system, we run npm install - g typeScript, and on Mac and
Linux, you might need to add sudo in front of this to get the right permissions.


Now, the npm command will only work though, if you installed Node.js. 

So make sure you do that first and from nodejs.org ,you simply install the
latest version. 

This gives you an installer both on Mac OS and Windows. 

You can walk through the installer and once installation finished you'll be able
to run this npm install command. 

If you do so, you might be prompted for your password, and then after this,
we'll install TypeScript. 

The TypeScript compiler globally on your system. 

and once it is installed, you can always run tsc , which is a command which now
is available, and then the filename you want to compile , and this will convert
this file to a JavaScript file, which is why you now also see app.js, and it's a
JavaScript file, which I'm now going to import here, into my HTML file, app.js
and I'll add to defer to make sure this only executes once the entire body has
been parsed. 

But now we're not going to work in app.js, but we're going to work in app.ts. 

Now when working with Deno, you won't see those js files because they are
generated and stored behind the scenes you could say. 

We only see it here because this is a very basic project where we control
everything on our own with help of the compiler. 

So now in app.ts, let's add this add function here, num1, num2, and return num1
plus num2 like this and then First of all, we can call it of course, as I showed
it before, with strings, and with numbers just like that. 

Now if I save this, and I compile this again, we can open this page in the
browser by simply opening this HTML file, and now to see something in the
console here, we just have to log our results here. 

So console.log the result here, and console.log the result here. 

Once we do that, let's recompile this. 

Reload, and we see seven and 16, and that's the same behavior we saw before. 

Now, where does TypeScript now help us? 

---