## 215. Fetching a Single Product

<strong><em>no description</em></strong>

Now that we're able to get all products, let's also make sure we can get a
single product and for that, I'll work on my get product action in the shop
controller and there we extract the product ID which is great, I don't need this
code here anymore by the way and the good thing is product is a mongoose model
and mongoose indeed has a find by ID method, so little convenience method that
defines for us. 

So again find by ID here is not our own method, it's defined by mongoose. 

And best of all, we can even pass a string to find by id and mongoose will
automatically convert this to an object ID, so it will handle that for us as
well, so again getting a lot of that convenience by just using mongoose and then
we should be able to get back a product and use that. 

So actually this should be everything we need to do, nothing basically I guess. 

One thing I have to do of course is I have to comment that route back, so this
route for loading a single product. 

With that if you save everything and you click on details here, we indeed see
the detail page for this product. 

So this is now also working and that of course is really great because well this
allows us to easily adjust our code to use mongoose. 

---