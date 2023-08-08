## 340. Retrieving a Chunk of Data

<strong><em>no description</em></strong>

I'm setting these query parameters and I can use that data on the backend to
control which data I want to fetch, obviously I do that in my controllers and
there in the shop controller. 

Here. 

we're working on the index page so I'm looking for the get index controller
action. 

In here I need to retrieve the information on which page we are, so which data
for which page needs to be displayed, so I'll store this information in a new
constant named page and in that constant, well I will store request and then we
can get query parameters on the query object provided by expressjs and there I
can access page, page because I named that query parameter page here. 

So now with that, I'm getting that page number and I'll store it in this
constant. 

Now with that, we just need to define how many items should be displayed per
page and that's something I will store as a global constant in this file, I
could also store it in a different file, export it there and import it here but
I will name this items per page and this will be let's say 2, it should be some
number lower than the number of items you have here so that you can see a
difference. 

So I have two items per page here and with that in get index, I know that I if
I'm on page one want to fetch the first two items, if I'm on page two, I want to
fetch items three and four, on page three I would fetch four and five and so on.


Therefore we now need to control the amount of data we're retrieving from the
database, find right now gives us all the items but we can actually control
this. 

In mongodb and therefore also mongoose, there is a skip function. 

We can add this on a cursor and find does return a cursor to skip the first X
amount of results and here, that would be page -1, so the previous page number
in brackets times items per page. 

So if I am on page 2, I would skip the first page -1, so the first one times
items per page items. 

So on page 2, if I have 2 items per page, I would skip the first one times two,
the first two items. 

I don't just want to skip some items, I also want to limit the amount of items I
retrieve though, so that I don't just skip the items of previous pages but for
the current page, I also only fetch as many items as I want to display there and
this can be done with the limit method. 

The limit method as the name suggests limits the amount of data we fetch to the,
well number we specify here and here I can pass items per page because that is
my item limit per page. 

With that if we save this code, we can reload this first page with the query
parameter set to page 1 and we only see the first two items. 

If I now click on two down there, I only see the third item because I'm on page
2, I skip the first two items and I fetch the next two items and I only happened
to have one other item. 

On page 3 if I would enter this, we would not find any products because I have
no items for this page but Page 1 and 2 were just fine. 

So this is the general idea behind pagination. 

Now obviously the idea would be that we update our pagination buttons here based
on, well the page we are on and the maximum number of pages that are available
or something like that. 

So let's see what we can do there. 

---