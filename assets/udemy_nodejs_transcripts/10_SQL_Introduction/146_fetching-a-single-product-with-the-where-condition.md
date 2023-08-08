## 146. Fetching a Single Product with the "where" Condition

<strong><em>no description</em></strong>

We're able to to save a new product and fetch all products, let's now find a
single product by ID. 

This also is not that difficult, we can again use our db pool, execute a query
and the query we want to execute here is select everything from products and
everything here means not all rows but simply all fields but now we can restrict
the number of rows with a where condition and where is another SQL keyword. 

So there we can execute where products ID equals one equals sign only, not
multiple ones as in javascript, where the ID is equal to question mark simply to
let my MySql inject the value again, the ID we're getting as an argument here. 

Now let's return this promise here and this is our statement for fetching a
single product with all the columns though, so with all the data. 

Now we can go back to shop.js and there where we do fetch a single product in
get product, well there we still use find by ID for a given product ID but of
course no nested function here, that didn't change so let's strip that out of
there, simply call find by id like this and instead add then and catch and in
catch, we got our error which we can output and in then, we got our product in
the end or to be precise we of course got that nested array where we know that
the first element will be all the rows we got and that will just be our product
or it should just be the product. 

Make sure to wrap that special syntax with the square brackets in the
parentheses. 

So now we just need the render function here and place it in this function we
passed to then and we're extracting a product here, we're passing it to our view
here, let's see if that works. 

If I now save this and I click on details, this failed, now let's simply console
log our products here to see why it failed. 

If I reload this page, here's what gets logged and the reason why it failed is
that product still is an array, an array with one element only but still an
array but the view simply expects one single object, not an array with one
object. 

The solution is to simply pass the first element in that array and we know that
there will only be one element in that array. 

So now if I reload this page, we see the second product, I just didn't add an
image for that otherwise we would see that too. 

So this is working, we're able to fetch a single product too. 

---