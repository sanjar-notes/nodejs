## 501. Using Object & Array Types

<strong><em>no description</em></strong>

<v Instructor>Okay, so we know about some</v> essential TypeScript Basics,
actually the core essentials already. 

But now let's also dive into some other key types, which you'll see throughout
the course and what you need to know in general and that are object and array
types. 

Here we're working with numbers and strings, but actually also already with
objects, HTML input element and the HTML button element, which is inferred here,
is actually an object type, because we have DOM objects here in JavaScript. 

Now, we can also define our own object types of course. 

Let's say we have another function, print result and here it actually wants a
result object, let's say and it wants that object to have a val prop, so that it
console logs result object val. 

Now this example clearly is not made up here, but it is realistic that in bigger
applications which are writing, you'll have functions that want objects as
parameters, for example. 

So here we want an object, which has a val prop. 

Now you could add any here as an explicit any type, to make this code work, but
I wanna be very clear that I have an object which has a val prop. 

I also wanna be clear, what the type of the val prop value is. 

And for that, we can set up an object type by adding curly braces here after the
type definition colon. 

And then we simply define the structure of the object here. 

So with this code, I'm not creating a new object. 

This is not a place in code where we could create a object. 

Instead here, I just define the structure of the object, I expect to get here on
result object. 

I'm defining a so called object type. 

And with that here, we can then say that we want a val field in there and well,
let's say is always a number. 

Now of course, we could have more properties in there separated by a semicolon. 

We could for example also have a timestamp here. 

And that should actually be of type date object. 

The date object is built into JavaScript and we can refer to its constructor
function as a type like this. 

And now when we call print result, we have to ensure that we pass in such a
object. 

So here I can call print result and pass in an object which has a val key which
should hold a number. 

Hence I use result here because that holds a number. 

And I need the timestamp here and the timestamp can be generated with new date
like this. 

Now here actually TypeScript is not able to understand correctly that result
will always be a number, since I'm passing into numbers, it theoretically could
be able to infer this, that we then always return a number. 

But to let TypeScript know that this will always be a number, I can of course,
cast it with as number, because I know that this always is a number. 

With that we're passing such a object and here we're creating the concrete
object as a value, we're passing it to print result where we defined the type of
the parameter and that the type should be such a object type. 

With that, we'll make it very clear which kind of data we're accepting and how
it should look like. 

Now objects are nice, sometimes you'll of course, work with arrays. 

Let's say instead of logging my results here, I wanna store them in arrays. 

So add some arrays up there, numResults, which initially is an empty array, and
string results or textResults, which is an empty array. 

And here where I generate a new numeric result, I'll reach out to numResults and
push the result. 

And here I'll reach out to textResults and push my string result. 

And thereafter, I will actually console.log numResults here and textResults. 

Now, you'll already see that I'm getting an error here. 

That, the type of numResults implicitly is any array and that describes the
problem really well. 

We are pretty specific about the types of data we accept in this function for
example. 

We are very unspecific regarding those arrays, sure, both constants hold arrays,
but we're not specific regarding the values stored inside of the arrays. 

And that's something we can be with TypeScript. 

We can assign a type to this constant, just as we assigned it to a parameter
with a colon after the constant or variable name. 

And then here, we wanna set this to type number, but not like this, but to an
array full of numbers. 

And for that the TypeScript shortcut, or the TypeScript way of expressing this,
is number followed by square brackets. 

This means that the type of data stored in numResults is an array full of
numbers. 

And here, we can set this to string array. 

Now with that, the push methods down there complain, because result is this
union type and therefore it could be a string. 

It's the same problem as before. 

So here, we can simply tell TypeScript that we know that this is a number and we
know that this is a string. 

With that everything works and we can compile this code. 

Whoops, compile this code like this. 

Run it here. 

Enter five and 11 and we see that those values were added to the respective
arrays. 

These are array types. 

And array types are of course very important because, that ensures, that we
never add wrong data accidentally to an array that shouldn't hold it. 

---