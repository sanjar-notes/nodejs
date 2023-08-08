## 158. Fetching Admin Products

<strong><em>no description</em></strong>

Now let's work on the admin products page because there, I also want to display
my products so that we can interact with them. 

So in admin.js again, get product still uses fetch all, now it's of course a
good practice for you to make this work with sequelize. 

So definitely pause the video at this point and try to change this code here
such that it does retrieve the products and render them on the admin page. 

Were you successful? 

Well the code to you is of course the same code we used in the shop.js, instead
of fetch all, we'll use find all and we don't use the callback function approach
here because we're not using a callback function with sequelize, instead we have
then and catch since we're using promises. 

So let's console log our error in this case or pass our function we used as a
callback before to then and now here, we have our render function where we
render the products. 

Therefore if I now reload this admin page, I see my product here and I can now
add it or delete it. 

These however are two things that don't work, added doesn't work because I don't
load the product successfully and delete wouldn't work either. 

So in the next lectures, we'll work on these two things. 

---