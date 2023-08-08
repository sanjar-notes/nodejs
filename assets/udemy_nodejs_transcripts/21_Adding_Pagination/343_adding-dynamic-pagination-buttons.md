## 343. Adding Dynamic Pagination Buttons

<strong><em>no description</em></strong>

So let's now use all that information we get back from our backend when
rendering our index.ejs page, we have all these utility information pieces,
these utility variables like total products has next page and so on which
hopefully should be helpful. 

So let's go back to index.ejs . 

and there instead of hardcoding this, we can now generate this dynamically. 

Now I always want to have page one here, that is something I absolutely need. 

Let's say the page next to it should be the current page, so actually instead of
total products, I should return current page here which is simply the page
number so that I always know what's the currently active page. 

So I'm returning current page as well and here, I can now output equals current
page because I'm now getting that data in my view and here I therefore will load
the current page number if I should click on that link again. 

And this current page will receive a css class of active because that will
always be the active class and I'll quickly go to my main css file to give that
the same style as when I hover over it. 

So here I'll have my pagination a class with an active class added to it with a
single dot, a active will receive the same style as when I hover over it. 

Now I only want to render this one by the way if the current page is not one
because otherwise I will already render it here, so we can add some ejs logic
here to check if current page is equal to one or to be precise, if that is not
the case. 

If that is not the case, then I will render this otherwise I will not render
this. 

So I can now close that and now this will only get rendered if the current page
is not equal to one, like this. 

This will always get rendered, the current page and I also want to render the
next page let's say, so I will repeat this one more time here and this will be
the next page. 

Remember the next page is some information which I return as well, next page
here. 

So I will render the next page, only however if there is a next page and that is
another piece of information I do return, has next page. 

So let me go back and here again if has next page, so if that is true, then I
will render this, otherwise I won't, so here I just close that if statement. 

I also want to render the highest page, so I'll add another anchor tag here and
that will use this last page information, by the way the active class here of
course not be added here and also not be added here. 

So here I will render the last page and it will lead to last page, here it will
lead to next page by the way so we have to adjust this link obviously, here it's
the last page and this last page should also not always be rendered, it should
only be rendered if last page is not equal to the current page, so if we are not
already on the current page because then this link would already render the link
to this last page and the next page should also not be equal to the last page
because if it is, then this link will already be rendered and this is then the
last and next page simultaneously but if both is not true, then I will render
this. 

Now let's have a look at this and let's reload this and here I got an error,
little logical error. 

Count used to be the function you should use, now it's count documents so change
count to count documents here but this error is not coming from that but in the
index.ejs here I got a dollar sign instead of a percentage sign which I should
use. 

With that fixed, this looks a bit better but I got 11 here and then a two again
so there seemed to be some issues. 

For one it's rendering the one here even though the current page is not equal to
one, the problem here is really just the data format, we're comparing strings
and numbers here so I should remove one equal sign and now this works. 

And now regarding the 11, next page somehow is calculated to be 11. 

The reason for that is that page here is a string, not a number and therefore
page plus one gets concatenated to 11, so to 11, this can be fixed by adding a
plus here in front of request query page and now this looks better. 

Now I can switch between these two and this is looking all right now with that
error, this format, this data type error fixed, now what happens if I load that
page without the page query parameter and then I have this not a number issue
here. 

And to fix this, I can add two pipe symbols here in that one and this means if
this is undefined or if this does not hold a true-ish value, then we'll use this
value instead. 

With that if I save that and I reload this page, I'll start on page 1 and now I
can jump around. 

Now let's also try this, when changing the items per page to one so that we
should have one extra page. 

Now if I reload this with Page 1 being loaded, I can go to page 3 and 1, 2, 3. 

Now I don't see a two when I'm on page three because we have no logic for it in
our template right now, I could of course add that logic to also show the
previous page. 

For that I can replicate this and if I have a previous page, then I can show my
previous page and link to it here. 

Now of course I want to avoid that I have two ones if I'm on page 2 because that
would render this link and I would render this link, so I don't want to render
this first page if I am on it already or if it's equal to the previous page. 

So I only want to render this first page if it's not equal to the current page
and if the previous page is not equal to 1. 

Now by the way since I fixed that data type, we can also work with double equal
signs here again. 

So now if I reload this page, it's in the wrong place, the previous page here
should be before this current page so let's fix that. 

Reload again, now this is looking better, now I can go to page two, page one and
that all seems to work. 

Now let's add another product, product4 with another deck again to see how it
works with four products on the shop page and now I see the first page, the next
page and the last page. 

If I go to the last page, I see the previous page and the first page, if I go to
three, well then I have the previous and the next page which is the last page
and the first page. 

So now this pagination is working and you can always of course tweak this to
your requirements or your different needs but now this is looking good to me
here. 

---