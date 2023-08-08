## 103. Refactoring the File Storage Code

<strong><em>no description</em></strong>

Now we added that file storage logic to our model, let's now fix this a little
bit or improve the code in the model, we're reusing some code and if we reuse
code that always screams for some refactoring and indeed, that is what I want to
do. 

I will create a helper function and I'll store it in a constant and I'll name
that helper function get products from file and this helper function will do
this path construction here for me and it will also read the file, so it will
basically do everything I do here in fetch all, like this and I will even get my
callback here because I do execute that here and ultimately return this because
the issue of this process taking some time and the need to inform the caller of
this function about when it's done hasn't gone away. 

So I still use the same pattern of having this helper function which receives a
callback which it executes once it's done reading the file. 

With this, get products from file is really just all I execute here in fetch
all, so I simply just call this and forward the callback. 

Now for save however, it means that here I can also call get products from file
but here I don't forward any callback because instead I have my own logic here,
I do retrieve my products there and that's essentially the same logic I do have
in get products from file, I either return an empty array if I have an error or
I parse my content, here we did it the other way around but in the end it will
result in the same result. 

So I'm only interested in this logic here then, you can remove that and instead
just take this code here and then create a new anonymous function where I know
that I will get my products because this again is the callback function, it is
the function I will pass as an argument to get products from file, so it is what
will get called here. 

So this function will get called in, will receive an empty array or the array
with the data and I should by the way add a return statement here to make sure
that we never execute this code after having executed this code, that was an
error we had in the code before. 

Alternatively you simply wrap the other code in a else statement, either of the
two, so here I'll use the if else approach. 

But now with that the callback will get executed and will get this array of
products and now here in save, I do have this anonymous function which receives
the products and in this anonymous function, I will then put in my code where I
append a new product and make sure to always use arrow functions so that this
never loses its context and always refers to the class and therefore to the
object based on the class and then I write to the file, this means I can get rid
of this line too. 

And now we get a slimmer version because we're reusing code but it still should
work if I reload here, loading product seems to work and if I add a second book
even though it's the fourth one, this crashes because p is not defined. 

Yeah the path here in save, that is a problem the path is not defined because
I'm only defining it in my helper function now. 

Now there are various ways of fixing that, one of the easier ways is to simply
create this as a global helper constant here, p so that I can use it in the
entire file, you can of course also go for different solutions and pass it
around in the functions but now the path should be available in the save method
and in get products from file. 

And with that if I now reload and try this second, actually fourth book again, 
this now works. 

So now we are able to elegantly work with our products, store them in a file,
fetch them from there and all of that through a model. 

And that is the MVC pattern implemented into our project. 

---