## 214. Fetching All Products

<strong><em>no description</em></strong>

Now that we're able to save products, obviously we again want to be able to
fetch them. 

So let's head over to the shop.js file in the controllers folder and let's start
working on get products and get index actions there so that we can indeed fetch
all products. 

Now we got no fetch all method in mongoose, that was a method we defined on our
own but we can still use something on the product model which we're still
importing from the product models folder and which is the mongoose model in the
end and there we got a couple of static methods, you can find all in the
official docs of course and one of them is the find method which you already
know from the mongodb driver. 

Now find works a bit differently when used with mongoose, it does not give us a
cursor instead it does give us the products, we could add .cursor and call this
to get access to the cursor and then use each async which would allow us to loop
through them or next to get the next element but I will just use find and this
will essentially give me all my products automatically. 

So then in products, I should get my products and I should be able to output
them, so if I now console log my products here so that we can also see them, we
have to go to the shop route as well and there we want to include the get index
route and the get products route and since I also did include the get index
route here, I of course also need to work on get index in my shop.js file in the
controllers folder, there we also want to use find instead of fetch all but that
should be it. 

If we now save everything and we go to the products page, indeed I do see my
product here so this is looking good and if I go back, well then I see here is
the output of the data that was fetched  and you see I get an array here because
find when used with mongoose automatically gives me that array here. 

Now again if you know you will query large amounts of data, you should turn this
into a cursor or of course manipulate find to limit the set of data that is
retrieved, something we will see in the pagination module later in the course. 

So here I now got my working get products and get index route, let's next work
on the detail route for a single product. 

---