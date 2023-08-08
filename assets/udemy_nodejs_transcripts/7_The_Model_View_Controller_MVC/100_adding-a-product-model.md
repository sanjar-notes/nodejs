## 100. Adding a Product Model

<strong><em>no description</em></strong>

With controllers and views added, it's time to care about the model. 

The problem with our model is that we, well we have a very simple one, we manage
our products array here and a product is simply created on the fly as an object
that looks like this. 

Now in the end, that product represents our data, we have products in our app,
later we'll also have our things like a user but for now it's just a product. 

Still we can define a model for that and for this, let's create a new folder in
our root project and name it models. 

Now all these names are exchangeable of course but this makes the separation
really clear, we get controllers, we get views, we get models and that makes up
the mvc pattern. 

Now in there, I'll add a new file product.js . 

Now please note it's not products here because I want to represent a single
entity because in the end, our core data is a product. 

Sure we also have lists of products with which we work but the core thing that
makes up the app is how a product looks like, which fields it has, does it have
an image, a title, that is our core data. 

A list of products is boring, it's just well more of that type, a single product
is what defines our app in the end or part of what defines the app. 

Now how this this model look like? 

This is totally up to you in the end, you can define this in which ever way you
want, you can for example simply export a constructor function here, so a
function which I name product and you call that to create new objects based on
that, using an ES5 constructor function but if you're using next gen javascript
as I'm doing it here, you can instead create a class. 

You can create a class named product that looks like this and this is now also
exported and in case you're not sure what a class is, check that javascript
refresher at the beginning of the course, I do explain it there too. 

Now here in this class, I want to define the shape of a product and for this,
I'll first of all create the constructor function, So here I want to receive a
title for the product which I'll then create from inside my controller, so here
I get my title and you can name this title of course and I will then create a
property in this class, so basically like a variable in the class you could say.


You do this with the this keyword and then this title is equal to the title I'm
receiving as an argument here and these names don't have to match and to avoid
confusion, you can also name this t here. 

So now I'm creating a property in this class, this allows me to then create an
object based on this class where I can pass the title to the constructor which
we call with new and then this will get stored in the created object. 

But obviously I don't just want to be able to create objects with a title, I can
do this with the current curly brace syntax too, instead here I want to be able
to create my or to store my product to an array of products and fetch it and for
this I will reintroduce my products array here and we will change this later
when we use a real database but for now let's go with this approach and I will
add a save method to my class here by calling save or by typing save, adding
parentheses and then curly braces. 

So it's like a function, just without the function keyword. 

So this is now a method available in this class and in the save method, I want
to store my product in this array and I can do this by reaching out to products
and then calling push here just as we did it before in the controller and I
simply push this because this will refer to the object created based on the
class and that is exactly the object I want to store in this array. 

Now obviously I also want to be able to retrieve all products from that array
and I also want to do that through my product model, however whereas save makes
sense to be called on a concrete instantiated object based on product, I also
want to have a fetch all method which is like the utility function you could
say. 

This is not called on a single instance of the product because it should fetch
all products and I don't want to create a new object with the new keyword with
some dummy title just to fetch all existing products and therefore I will add
the static keyword which javascript offers which makes sure that I can call this
method directly on the class itself and not on an instantiated object and then
in here, I will return this, whoops, products like that. 

Now this is the model finished, now let's move to the products controller file. 

There I will first of all get rid of products here at the top and also of
products push down there because now I want to use my model, I also don't need
that anymore, so that I got no products array related logic left in this file
instead I will now import my class by adding a new constant, product and you can
name this however you want but the convention is to use a capital starting
character for classes and in the end, we do just import this class so I will add
the capital character in this controller file too and I do import a class by
requiring this from the models folder, from that product.js file. 

With that added, in post add product I will now create a new object based on
this class blueprint and that is what classes are in the end, they are
blueprints. 

So I will create a new product, a local constant with new product and there I
will pass request body title and that simply takes the title I have here as a
name on my input which is submitted. 

With this, we create a new product based on our class, now there's one
additional thing that needs to be done though, I want to save that and I can do
that by calling product, save. 

This will use that save method we defined and it will therefore for now push
that onto this array. 

Now with that in get products, I also want to fetch all products. 

So I will create a new local constant, products and now I will use that static
method because I don't want to create a new product where I would have to set up
some dummy title because I don't create a product here, instead I just want to
use product and call fetch all and this should give me all the products and now
I have my products here and if I save this, it should now work. 

If I go back and I reload this page, I get cannot read property length, that
makes sense because fetch all returns this product which is incorrect, it should
just return products because we are returning this array, not some local
property of this class, there is no products property. 

So after fixing this and removing this down there, now if I reload this, this
works and if I now try adding a first book, this again works now using a model. 

And whilst this might look more complicated right now and it certainly is
because we're just using our dummy storage here, this is great once you really
got more complex models with more fields, with more methods and where you don't
store them in some random array but where you got the whole database connection
logic and so on too, you then put that all into your model and you don't have to
care about it in your controller. 

And it actually simulate this by moving away from our array storage here and
move towards a file storage at least, before we then later in the course also
use a real database. 

---