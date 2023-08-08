## 120. Loading Product Detail Data

<strong><em>no description</em></strong>

Now that we're able to output our dynamic segment here, we can of course use
that information to instead load that product from our product file, so through
our product model which is responsible for interacting with the product and then
we can return a view which does actually show us these product details. 

So for loading let's get into our product model now, there we got to save and we
get fetch all, now I want to load a single product and for this, I'll add a new
static method and I'll name it find by ID, the name is totally up to you of
course but there I expect to get an ID as an argument and then also a callback
which will be executed once we're done finding the product here. 

In this function here, I will get all my products because I basically need to
read the entire file, we got no database here where I could run a query for one
product only, we'll do that once we add a database of course. 

So for now I get all my products just as in my fetch all function here but here
I now have my products available And before I return them in the callback, I
want to filter out that one product with my ID. 

Now keep in mind products which I'm returning here is already a parsed array of
products and a product will have an ID right, we assign that ID here and we
store that ID. 

So we will have an array of objects where each object has an ID and therefore we
can now use normal javascript to filter out the product we interested in. 

I can simply find my product and store it in this temporary variable there, I
can find it by searching products with the find method, a default javascript
method, this will execute a function we pass to find on every element in the
array and we'll return the element for which this function we pass returns true.


So this function we pass here will get the product it's currently looking at
because it executes it for all the products in the array. 

It will pass us this product into the function and then I write an arrow
function here and there is a short arrow function syntax where you can omit the
curly braces if you only got one line in there and you also return the result of
this one line, so there is an implicit return statement in front of that code
I'll now write, so I will have one line of code here which is returned and there
I will check if the ID of the product I'm currently looking at is equal to the
ID I receive as an argument here and if this is true, then the product which I'm
currently looking at will be returned and stored in this constant here and
therefore I can then execute a callback with that product. 

This is a synchronous function, doesn't execute any async code, so simply having
two lines after each other will do the trick here. 

So now we have that find by ID function in the model and now in the shop.js
controller, we can use that, so instead of logging the prod ID here, we can log
product, referring to our model, remember we're importing the class here,
product find by ID, though we can't log this because that will be an
asynchronous function, we have to pass in a callback. 

So here instead I pass in my prod ID and then I will get the product eventually
and in that function here, I will now simply log that for the moment so that we
see if that was retrieved correctly. 

So back on the products page, let's view the details again, that works and in
the console log on the server, we indeed see the details for the product we
loaded, so this seems to work. 

Now let's also verify that this still works if we add another product here. 

I'll add this and indeed we see the product here so this is working and now if I
click the details link here on the products page, I also get the information for
this product and the link of the image is so long here because it's not a url to
an image stored on a server but actually the image encoded in base64 which is
like a text encoding technique you could say. 

So this is the product and this is our fetch product function working. 

So as a next step let's add a view that displays the details and obviously feel
free to pause the video or to well this video ends here but to go ahead and do
this on your own, we'll do it together in the next lecture. 

---