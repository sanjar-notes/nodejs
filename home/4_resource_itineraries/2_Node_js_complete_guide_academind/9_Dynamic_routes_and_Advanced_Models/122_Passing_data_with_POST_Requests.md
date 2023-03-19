# 122. Passing data with POST Requests
Created Sunday 19 March 2023 at 10:55 pm

[Code at this point](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/4351719113ea11bacc7fd0255815a2df6a76149b)

Since the "Add to cart" is a POST request, we should pass the data not as a dynamic route but as a body.

Steps to access POST request's body as form data:
1. Parse the body properly - using `express.urlencoded` middleware.
2. Access the body - `req.body`. In this case it's an object with keys as "name" attributes used in the form.

[Code](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/6dc2c5e735e932692407dbceccb80ae0e9f33e2b)

Of course, the middleware needs to be used only once. It's usually kept in the root router (`app`), to avoid clutter in specific routers.

Note: GET requests cannot have a body, as per modern HTTP. So dynamic data is passed as dynamic params (ignore custom headers for now).


## Passing form from the frontend
The usual, 
1. Specify the `method` and `action` attributes on the form
2. Use `name` attribute in the `input` tags.
3. If the form is to merely act as submit button, the `<input type="hidden" />` can be used, to hide the `<input />` UI. Of course, a `name` and `value` is still needed.

Example:
```html
<form action="/cart" method="POST" >
  <input type="hidden" name="productId"  value="34" />
  <button type="submit" class="btn">Add to Cart</button>
</form>
```