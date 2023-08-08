## 144. Fetching Products - Time to Practice

<strong><em>no description</em></strong>

So right now, our get products page is a bit broken because there we still use
fetch all in a way that well simply does not work, we don't have this callback
approach anymore so we have to remove that and instead we still want to render
our view here in the end but we can pretty much copy the code we have here on
get index and of course you could also therefore refactor this to use a shared
function. 

But there, I now also have my then block and catch block and I will simply
replace the render function there to not render the index page but the products
page and use the rows as products. 

By the way, you can of course get rid of that field data, you don't need to
extract that because we're not using it, I just wanted to show you how you can
extract the different elements of an array in the argument list already. 

With that if you save this, the products page will also work again. 

Now that's all nice, what about add product? 

Let's tackle that next. 

---