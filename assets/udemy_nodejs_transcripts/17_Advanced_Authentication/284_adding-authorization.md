## 284. Adding Authorization

<strong><em>no description</em></strong>

So how can we add authorization? 

I want to ensure that I can't delete or edit this book with or this product with
the wrong account. 

Now we do have important information stored on the product, we know which user
did create it, so in the end we just want to check if the currently logged in
user is the user who created that before allowing any edits to that item. 

And that means that on the admin controller where we render our admin list here,
get products here, I only want to render products that were created by the
logged in user because there is no sense in showing products on this page that
were not created by the user because we're in the admin section, you are not
able to do anything with it if you weren't a creator. 

So authorization simply means we restrict the permissions and we can do that by
restricting the data we return for example, so here when I find product, I dont
find all but I'll add a filter and I'll filter for products where the user ID is
equal to the user id of the currently logged in user, so user ID is equal to
request user id, whoops, ID and keep in mind request user exists because we do
extract that user in app.js in a separate middleware here, there I do store the
user in request user, so I know that only products which were created by that
user should be retrieved. 

With that changed if I reload this page, I find no products for test2 but if I
do login with my other account with test@test.com and I go to admin products, I
do find that book, so that is the first important step forward. 

The problem is I could theoretically still issue requests behind the scenes
where I do try to delete a product which was not created by me, so more
protection is needed. 

Let's add that next. 

---