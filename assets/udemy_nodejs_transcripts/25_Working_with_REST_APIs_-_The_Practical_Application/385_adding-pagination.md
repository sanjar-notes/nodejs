## 385. Adding Pagination

<strong><em>no description</em></strong>

Now before we actually move onto authentication, there's one more thing we can
do on the frontend and that is pagination, so splitting our list of posts across
multiple pages and I want to do that first. 

Now for that we need multiple posts, so let's quickly create a couple of posts
like a cup of coffee, choose that cup image which fits it quite well, so tasty,
whatever you want and click accept and let's add another post, a real duck
because I replaced that image of the other duck so maybe it's time to add
another one, this is a duck, click accept and now you see here I only see two
posts on the frontend, I don't see any more posts in that. 

If I reload, I see three however but I actually want to limit that, I want to
limit the amount of posts I see there and instead pass some information to the
frontend that allows the frontend to show some next and previous buttons at the
bottom. 

Now all the logic for this was already added to the frontend but on the backend,
I need to return different data, I need to paginate my data. 

For that, we should dive into our controller and there into the get posts method
or action because that is where I fetch all posts of course and that is where I
want to implement pagination . 

Now it turns out that in my frontend, feed.js, where I load my posts so in the
load posts method there, I actually do set some pages, I have my own pagination
logic in there and I can pass that page data back onto my backend. 

I want to do that through query parameters and I want to do that in load posts
in the frontend code, here in my url I'll add questionmark page equals to add a
page query parameter and I'll add this page variable which I'm creating up here
and this will be managed internally in my frontend app, so this will be either 1
or 2 or whichever page I'll try to load there. 

So now I pass that page query parameter to my backend and there, I now need to
extract it to implement pagination. 

So in my get post action here, I can extract the current page by accessing
request and then query parameters are stored in the query object and then page,
I'll set this to one as a default. 

You saw the syntax a couple of times, this or syntax checks whatever this is
undefined in which case it would assign this value so that I always start on
page 1. 

Then I'll set the per page value to two and I do this because I have the same
value in the frontend. 

Now of course you could find a more elaborate solution where you pass that per
page data from the backend to the frontend so that the frontend can adjust
dynamically but here I want to show the general setup and how this works, so I
am hardcoded per page here and I have hardcoded it in the frontend. 

Now I'll create a new variable, total items which I'll need to determine how
many items I have in the database because now I'll add a new find request and I
will add count documents here to find out how many documents I actually have,
this will not retrieve the documents, it will just count them. 

Then I can have success or fail, if I fail I'll have the same logic as before,
so I'll check the status code, add it  if it does not exist and forward the
error. 

If I succeed, then in this then block, in this function there, I'll know how
many items I have and I'll store that value in my total items variable. 

I created that variable so that I can now also use that data in other functions
than this function because in here, in this then block, I now want to return my
old fetching logic so that I first of all count and once I got the count, I
actually find the documents and retrieve them. 

So here I will return this and all that logic, so this then block essentially,
I'll cut that out. 

I'll remove the catch block, I'll add the then block after the first then block
and this catch block will now take care about both counting and then this
internal finding. 

However here I will not just find of course, I want to add pagination and the
logic is the same as before. 

We can skip a certain amount of items with the skip method and there, I
calculate the current page minus one times per page, so that if I am on page 1,
this will result in 0 and I skip no items, if I'm on page 2, this will result in
one and I skip all the items that were on page 1 and I also want to limit the
amount of items I retrieve with the limit method and here I take per page, so
the amount of items I want to have on each page. 

This is what I now return in there and then the posts here are these well
limited amounts of posts. 

In my response I now don't just to return to posts though, in my frontend I also
have some logic to take the total amount of posts into account so that in my
react frontend I know when to show the next and previous buttons. 

For that I'll add another argument to the data that I returned in the response,
I'll add total items in there, I'll be looking for this total items property in
my frontend code, so you should get this right not misspell it and the value
will be my total items variable, so this variable value which I assign here will
be stored down there. 

With that if I save that backend, if I reload the frontend, you now see a next
button here, if you click it we load the next page and we only have one item and
I can go back. 

So now I have pagination added as well, as you saw in the same way as before
because rest APIs are not that different in the end, just handled differently
because we have a separate frontend. 

---