## 110. Storing Product Data

<strong><em>no description</em></strong>

Time for more logic and with which logic do we want to start? 

We could add more logic to add product for example so that we finally can not
just add a title but actually also an image, a price and the description text
here. 

So to do that first of all, I'll work on my model here. 

In this model, I want to make sure that we don't just work with the title here
but that I actually initialize a new product with my title and I will now rename
it here as an argument, you probably got the point that these two names don't
have to be equal but it's easier to understand the constructor if we give it a
title that makes sense or a name that makes sense. 

So I got my title here, now a product will also have an image url, later in the
course we'll also add image upload, for now let's take a finished url of some
image on the web, it also needs a description and a price. 

And then here I will simply store all that data in properties, image url will be
stored, the description will be stored and the price will be stored, whoops, not
the description, price like this. 

With all that, future products we add to our file will have all that data in
them and the data we fetch or products we fetch will have too, now we just need
to work on our add product view and make sure we've got more inputs to fetch
that additional data. 

And for this let's simply copy that form control and add an additional one,
we're fetching the title. 

Now as we just worked on the model, we'll also need an image url and I'll simply
fetch this as some text input for now, again we'll add an image upload later in
the course, so here I will get my image url, name that field image url and
optionally also assign an ID here for best accessibility. 

Now I'll copy that again and here I will not add an input but instead here I
want to fetch the description or let's actually fetch the price first, so it
stays in input actually and here I want to have a price. 

Now this can be of type number and I will give this here an ID of price and also
a name of price and now I will add one more form control and that should be my
description, so here this is for my description for the element with the
description ID, it gets the label description and now this is not an input
instead it is a text area and that text area has a name of description and an ID
or description and it also has let's say five rose here. 

If we add all that and we go to add product, this is the form we see, doesn't
look too bad but the description field doesn't look good, well that is a styling
thing and we can quickly fix that in the public folder by going to forms.css . 

I want to give it the same styling as a normal input has, so here where I have
form control input, let's add form control text area with a whitespace
in-between and let's also add that rule or that selector for this rule here and
also down there for this rule, I will add text area and then the focus pseudo
selector and with that if we now reload, this looks much better. 

So now we got all these fields here which we need to add a product and these are
automatically added to the request which is sent to the backend because we are
using regular html inputs in a form and we assigned names, so now we can extract
all that data up by the names we assign to our input fields here. 

And with that, let's actually go back to our controller, to the admin controller
where we have post add product and there, we create a new product. 

I do extract the title here, now let's do this in a more structured way to make
it easier to read. 

I do extract my title here and store it in a constant, title constant because I
never overwrite the value in this function, I will then also add my image url
which I extract from request body, image url. 

Now make sure to type this in exactly the same way using the same casing as you
assign the name here and the same is true for the price and the description. 

So here I'll also add a price field and extract the price and of course also
extract my description. 

And now with that data extracted here, we can pass the title, we can pass the
image url, we can pass the description, watch the order you defined in the
constructor and we can pass the price and now we create a product with all that
data. 

Now with that, in the next step, let's also extract that data and show it when
we show all products. 

---