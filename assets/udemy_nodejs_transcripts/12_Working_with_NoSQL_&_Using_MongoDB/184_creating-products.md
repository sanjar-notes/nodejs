## 184. Creating Products

<strong><em>no description</em></strong>

So let's make add product work again and for this we'll not use the user anymore
but instead here before we use then, we'll re-use that so no need to delete it,
before we do that we'll use our product model. 

So I'll create a new product constant by initialising product again and here, I
will simply pass title, price, description and the image url, so we'll pass all
that data into the constructor of the product. 

Then on this product, I can call save and then here to call then, I'll go into
my model again and I will return this here, so I'll return my collection and
then this entire command chain because that will allow me to well treat this
overall as a promise and chain then thereafter and then therefore also redirect.


So now with that if I save that and I go back to the form and resubmit that, I'm
actually redirected to a page which is not found because I commented out all the
shop pages but if we go back to our server side console, we see something
interesting. 

We see that this here has to be the output of this console log line in the
product model where I print the result of the insert operation and there, we see
a lot of data about that operation and for us important, if we scroll down to
the bottom, we see one document was inserted. 

It received an ID and such an ID is managed automatically by mongodb because
every document needs to have such a _id, this is a must have and mongodb creates
it on the fly automatically if the object you entered does not have it, so we'll
use that auto-generated ID and then you see the data which we entered also was
stored. 

So whilst we can't look into database yet because we're not fetching anything,
we see that our insert one operation was successful and did successfully add a
product into the collection which is of course amazing. 

---