# 195. Storing associated User in Product
Created Sunday 7 May 2023 at 10:01 am

## Need to store associated models
Created Sunday 7 May 2023 at 10:01 am

Products are created by admin, who are a User too. Consequently, we expect to access products created by a user (given user document), and access the user with a given product document.

This should be thought through clearly, since storing whole objects may result in inconsistencies. Example situation - we saved the whole user object in each product, but after some time, the user changed their username, and therefore all user data in their products are now stale. This is a con, but it also has the advantage that the product as well as the associated user data can be fetched in *one call*.
**Alternatively**, if we just store the user's id in each product, we'd need an extra call (`User.findBy(prod.userId)`) if we wish to know user data associated with a product.

*In other words*, there's a trade-off between extra calls and degree of duplication.

In the current application, the product detail page does not need to show the admin info, so storing whole user object in every product is not needed, storing only the id would be fine.

## Updated Product model
- Add the field `userId`
- Updating model pre-population code - since User can exist without a Product, but every Product is created by some User. Also change the dependency function order, run user then product. Skipping the code here.
```js
class Product {
  constructor(/* existing params, */ userId) {
    // existing code
    
    this.userId = userId;
  }
}
```

[Code](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/6696c8dcd369d3e009d604a3aa21bd7f38cd4574)


## Re-enable mock auth
We also need to re-add the 'mock' authentication middleware, since we need the user for almost all operations. [Code](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/15d08347c88e6d5a83740d1dcd9a38edf8cdf11e)
```js
// Main app file - `app.js`
const app = express();

app.use(async (req, res, next) => {
  const [firstUser = null] = await User.fetchAll(); // as of now, this is the sample user
  req.user = firstUser;
  console.log("Mock authentication success", firstUser);
  next();
});

// ...
```


## Updating the create product action
Every product must have a user, so we only have to change the "Add product" action.
[Code](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/9529d8fb07ac23db3118f53259dada2fa3d7465e)
```js
const postAddProduct = async (req, res, next) => {
  const product = new Product({
    title: req.body.title,
    imageUrl: req.body.imageUrl,
    description: req.body.description,
    price: req.body.price,
    userId: req.user._id, // CHANGE: add userId
  });

  product.create();

  res.redirect("/");
};
```

