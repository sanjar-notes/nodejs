## 522. Working with Deno Permissions

<strong><em>no description</em></strong>

We wrote some Deno code, but when we wanna execute it, it compiles, but then, it
does not execute, but instead fraud is error. 

And this is not a bug with Deno, and this is not an error in our code, instead,
this is a Deno feature. 

Remember that third feature, which I advertised earlier in the module, Deno is
secure by default. 

What does this mean? 

It does not mean that Deno code that we write, is more or less secure than node
code. 

It's us who write the code, and we as a developer, we can write good, and we can
write bad code. 

So just because we use Deno does not mean, that our code is always secure. 

We can still open up security holes, when writing Deno code. 

This means something else, it means that when we run a script with Deno, that
script does not by default, have all possible permissions. 

For example, something like reading or writing files, or sending network
requests, or listening to network requests. 

These are all operations, that are always unlocked and possible with node, any
node script can do anything. 

When you execute a JavaScript file with node, that file is able to do
everything, it could delete all files on your system, and nothing would stop it
from doing that. 

Therefore, when you execute code with node, you have to trust that code, either
because you wrote it on your own, or because it's some third party library,
which you trust, because code could potentially do a lot of bad things. 

With Deno, there's a different model, that's being used. 

Deno by default, is not allowed to do everything. 

Instead, by default, it must not do a lot. 

By default, when you execute code with Deno, that code may not write to files,
that code may not read files, and it may not send or get HTTP requests. 

So therefore, here when we try to write to a file, this is denied by default, as
part of Deno's security model. 

By the way, I keep on saying Deno, as I mentioned earlier, you could say Dino,
it probably would be the more correct term, I simply got started with Deno, and
I can't get rid of it Sorry. 

Anyways, that's not part of, Denos security model, so, here when we do want to
write a file, we have to set the appropriate permissions, we have to let Deno
know, that we want to be able to write to a file. 

And we do this by running the script, but not just like this, but instead before
we specify the file name, we can add extra flags to this execution, and we can
set some security specific flex, some security specific options, and there is
the dash dash allow dash right flag. 

If we execute this code, with this flag, then we do allow app ts to write to
files. 

There always allow read flag to do the opposite, you can also narrow this down,
you can provide an optional argument, to allow right to make it clear to which
files, this app may write. 

Here for example, I could allow writing to message dot txt, and I could add more
files, separated with a comma. 

But our files could not be written to, So that's up to you. 

But if we execute the code now, for example, with this flag with this option, if
I hit Enter, now you'll see it executes successfully, it prints out this success
response. 

And here's our text instead of message or text. 

So this is how Deno, whatever you wanna name it works, you see, it's not too far
off from node, it has this core difference besides the fact that it supports
TypeScript, of course. 

Now we'll dig deeper into Deno, and we'll write more code with it. 

But before we do that, to have a comparison, let's write the exact same script
with node. 

Definitely try this on your own. 

First, we'll do it together in the next lecture. 

---