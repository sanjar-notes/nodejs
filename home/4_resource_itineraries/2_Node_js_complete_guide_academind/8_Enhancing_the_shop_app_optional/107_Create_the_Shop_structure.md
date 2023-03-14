# 107. Create the Shop structure
Created Tuesday 14 March 2023 at 12:57 am

Note: Forked the project, for this enhancement/practice section (and showoff in resume). [Repo link](https://github.com/exemplar-codes/online-shop-express-ejs-mvc)

## Move views to relevant folders
- Change `res.render()` since views moved.
- Change EJS `include()` path since views moved.
- [Code](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/dea7f61a024da17fb8eca4750c1a48d77b1455f0)


## Add more views (todo)
### Shop
1. Landing page for products - show only popular products, not the whole listing (which is the case now)
2. Product detail page - details for selected project
3. Cart page - see added item, when the cart icon in the navbar is clicked
4. Checkout page - opens from inside the cart page

Both admin and customer admin should not be on the same navigation bar. We'll ignore this for now, work on the UI (i.e. add all links for now), and add handle this later.


### Admin
1. Edit product page
2. Product listing (for admin). Similar to the one views by shop, but only products created by the admin are listed here.

---
## Work

- Add links for the pages we'll be adding. Then, handle the routes, add new controllers.