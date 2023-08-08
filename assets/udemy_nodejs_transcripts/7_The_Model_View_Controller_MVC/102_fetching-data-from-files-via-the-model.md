## 102. Fetching Data from Files Via the Model

<strong><em>no description</em></strong>

I'm still getting the error that my products don't seem to have a length even
though I'm fairly confident that this code should retrieve my products but what
is wrong with that code? 

Well I am returning data here in both cases but keep in mind that this is
asynchronous code. 

So my fetch all method here executes this line, executes this line and as you
learned, it simply registers this callback in its event emitter registry to put
it like this but then it just finishes with this function and this function
itself does not return anything. 

These return statements here belong to this inner function here, not to this
outer function, so fetch all does not return anything, it returns undefined
therefore and hence in my view, in the shop.ejs file, if I try to access the
length on my products, I try to access length on undefined and I get an error. 

So this is the issue and how can I fix this then? 

There are multiple ways of fixing this, for now I will simply accept an argument
in fetch all and that's a callback and that actually allows me to pass a
function into fetch all which fetch all will execute once it is done, so that
the thing calling fetch all can pass a function it is then aware of being called
which holds the data I want to return. 

Sounds complex? 

Let me show you how it works. 

So I will receive a function here, this argument will hold a function and
therefore instead of returning an array, here I will have a callback where I
pass an empty array, so I execute this argument as a function to which I pass an
empty array and I will do the same down there, just not with an empty array but
here I will have a callback where I pass my parsed json data. 

So I do call this callback and this allows me to go to my controller where I do
call fetch all and there, I now simply have to pass in a function where I know
that I eventually will get my products, like this and therefore I don't need to
store it here because this fetch all function will not return anything. 

Instead here I simply create my own callback process and I render in that
function I pass to fetch all once I know that fetching all products is done and
I receive the products here because that is exactly the argument I passed to the
callback in fetch all because the callback argument here will refer to this
anonymous function I'm passing into fetch all. 

It's the same logic read file uses here, just that we didn't defined read file
on our own but read file also takes a callback and here we pass in the function
read file should execute for us once it's done. 

We do the same just that we write both sides now. 

We have fetch all and fetch all takes a function it should execute once it's
done and once it's done, we get the products, thanks to our own implementation
of fetch all and we then render our response with those products. 

And with that if we save that and now we reload this page, we do see the
products here and we do of course see all the products we had in the past as
well as any new products we add and there is a little styling page I see. 

But this is how this works and now it's still not a database but it's better
than this in array storage and it already shows us why we might want to use such
a model. 

It's not super complex code but it clearly is code that belongs to this data, to
this model and therefore it's outsourced into its own separate file. 

---