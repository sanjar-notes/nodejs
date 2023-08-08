## 513. Wrap Up

<strong><em>no description</em></strong>

<v Instructor>And that's it for this module.</v> Now we learned how to use
TypeScript together with "node.js." And that can really be an amazing
combination because TypeScript adds many useful features which simply allow us,
as a developer, to write better less error prone code. 

Which has a lot of built in checks during compilation and during development. 

Which avoids errors at runtime, when we then execute our code. 

It is important to understand that node itself is not able to execute TypeScript
code. 

So the code we write in the source folder here, is not directly the code we're
going to execute. 

This is just our source code. 

To execute it, we need to compile it first and we do that with the "tsc"
command, which invokes the TypeScript compiler in this project, thanks to the
"tsconfig.json" file and of course adhering to the configuration we set up in
this file. 

This generates the "dist" folder and it's now the "dist" folder that holds the
code, which we want to execute. 

So in "package.json" if I would wanna add a script that runs my node server, I
would add a "start" script in there, where I run "node dist/app.js". 

And now we could run "npm start" to speed up that node server based on our
compiled JavaScript code. 

Now whether you wanna use TypeScript or not is entirely up to you. 

You absolutely don't have to and as you saw throughout this course, I used just
JavaScript. 

I would argue that probably the majority of node expressed projects use just
JavaScript. 

But you see how easy it is to use TypeScript as well. 

And if you like TypeScript, if you like this syntax, if you like the features it
has, definitely consider using it. 

It's super simple and in the end you get a regular node expressed JavaScript app
of course just with the extra TypeScript features during development. 

Now what you'll learn throughout the course about validation, authentication,
databases, error handling. 

That all applies to this application as well. 

You see it here, we write the same code we wrote over and over again throughout
the course. 

The only difference is the extra TypeScript syntax which we can add. 

Extra TypeScript features like type assignments or type conversions which act as
extra type safety, TypeScript is all about. 

But that's east to add to the existing code. 

So you don't need to learn a new language and you don't need to use libraries in
a new way. 

You use everything as you learned it throughout the course just if you want to,
with the extra TypeScript features. 

---