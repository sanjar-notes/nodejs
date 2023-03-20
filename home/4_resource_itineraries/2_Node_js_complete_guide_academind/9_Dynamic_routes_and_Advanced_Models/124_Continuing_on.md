# 124. Using Query Params
Created Monday 20 March 2023 at 08:36 pm

## Edit product page
Let's work on the edit-product page. The edit-product page (makes sense for a given product only) should be a pre-populated form, containing existing title, price and other information about the product.

To handle the update operation, we'll accept a POST request and update the product.

---
The "edit page" will look exactly like the "add-product" page, except that:
1. It's loaded for a specific product. `/edit-product/:id`
2. It's pre-populated with the product information
3. For submission makes a POST request to `/edit-product/:id`.

We can reuse the add-product page (view). Better, we can a single view and optionally pass an `edit` boolean, which will be false for add-page but true for edit-page. [Code](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/a342b762df03cce4f73d720cbc05cd63407b4f90)

Pre-populating product info in edit page. Pass the existing info as `value` attribute of the `<input />`. For the text area, pass the info between the `textarea` tags (take care of white-space). **`<input />` with the `value` attribute can be edited normally.** [Code](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/8a97d6e0ff58406d86f25fb39a797229374de7be)


## Delete product
Button exists already, just add the endpoint. [Code](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/ad6f98248b84f8dd858658a0622e73b365f6d188)

Note: Since `<form method= />` can only be "get" or "post". We are sending a POST request to handle deletion. This is not ideal, but OK since we are avoiding JavaScript (fixme, anyway to send DELETE request without JS?).


## Delete cart item
Add button under product detail page. Add endpoint.

Ignoring errors:
1. Product id is invalid
2. Product is in cart, but has been deleted by admin

[Code](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/8e411170a801c64a86d6522f6f798c7e01006099)


## Show cart items
- Major thing is the table - filter out available products, and quantity in cart.
- Add plus, minus and remove item functionality. Copy add to cart functionality that exists already. Write code for the remaining two, from scratch.

[Code](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/6126819bf6be838c56a2acc99d6a3c9d50193e3b)