## 524. How Deno Features Are Organized

<strong><em>no description</em></strong>

<v Instructor>So we got started with Deno here,</v> we wrote some first basic
Deno code to get good IDE support. 

Again, I'll switch back to the extensions. 

And there I'm just going to enable my Deno extension again here. 

And with that done, we can continue with development here. 

Let's now dig a bit deeper into Deno. 

And for that, it's important to understand how Deno code and features are being
organized. 

We get those core APIs, the so called Namespace APIs. 

Which are built-in core functionalities, built-in utility functions as well like
set timeout, like right file, so all these core APIs, which you can see here in
those docs. 

These are core APIs built into Deno. 

Now, we also got the Standard Library, which is a set of modules which you have
to import into your files in order to use them, but which are still being
maintained by the Deno team. 

And then we got third party libraries which are maintained by the community. 

Now, the Deno Namespace APIs are stable, so they shouldn't really change
anymore. 

And they are maintained by the core team. 

The Standard Library modules are also maintained by the team. 

But they're not necessarily stable. 

They're some things some features could still change. 

For third party libraries, as the name suggests, those are maintained by
different community teams, not by the official Deno team, and therefore their
stability and maturity also differs. 

Some libraries are very new, some libraries are heavily maintained and might be
quite stable. 

Now the Namespace APIs are built into Deno, no installation, no imports are
required to use those features, as you see here, with our right file extension. 

And that, of course is a difference compared to the Node core APIs. 

For those core APIs like the file system API, we of course needed to add an
import to use it. 

That's a difference for these core Deno features, no import is needed. 

But if we then move a step further towards the Standard Library, we will need to
import those modules in order to use them. 

We still don't need to install anything. 

But as you will see, installation is not really a thing in Deno scripts anyways,
but we'll need to import those libraries to use them. 

That brings up the question, what is the Standard Library? 

And what's the node equivalent? 

Well, we can find out more about the Standard Library on the Deno page,
Deno.land, and then there you find the Standard Library. 

And these are simply a bunch of packages, which in the end build up on the core
APIs. 

And make certain things easier to use. 

You could build any kind of app with just a core runtime API. 

But it gets easier if you use some Standard Library modules, or even also some
third party modules, which build up on those core APIs to make certain things
like listening to incoming requests easier. 

And that's the whole idea. 

The Standard Library builds up on those core APIs and makes working with those
APIs easier, you could say. 

Third party libraries have the same idea. 

There you also don't need to install anything, but you need to import them to
use them. 

And they also build up on the core APIs. 

So those Namespace or runtime APIs are built into Deno. 

And they have a small set of low level core functionalities with which you could
build everything, but doing so would be cumbersome, that's why we have the
Standard Library and third party libraries. 

The third party modules that build up on those core APIs to make the integration
of certain features easier. 

And therefore, let's now make the next logical step. 

And let's start using some Standard Library features, as this will also cover
one important aspect of Deno. 

It will show you how we integrate our modules into our Deno code. 

---