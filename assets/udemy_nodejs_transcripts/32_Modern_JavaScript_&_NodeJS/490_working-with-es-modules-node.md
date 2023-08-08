## 490. Working with ES Modules & Node

<strong><em>no description</em></strong>

<v Instructor>With that I got a simple</v> starting project for you. 

Here you'll find it attached to this lecture. 

There, we got a packaged up json file, where I simply installed express. 

We've got the app.js file where I'm importing express, where I'm also importing
the core file system module that's part of node.js, and where I then create a
very simple express application that does just one thing. 

For incoming get requests it reads this my page HTML file, which contains some
HTML code and it returns the content read in from that file with the sent method
back to the client. 

So if we now run this application by running the app.js file and we visit
localhost 3000, we'll see the content often as HTML file on the screen. 

Definitely not a very fancy application, but it's not about the content here or
the application. 

It's about those new features, which I want to show you, and let's start with
the ES modules feature. 

Here we are using the import syntax you're used to. 

We're importing with the require function. 

Now, let's also quickly see how we export it, thus far. 

If I would create a new file here, response-handler.js, for example, and I take
this function here and cut it out of the app.js file and define it in there,
resHandler equals this anonymous arrow function here. 

I could export it with module exports pointing at resHandler or storing
resHandler to be precise. 

And I'll back it app.js. 

I can import my file, the resHandler here with require and then dot slash
response-handler omitting the file extension. 

We should now also bring the file system import over to the response-handler.js
file by the way, because I'm using default system in there. 

But that's how we could restructure this to also export something on our own. 

Now, of course, we just need to register the response-handler function here on
the get middleware. 

Now that's the import and export syntax you are used to that what we used many
times throughout the course and of course this works if we restart the server,
we can still load this page. 

Now, how can we switch to the more modern or this alternative new syntax? 

Well, let's have a look at the official docs. 

There's one important thing I wanna draw your attention to though. 

You see the stability is experimental at least at the point of time I'm
recording this. 

This means that the exact implementation could change. 

It also means that you should reconsider whether you want to use this in
production or no. 

That is the reason why the vast majority of projects don't use the syntax. 

You can use a dope, it should work and it is definitely worth a closer look
because you'll see pretty much the same import export syntax on the client side
in the browser if you were building applications for debt, hence whatever you
learn here will also be useful for browser side JavaScript code. 

Or if you already learned about ES module there, it'll be easy to get started
with them in node projects. 

Now, how do we get started? 

To get started we first of all need to enable this syntax and there, we got two
main ways. 

We've got three ways, but we can ignore the third one for now. 

One way of using these imports is that we rename our files from dot js to dot
mjs, where the m stands for a module. 

We could do this and if I renamed us here, I can now import it with this new
syntax, but I'll not use this approach. 

So let's revert this back. 

Instead the second alternative is that we keep dot js as a file extension, which
I'd like to do here and instead in the nearest package dot json file, we should
make sure that the type property or the type configuration is set to module. 

So if we dive into our packaged dot json file here, we see that there is no
type. 

It's not this type here by the way. 

We can remove does actually there should be a main type node or property here
instead, and there is no such property. 

So let's add type here and set this to module. 

Like this. 

With this, we can now use ES module imports. 

Now in app.js, let's start with importing express. 

If we want to import express now this syntax here, which I'm going to comment
out, changes to import express from express like this. 

That's the ES module Syntax for importing something. 

If I saved this and then I'll run this file again, you'll see it crashes it
crashes because I'm still using require on that other import here. 

Now, since I set my type two module, we have to use the new import export syntax
everywhere. 

So here, I'm also going to comment this out and now I want to import resHandler
from dot slash response-handler. 

This would not work however, because we're using the wrong export syntax. 

If I now save this and rerun, you'll see it runs with an error. 

We need to go to the file and change the way we export. 

Instead of exporting with module exports we now use the export keyword, which
exists in modern JavaScript, and we export it to response-handler. 

However, we can't use it like this. 

Instead, we now either have to add it a right in the line where we define the
function or the variable which we want to export or we use exports default. 

So this variation of the export down there. 

Now I'm going to use export default here because otherwise this import wouldn't
work here. 

If you use the other approach this import wouldn't work here and I'll come back
to the other approach in a second though. 

With that, however, with the default export here and the change to import here,
if we now restart this, it still fails and the reason for that it's the
extension. 

Now here, we do have to add it. 

We do have to add dot js here, not for third party modules, but for our own
files, we have to add it. 

So here I add dot js. 

and now if a restart this, I get another error. 

The require import in response-handler, of course, this doesn't work anymore. 

We also need to replace this and import fs from fs like that. 

With that now is saved. 

If I now started, now it works. 

We get no error and we can now visit this page again. 

So this is now simply an alternative and it's up to you, whether you prefer
this, it is however the import-exports index, you know, from the browser and
that alone might make it a bit more attractive. 

Nonetheless, as I mentioned, switching is not mandatory, it's optional. 

I also mentioned another exports syntax. 

Now that other syntax looks like this. 

If we have multiple things that we want to export, we can't use export default
because that is only usable once per file. 

So if you got only one thing you want to export, you can use it. 

If you've got multiple things, you can't use it. 

A little bit like module exports, we can also only use this once and if you have
multiple things, we need this exports dot syntax if you remember. 

Here it's the same, we can export one thing with a default, but we can always
export one but all the multiple things by adding export right into line where we
define the variable or constant that we want to export. 

Now, when we use this approach however, when we don't use default, we have to
change our import syntax. 

Instead of importing like this, we now have to remove this name here and use
curly braces instead, and between those curly braces, you repeat the name of the
constant or variable or whatever it is, which you want to import. 

So in this case, because I named it the resHandler here, I now do use resHandler
here. 

With the default export, the name was actually up to you. 

You could have also just named deresh or whatever you like. 

With a named export, so where you have the export keyword right in the line
where you define a constant or variable, the name is no longer up to you. 

Now you need to curly braces and you need to use the exact name of what was
exported then. 

With that, however it again works. 

And as you can tell, the third party libraries we're using here, express and the
core fs module. 

Those seem to use default exports under the hood. 

Otherwise this way of importing wouldn't work. 

If we now reload it, of course still works. 

So that's simply an alternative syntax for exporting and importing and in your
files, it's of course totally up to you, which syntax you prefer. 

---