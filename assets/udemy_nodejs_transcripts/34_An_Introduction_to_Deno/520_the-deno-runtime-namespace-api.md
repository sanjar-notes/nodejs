## 520. The Deno Runtime (Namespace) API

<strong><em>no description</em></strong>

<v Narrator>As mentioned, when you're working with Node,</v> you have these core
Node modules here. 

for example, a module for working with the file system. 

and with Node, you simply import such a module, and then you can start reading
or writing files for example. 

As you learned in the modern Java script with Node module, you also have a
promise based API version available for some of these core modules. 

Now for Deno, we have a similar concept. 

There we have this so-called runtime API here, also sometimes called the
namespace APIs. 

These are core APIs, core features, which are built into Deno, and which are
available on a Deno object, which in turn is globally available in any Deno code
you're executing. 

And here you got core modules for working with files, for working with requests.


You also got core features like set timeouts, set interval, clear timeout. 

You have to fetch API available for sending network requests. 

And that actually by the way, is a difference compared to Node already. 

In Node, You also have some core APIs available, some core features available,
either after importing them from the respective core module, or things like set
timeout also are globally available in Node scripts, but things like the fetch
API are not available in Node because Deno has the core philosophy of being as
browser compatible as possible. 

That means that any code that could run outside of a browser is also supported
in Deno. 

Something like the fetch API for sending HTTP requests. 

This is a available in Deno because this is not strictly tied to a browser. 

Of course we can send a fetch request at HTTP requests from any Java script. 

Now, of course, there also are other features, for example, related to writing
files, which exist in Deno because Deno runs out sort of a browser, but which
wouldn't exist inside of a browser. 

And there are features which we can use in a browser, for example, features to
interact with the browser Dom, which are not supported in Deno. 

Also not supported in Node of course, because there we have no Dom there we are
not running inside of a browser. 

So that's how you can think about these core APIs. 

It's basically what you can do in the browser minus features that only makes
sense in the browser plus features that can't be used inside of the browser that
can be used outside of it though. 

Something like writing files. 

And with that, I say, we talked about this enough, let's now write some Deno
code, and let's see how we can utilize these built-in core features. 

These namespace API features. 

---