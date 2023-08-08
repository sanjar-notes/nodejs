## 436. Adding Pagination

<strong><em>no description</em></strong>

Now that we're able to fetch our posts through graphql, let's add pagination
again. 

How does that work with graphql? 

Turns out not too difficult. 

We start on our graphql schema again because there, we'll need to change
something on our posts query because it is the post query where we want to add
pagination right, we want to be able to paginate through all the posts. 

Therefore the posts query needs an argument, it needs an argument that allows us
to define the page we are on and I'll name that page, you can name it however
you want and this will be of type integer. 

Now with that argument added in the schema, in our resolver we can implement
pagination. 

There in my posts resolver, my arguments now will have that page property, so I
can retrieve it with destructuring and after checking whether I'm authenticated
or not, I now need to setup pagination or I need to find out which page I'm on
and use that. 

Now first of all, I'll quickly check if page is not set because if it is not
set, so if it is undefined, I'll set it equal to 1 so that I always start on
page 1 in case I don't specify any other page. 

As a next step, we can define the per page variable which is two as it was in
our rest API scenario, you could theoretically also fetch this as an argument,
I'll hardcode it here for simplicity reasons because this was primarily
something we would have to manage in the frontend with a dropdown offering the
user different page sizes and so on. 

So I'll hardcode it here and now we have per page, we have the current page, now
we can use that here when we find the posts. 

And you already learned that you can paginate with skip and limit, so skip and
limit is what you can add here and in skip, you want to skip your current page
minus one times per page. 

So if you're on page two you have two minus one which is one obviously and you
skip one times two, so the first two items, the two items that were on page 1. 

You don't just want to skip though, you also want to limit and you limit the
result set to the amount of pages, of items you want to render per page by
adding per page as an argument here. 

And that is it, this is pagination in place on the server side. 

Now in the frontend there, we already have some logic for the pagination if we
go to load posts and there I do already get my page variable, now I just need to
send that with my query and for that on the posts query, I can set page equal to
well the page I calculate up there, since this is a number I also don't need to
wrap that in double quotation marks. 

Let me save all that, also make sure the backend code is saved and let's reload
our frontend application. 

For that I should restart the server and indeed here, I got pagination in place.


And when I add a new post to make sure that it does not show up as a third
element when we only want to have two, I will go back to my react code and there
to the finish edit handler and here in set state where you find that unshift
statement, simply add update posts pop in front of that. 

And that is all, this will remove one element and add the new one at the
beginning and now let's give this a try, let's add another duck, choose the duck
image, also very lovely, accept this and here is the another duck, another cup,
here is the rest and this is exactly the data we find in the database too. 

We got tWo another ducks just in case you got confused. 

So this is working, let's now work on the image upload because that obviously is
something very interesting which we haven't touched on thus far for our graphql
API. 

---