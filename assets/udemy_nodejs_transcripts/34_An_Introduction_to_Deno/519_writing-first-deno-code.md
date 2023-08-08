## 519. Writing First Deno Code

<strong><em>no description</em></strong>

<v ->So I'm gonna brand new empty project here,</v> an empty folder, open up in
Visual Studio code, the IDE I'm using here. 

And in there, we're going to write some first Deno code. 

Now, here's one important disclaimer, one important prerequisite, you should not
dive into this module right away. 

I do expect that you went through the node course first, maybe not through all
sections there, but definitely through all the basic sections, so that you know
why we use node, how we write node code, how we can spin up a node web server,
so that you know about the Express framework. 

All that knowledge is required for this module, because I'm teaching Deno for
people that already know node, at least a bit. 

That's important. 

In addition, I mentioned that with Deno you will be able to execute TypeScript
code Therefore, it will help a lot. 

If you went through that TypeScript module in this course, first, that's just
another node. 

Also check out the modern JavaScript with node module first before you go
through this module. 

With that all out of the way, though, you should have an easy time following
along. 

And therefore let's write our first Deno code. 

Now, as I mentioned, it's up to us whenever you want to write this code with
JavaScript or with TypeScript. 

But since steno does support TypeScript, and since this is a core difference to
note that Deno has this built in TypeScript compiler, and we don't need to
compile the code ahead of time. 

Since that is all the case, let's write some TypeScript code. 

And hence here I'm adding an app.ts file. 

The name is fully up to you, though, I'm just using .ts because I will write
some TypeScript code in there. 

And here, our first basic Deno code could be code that we can almost run like
this with node js As well, I'm going to define a message variable, which will be
of type string. 

So this is how I assign a type with TypeScript, I'm making it clear that this
should contain a string eventually, then I'm assigning such a string value. 

And then I console log it. 

Now it's needless to say that we could have merged these two lines of code into
one line. 

But I want to show you that we can use TypeScript features here. 

That's why I'm going for two lines. 

Now, this is no fancy app. 

This is no web server. 

But this is some code, which we will be able to execute with Deno. 

So with that saved, we can now open up the terminal. 

And here I'm using the one integrated into the IDE. 

And we can execute our app.ts file with Deno, however, not with just Deno and
then the file name, but instead with Deno, run app.ts. 

So that's a difference to note with node with just execute a file with node and
then a file name, with Deno, it's Deno run, and then the file name. 

Other than that it's quite similar though, this will now execute this file with
Deno. 

And you see, first of all, it compiles to code from TypeScript to JavaScript,
you could say. 

And then the we ate JavaScript engine that is wrapped by Deno goes ahead,
executes the JavaScript code, and therefore prints Hi there. 

So this works. 

If I run this again, by the way, you will notice that the compilation step is
skipped, because it caches the compiled code. 

And if you didn't change the code at all, it will just reuse that already
compiled code to run the script again. 

So this is now a very simple first app, if we want to call it an app, which we
can execute with Deno. 

Arguably not too fancy, but a nice start. 

Now before we start writing some web server code with Deno let's see what else
we can do. 

Let's see what is baked into Deno. 

Because for node, if we dive into the node API docs, we have all those core
modules that are built into node. 

Now let's see if there is an equivalent for Deno. 

---