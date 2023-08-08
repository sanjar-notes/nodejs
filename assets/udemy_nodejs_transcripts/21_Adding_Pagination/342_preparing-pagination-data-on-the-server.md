## 342. Preparing Pagination Data on the Server

<strong><em>no description</em></strong>

We are able to skip and limit the amount of items we fetch and we can control
that with query parameters but my buttons are hardcoded right now and that is
not ideal of course, instead I rather maybe want to highlight the page I'm
currently on and then show the next page number or the previous page number. 

For this I need to fetch more information. 

I will find my products and call count here, then I can also add then and catch.


The important thing is I don't need catch because I'll concatenate my other
promise chain later, the important thing here is this will now not to retrieve
all the products but simply just a number, so number of products is what I get
back in this then block function here and in that function, I then want to kick
off my request where I really do fetch all the data. 

So we'll return product find in here with skip and limit chained after it,
that's important and then I'll add this then block to continue. 

So I'll first of all find the count, then I have this number of products here
and then I kick off my normal find method where I then really fetch the items
and I skip and limit them. 

Here I'll add a variable, total items and I'll set total items equal to num
products in here. 

So now I will have the total number of products stored in that variable here and
when I render the index page, then I want to return that information as well, so
not just the products but also total products and that will be total items, so
that will be a number in the end and I also want to pass the information whether
there is a next page, so maybe has next page which only will be the case if the
total number of items is greater than the page we are on times the items per
page. 

So we have a next page if items per page times page is smaller than total items
because if we have 10 total items and we are on page 4, then we have 2 times 4,
8 items which we are seeing or which we saw and we have 10 left so there will be
a next page. 

Simultaneously I can add has previous page here where I can simply return the
information whether the current page is greater than 1. 

If that is true then there is this a previous page because there will be page
one, if that is false because we are on page one already, well then there is no
previous page because we can't go lower than one. 

I can also return some extra information like the next page and that will be
page plus one of course, if we are on page 1 the next page would be page 2 and
previous page would be page -1 obviously. 

We can also add last page to have a way of displaying the highest page number
and that is math seal total items divided by items per page. 

So if we have let's say 11 total items and we have items per page of two, then
the result would be 5.5 and then math.seal would return us 6 which would be the
correct value because we would need 6 pages to display all 11 items if we show 2
items per page. 

So now I'm passing all that information to my products page, to my index page
here to be precise and there, I now want to use it. 

---