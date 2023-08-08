## 503. Understanding Generics

<strong><em>no description</em></strong>

<v Instructor>Now, last, but not least,</v> to sum up this basics refresher,
let's talk about generics. 

Generics are a feature that can look very confusing at first, but it makes a lot
of sense. 

Actually, in our code here, we already have a generic type, our two array types
here. 

A generic type simply is a type that interacts with another type, and an array
is a great example. 

An array is a type on its own. 

It's a list of data, that's the core type, but it interacts with another type,
the type of data inside of the array. 

So, you could say that the array is the outer type, but then you have all the
elements in the array as an inner type. 

And this here, this way of defining an array type, is actually just a shortcut
in TypeScript. 

The longer form would be that we set numResults to type Array, but now array is
a so-called generic type, and you have to define the wrapped, the inner type, in
this case, the value types of the values inside of the array, and you do so by
adding angle brackets here, the smaller than and the greater than sign, and,
between that, the generic type of array. 

So, in this case, number. 

And this says that numResults is an array full of numbers. 

Now, what the thing between angle brackets refers to depends on the generic type
you are working with. 

Another example for a generic type would be a promise. 

Now, for that, we can create a new promise down there, myPromise, by calling new
Promise. 

And, by default, this code won't work here because we need to add a library to
tsconfig to, basically, tell tsconfig which kind of features we wanna support. 

And, for example, by default here, because of this target, it's configured to
compile the TypeScript code down to es5 JavaScript code, which is quite old. 

If we pick es6 here, for example, now this will work. 

We still get an error, but now it's a different error. 

So, we just have to ensure that we're telling TypeScript that we're working with
a JavaScript version that supports promise. 

Because promise, of course, is not a TypeScript feature, it can't be compiled to
something that works in older JavaScript. 

Instead, we need to tell TypeScript that we wanna compile to JavaScript, which
natively supports promise. 

And that's what we just did by changing the target to es6. 

With that, we can define our promise here. 

And a promise gets an argument which is a function, and that function itself
gets two arguments, a resolve and a reject function, and, inside of the promise
when we define it on our own, we can, for example, set a timeout to execute some
code after a second, and after that second we resolve the promise with, It
worked! 

And then, we can use our own promise here to listen to the result, and
console.log it here. 

And we could also add catch to react to the rejection of the promise. 

And now, let's compile this. 

By the way, now with a config file, don't select the file manually otherwise the
config file won't be taken into account by the compiler. 

It is taken into account by the IDE, but not by the compiler. 

Instead, just press tsc like this, enter tsc like this, and it will compile all
TypeScript files in the folder. 

And now, it compiled this code. 

And if we now reload, you see, It worked, after one second. 

But now, why is the promise a generic type? 

Because it eventually resolves to a value, and the value it resolves to, that's
the generic type for the promise. 

For the array, it was the value stored in the array. 

For the promise, it's the value the promise resolves to. 

And, for example, here it resolves to a string, and, hence, we should be able to
call split here, for example, and split on the w. 

But this does not work because TypeScript does not understand that this is a
string. 

It does not know the type. 

Well, by adding angle brackets after Promise, we can set the type to which
promise will resolve to to a string. 

Now, you can't set angle brackets on every built-in object. 

It needs to be an object that supports this, but the promise object, the promise
constructor function, does support generic types because you can set the value
the promise will eventually resolve to. 

And now, you see that split down there works, and if I recompile this and
reload, we see an array, it orked!, because of split. 

So, generic types can be tricky the first time you see them, but they make a lot
of sense, and they give you extra type safety when working with more complex
types or types that are simply connected to each other. 

---