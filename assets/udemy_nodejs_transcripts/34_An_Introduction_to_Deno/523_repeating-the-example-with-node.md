## 523. Repeating the Example with Node

<strong><em>no description</em></strong>

<v Instructor>So we get this first basic script here,</v> which we executed with
deno. 

Let's now write the same code in our app js file for node. 

So I wanna store some text in a file. 

How does this work? 

Well first of all, I'm setting up my text here, and then in node's world, I need
the file system core module. 

We import this with the require syntax. 

So from the fs module we import the file system. 

Now here by the way, I'm getting an error that fs is a module that's not being
found. 

That's of course incorrect. 

And for me to fix this to temporarily disable my deno extension. 

You might not need to do this. 

I need to do it here, so I will disable it and reload the project and thereafter
this will work here. 

So now I got the file system here. 

Now to write to a file, we also got a write file method here, the writefile
method now also wants a path which in the simplest form can just be the file
name. 

And then it wants the data that should be written. 

One core difference compared to deno for this specific method here, is that the
data could be just a string though, that we can also pass in such a bytes array,
but that it also just can be a string. 

So here we could have to node-message.textfile, and we just pass in the text as
a second argument. 

Now one crucial difference is that write file, like this does now not return a
promise, but that instead we pass in a callback here to have some code that
executes once this completes or that tells us about a potential error that could
have occurred. 

However you learn that you can access dot promises here to then have the promise
based versions of those API is available, and now write file would give you a
promise. 

So you can always get a modern feature like a promise here, and to have the best
possible comparison I'm going to use that. 

So I'm going to import the file system from the promises part of the file system
core module, and therefore now here writefile gives us a promise. 

Hence this function will execute once writing to a file finished and therefore
here I can console log wrote file. 

And now we can save the file and execute it. 

And for executing it with node, all we need to do is run node and then the file
name. 

So the command is just node and the file name and then that's probably the most
striking difference. 

We now don't need to specify any permissions we wanna assign to that execution
process. 

Instead by default as I mentioned before, node scripts, scripts executed with
node by default, have full read and write access. 

They can do anything. 

And that of course can be an issue because if you're running a script from a
source which you don't know, you have to trust that script or analyze all the
underlying source code to make sure it's not doing anything harmful with denon
that's not the case. 

There if you execute a script, you can rely on it only being able to do the
things you do allow it to do. 

Of course if you're executing some third party script with deno, you still might
have to scenario that this script needs write permissions to do what it does and
well you then again have to trust it that it won't abuse those permissions. 

Anyways, if we now execute this file, you see it does finished successfully and
it writes our message to the node message text file. 

So this is now the node equivalent of this code, using some modern node feature
here, but otherwise achieving the same result. 

So the key difference here really is just typeScript, which has built into deno,
and of course that permissions thing. 

---