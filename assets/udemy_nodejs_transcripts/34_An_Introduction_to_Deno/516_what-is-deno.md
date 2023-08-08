## 516. What is Deno?

<strong><em>no description</em></strong>

<v ->So, what is Deno?</v> Deno is a JavaScript runtime based on Chrome's V8
JavaScript engine. 

And if you think about that sentence, if you read it, it might sound quite
familiar, that's the same thing Node.js is. 

Node.js also is a JavaScript runtime based on Chrome's V8 JavaScript engine. 

So, is Deno the same thing? 

Well, let's see. 

Deno, since it is that JavaScript runtime, allows us to run JavaScript outside
of the browser, just like Node. 

But now there are a couple of key features in Deno, which don't exist like that
in Node, for example, Deno is not only a JavaScript runtime but actually a
JavaScript and TypeScript runtime. 

Now I do have a whole module, where I show you that you can use TypeScript with
Node.js as well. 

The key difference is that for Node, Node itself, the Node executable is only
capable of executing JavaScript code, TypeScript code needs to be compiled to
JavaScript code first. 

Deno on the other hand is also an executable, which is capable of executing
JavaScript code, but it's also capable of executing uncompiled TypeScript code,
because Deno has its own built in TypeScript compiler. 

Now, in addition, Deno supports URL imports out of the box, and modern
JavaScript features like promises are embraced. 

Now, I do you also have that module, on modern JavaScript with Node and there
you learn that you can also import in a different way than used in the majority
of the course and that you can use promises for example, on some of the built in
features but unlike Node, Deno embraces this concept out of the box from very
start simply because it's newer than Node. 

There also is something about these URL imports that differs significantly from
how you manage dependencies and Node projects, but I will come back to that
later. 

And last but not least one other key difference and one other key feature of
Deno is that it's secure by default. 

Now, if you read it like this, this sounds horrible, right? 

It sounds like Node is not secure, and that's not the case. 

I'll come back to what I mean with secure and which specific aspect this is
about throughout this module, and you will see that it's not that horrible, but
that it still might be a nice feature to have. 

So let's maybe now get started with Deno, let's write some code so that we get a
feeling for it and let's then step-by-step find out what the differences are
compared to Node how you can build apps with Deno, and in the end, let's find
out whether you should switch. 

---