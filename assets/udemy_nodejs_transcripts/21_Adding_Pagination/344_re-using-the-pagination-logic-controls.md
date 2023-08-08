## 344. Re-Using the Pagination Logic & Controls

<strong><em>no description</em></strong>

Now with the pagination added to this first page, let's add it to the products
page here as well. 

And to do that, we can of course grab this entire section either from the
index.ejs file, cut it and create a new include for it which we can name
pagination.ejs and in there, I'll insert this pagination content and in
index.ejs where I had this previously, I can copy that include code from add to
cart and add it here and include not add to cart but pagination of course and I
just need to forward the data into pagination, so current page, previous page,
next page, has next page, has previous page, all that data should be forwarded. 

So I want to forward current page, which value is current page, so the key value
pairs here need to be equal. 

Next page which is next page, previous page which value is, whoops. 

previous page, last page where the value is last page, has next page where you
guessed it, the value is has next page and and has previous page where the value
is has previous page. 

Now with that include added, let's quickly test this by going back to the index
page, that all seems to work and now we can grab that include code and add it
also on the product list page. 

There we load this div, I can add my include to add the pagination section too. 

So now if we save that, we also need to adjust our controller because there in
get index, I have all the logic for paginating, I need that same logic in get
products. 

And again, you could refactor this because now we're sharing a lot of code but I
will copy that entire code here where I get my products, get the count, skip and
limit and so on, so I will copy all of that and replace my logic and get
products up there with it, just render something different, the product list
view here, name this products maybe and the rest should be equal. 

And now if we save all that and I go to products, I should update the path here
too, to products so that the right item gets marked in the navigation. 

So now if I reload this page, products is highlighted and now here I also have a
working pagination in place. 

Now there is a tiny error I need to fix because right now if we're on the
products page here and we paginate around, I actually load my index page again
because in the pagination.ejs file here, I always have this absolute path, slash
and then the query parameter. 

Well I should only have the query parameter so that this gets appended to
whatever the current url and path is and this will make sure that if I am on
/products, I stay there and if I'm on slash nothing, I stay there. 

So if I reload slash nothing, you see the pagination query parameter still gets
appended but if I'm on products, it gets appended there and I stay on /products
which of course is the behavior I want here and with that, this is fixed. 

---