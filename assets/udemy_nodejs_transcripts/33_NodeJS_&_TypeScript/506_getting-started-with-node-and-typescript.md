## 506. Getting Started with Node and TypeScript

<strong><em>no description</em></strong>

<v Tutor>So we get our app.js file,</v> we get these configuration files. 

Now it's time to convert this to a TypeScript file. 

For this we can change the extension here to app dot ts, and now we can use
TypeScript features in here. 

But automatically, you see that I'm getting an error here cannot find name
require. 

Now, we also thankfully get a suggestion on how to fix this. 

You need to understand that this require method is only available when we're
running this code with Node. 

If we would want to run it in the browser, this does not exist. 

Now TypeScript does not know where we plan to run this code, and my IDE has
built in TypeScript support and therefore it detects that TypeScript will not
know whether it exists or not. 

So to let TypeScript know that this exists, we can simply run npm install dash
dash save dash dev to install something as a dependency that's only used during
development at types slash node. 

Now this at types thing here is important. 

On npm, you will find many at types packages. 

These are packages which provide TypeScript translations for JavaScript features
you could say. 

They contain code that allows TypeScript to understand a certain library, a
certain package or a certain commands, and with at types node, the thing is that
if we install it, we can use Node.js specific syntax in our TypeScript files,
because this dependency will provide TypeScript with the translation of this to
JavaScript, and in this case, it will just let TypeScript know that this
function here will exist because we're building a Node application you could
say. 

So we can hit enter here and this will now it install this package, and you see
the error is now gone. 

The reason for that is that if we dig into this types node folder, here in the
end, we got a dts file, we get a bunch of dts files actually, which provide all
these core node modules translated to TypeScript, and it's really just
translations from TypeScript to JavaScript. 

So here you don't find the entire node code re-written in TypeScript. 

Instead, these are really just instructions which TypeScript is able to
understand so that it knows how to convert your TypeScript code to valid
JavaScript code. 

In this example here, it would simply keep the code as it is because it would
know that this code is valid JavaScript code if executed with Node. 

Will use more of those at types packages. 

Because for example with Express the thing is, if I add a dot here, I get no
auto completion. 

My IDE doesn't know that I can listen on the app here on this app object. 

Now that's not horrible, our code would run. 

But it would be nice if we would get this extra support by the IDE. 

So if TypeScript would understand that we have a listen method. 

This would also ensure that we can't pass in invalid data. 

For example, if we think that listen works like this, and it wants an object
with the port here, then this is an error we might wanna catch, and currently,
if I run tsc here to compile all files, this compiles just fine. 

Because TypeScript does not understand how this listen method looks like, which
arguments it wants and how it works, and because of that, it just accepts this
code. 

Now we can make TypeScript aware of the express package just as we made it aware
of the node runtime in general by installing another types package with npm
install dash dash safe dash dev at types, and now it's slash express, and for a
lot of popular third party libraries, you will find such types packages. 

We find it for Express, but you essentially find it for all major libraries out
there. 

There are TypeScript translations available for all major JavaScript libraries
always under this at types slash, and then the library name package. 

So for now, it enter this installs to types to type definitions for the express
library. 

Now that alone won't do the trick though, as you can tell, I still don't get an
error, I still don't get auto completion. 

Because installing the types like this is not enough. 

It was enough for a Node which is our general code we're writing. 

But it's not enough for this third party library which we're importing like
this, and the import syntax is the problem. 

By default, TypeScript is tuned for web apps running in the browser, and they
are this import syntax would not be available. 

So that's not the default import syntax it expects when it comes to combining
multiple files. 

We can change the expectations by TypeScript in a tsconfig.json file. 

Their module should indeed be set to commonjs. 

But also add the module resolution config and set this to node here, and while
we're at it, let's also change the targets to es six so that we compile our code
to more modern JavaScript, which Node.js is capable of executing. 

Now with that, let's go back to app.ts and all the change code in one little
other detail, and that's here for the import. 

Instead of this import syntax, write import express equals require express or
alternatively, you can now also switch to another import syntax, which normally
is not supported like this in Node.js, you can import express from express. 

Now this is a import syntax you know from the client side, you know from the
browser in the end. 

This is how you typically import files from other files into this file in client
side code. 

In Node.js, by default you use that require syntax. 

Now with TypeScript, you can enable this syntax and TypeScript accepts this
syntax. 

But if you then compile your code, if you run tsc, you will see that in the
result in the end does looks quite different. 

But in the result here, it still uses require. 

Now it also transferred this code in a couple of other ways. 

But that's just some internal stuff that it does. 

It still uses require in the end here. 

But we can write code like this. 

Which is especially nice if you're coming from the front end, and you're used to
this import syntax. 

Now, of course, in the modern JavaScript feature section, I showed that this
import from syntax is also supported by Node.js natively even if you're not
using TypeScript, and that's true, and I showed you how to enable and use it
there in that separate course section. 

But please note that here, I didn't change the package json file to enable this
import syntax, as we did have to do it in that other course section, and with
TypeScript here, and that's something you'll see throughout this section, we
will also still be able to omit file extensions for example, and other
difference to the baked in modern import export syntax. 

I've written that it's pretty similar though, but the difference that you need
to understand here essentially, just instead here in TypeScript we always can
and actually should use this import from syntax, and it is then still compiled
down to that require import syntax node uses by default. 

So there will be a difference between the code we write and decode that will
actually run on the server, and with that, you now see that if I type a dot
here, I do get auto completion, and now we also get help regarding the arguments
we can pass to listen, and now for the argument, we see that indeed listen has
this handle argument which it accepts which can be typed any, and therefore it
doesn't yell at us here. 

But we can also see if we add lists and for the first time that there are
various ways of calling it we can cycle through these different ways here with
the arrow keys, and that it typically one support which is a number. 

So it gives us this hint here, and that's some extra help we get in the IDE
because we're using TypeScript. 

So here, I can then enter 3000, and have valid code, and this extra IDE support,
which we get thanks to TypeScript, as well as this import syntax which might be
preferred by some developers since we're used to data import syntax from the
client, these are already some advantages we get from using TypeScript. 

Now with that out of the way, I promised you a simple REST API built with Node,
Express and TypeScript. 

So let's now continue working on that. 

---