## 521. Using the Runtime API

<strong><em>no description</em></strong>

<v Instructor>So let's get started</v> with these core Deno features. 

So let's write some Deno code, and for that in apt.ts, I'm going to delete this
simple code. 

And now instead, I want to store some text in a file, let's say. 

So a very trivial application. 

So we got some text. 

This is a test and it should be stored in a file let's say. 

Of course, this could be some text, which we got from the user input. 

And I want to store this in a file now. 

For that we have the globally available Deno object. 

Now, if I just type it like this, you see my IDE is not liking this. 

Now this code will run, not like this, but as soon as I access something on
Deno, but it would be nice if my IDE would also understand that Deno code will
work. 

If it would understand that there is this global Deno object available. 

And to help my IDE, to help which will still code with that, I recommend that
you go to View, Extensions and there search for Deno, and you'll find Deno
extension, which you can install, which will bring Deno support to visuals to do
code. 

Once you install and enable this, you can go back to the Explorer and now you
will see that on this Deno object, you get all the completion. 

At least you should be getting this now, and this of course yields a better
development experience. 

Of course, just to make it is clear again, this Deno object and all the methods
we can access on it is only available if we then later execute this file with
the Deno executable, not if we would execute it with node or anything else. 

So this Deno object here is really only available if that script later gets
executed by Deno, otherwise it'll not be available. 

Now our goal was to write a file. 

So conveniently there is a writeFile method, which we can call. 

And as the name suggests, this is a method that helps us write to a file. 

There always is the writeTextFile method, which makes writings on text to a file
even easier, but to see more Deno features in action, I'm going to go for
writeFile. 

Now, writeFile wants two main arguments here, it wants a path to the file,
including the file name and the data that should be written to the file. 

And the data should be a Uint8Array, which is a strange data type, but which is
actually a core data type built into JavaScript, which in the end is an array
full of bytes, you could say. 

Now, we will be able to convert our text to bytes. 

So it's no problem that we have no bytes right now, but that we only have a
string. 

Let's start with the first argument, the path. 

And here let's say we wanna create that file in the same folder. 

Conveniently, the only thing we then need to do is specify a file name. 

So here I'm going to create my message.TXT file. 

The second argument should be the data that we wanna store, and that should be
this byte array. 

Now, actually here this preview snippet gives me an idea on how we can convert
the string to such a bytes array. 

We simply create an encoder by instantiating a new text encoder that is a
globally available feature in Deno. 

If we go to the Deno docs and we search for text encoder, we see that is a
globally available constructor function. 

And in the end, this creates an object that helps us convert text to bytes. 

So our data then is encoder.encode and to encode we pass our text. 

And then it's the data, the encoded text, which we feed as a second argument to
writeFile. 

No, that's not too fancy, but that's our first Deno code we can write. 

Now, Deno, as I mentioned on a slide earlier, embraces modern JavaScript
features like Promises. 

Therefore writeFile does not take a call back to let us know once it's done. 

Instead here, we now can call then or a catch because writeFile returns a
promise. 

So here with then we can listen for the success of this write operation and we
can then do whatever we want to do. 

For example, we can console.log "wrote to file" and be done with it. 

Now, if we execute this file, if we save it and run it with Deno Run, we should
have a script that writes to a file. 

But actually what happens is that we get an error, a permission denied error. 

Well, and that is actually a key feature of Deno. 

So what's up with this error? 

---