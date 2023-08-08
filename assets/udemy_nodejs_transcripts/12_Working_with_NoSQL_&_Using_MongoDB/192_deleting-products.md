## 192. Deleting Products

<strong><em>no description</em></strong>

So now that we're able to add, fetch and update products, let's work on deleting
them. 

Now for deleting, you could implement different approaches, you could add a
method to the product class so that you can create a new product object and call
delete on it just as you called save on it but I will go with a static method
and I'll add a static method which I'll name delete by id and where I expect a
product ID as an argument. 

Now in here, of course again we need access to the database, so let's call get
db to get access to that one central database connection we configured at the
start and then on the db, again it's time to reach out to the products
collection and on that collection, we want to delete an element. 

Now as always, you'll find more in the official docs in the crud operations, if
you click on the documents you see that just as we had insert one, insert many
and so on, we also have delete many and delete one. 

Now I don't want to delete many products but exactly one, so I'll delete one
product here and you need to specify a filter now, so again pass an object where
you describe how to find that product and again it will be our boring ID equal
to check here. 

Now here product ID is an argument, so we need to convert it to an objectid
manually again by passing it to the objectid constructor and now mongodb will go
ahead and delete the first element it finds that has this criteria fulfilled. 

So I will return here and of course just as before, we can add then and catch
here if we want, we can catch any error and console log it and we can also work
with the result of this operation, we could console log it, I'll just console
log deleted and that will be it. 

So now we have the delete by id method,  now we just need to add it. 

So in the admin.js controller file, here the post delete product route, let's
comment it back in or not route, the action I mean of course. 

We extract the product ID and then here we had a different flow, I first of all
found the product here, now we don't do that anymore, we just call product
delete by ID instead, we pass the prod ID as a string and then we just have our
then block here which won't receive an argument and yeah that is it, we redirect
thereafter. 

So let's go back to our application, let's quickly add a new dummy product with
totally invalid and uninteresting data and that fails, that's an interesting
behavior, let's fix that in a second. 

Let's first of all check if deleting works, I get redirected to a page that is
not found, yeah makes sense because obviously working in a controller is not
enough, I need to go to my admin routes and comment in the post delete product
route. 

So after changing this, let's now click delete and now I get no products here. 

Let's confirm in compass by quickly refreshing that page and our product is
gone, so deleting works. 

Let's now see what's going wrong when I tried to add that product. 

---