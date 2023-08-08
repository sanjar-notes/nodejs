## 352. Manipulating the DOM

<strong><em>no description</em></strong>

So we get a result and that's great, now first of all that result had some
cryptic body which was a readable stream. 

Now what we can do here in the then block is we can return result json which is
a function that will throw a new promise or return a new promise, so I can add
another then block and here I will have the data, so the response body. 

I don't necessarily need that but I want to show you how you could get that data
that's getting returned by the server. 

More importantly, I know that either here or here, does not matter, I have a
response so the item was deleted on the server and now I want to delete it here
in the dom as well. 

Now how can we do that? 

Well we got access to the button on which we clicked right and the button is in
the end inside of the whole dom element we want to delete, so it is this article
which I want to delete. 

So therefore what I have to do is I have to find this article based on this
button and that's relatively straightforward to do. 

My product element and you can name this constant however you want is basically
my button and then there is a closest method provided by javascript and you pass
a selector to closest which gives you the closest element with that selector and
the closest ancestor element to be precise and there, I will simply use article
because I only have one article in my ancestor history here for this button, so
if I select my closest article, that should be the element I want to delete. 

So inside here let's say, I can call product element remove and that is a
function that will not be supported in Internet Explorer, there you would have
to access the parent node and then remove a child and that child would be the
product element. 

So that is a code that works in every browser, remove would work in all modern
browsers. 

Now with that in place, we can reload this page here and now if I click on
delete, it will eventually be gone and here, we see our success message. 

And now just to validate that it really only deletes one element and not all
elements, let me log in with my other user who also has two products I can
delete, these two products and now let's go to admin product, delete the boat
let's say and now only the duck is left. 

So this is great and indeed if I go to products, this data really is gone, I
can't load it here. 

So this is how you can use asynchronous requests. 

Now of course there is more you can do on the client side but this is not a
client side javascript course. 

The important thing here is that you can send data to your backend with the
help, with these asynchronous requests and how you can include data and how you
can handle that on the backend. 

---