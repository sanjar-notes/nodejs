# 214. Fetching products
Created Monday 29 May 2023 at 04:32 am

## Fetching all products (i.e. fetch multiple)
Created Sunday 7 May 2023 at 09:08 pm (binge)

Use the Mongoose provided `find` method. Syntax:
```js
Product.find() // has array behavior by default, unlike pure MongoDB

Product.find().cursor().then(); // also supported: for generator/pagination behavior
```

Let's update the controller:
```js
ShopController.getProducts = (req, res, next) => {
  const allProducts = await Product.find();

  render('./products-list-view', { products: allProducts });
};
```


## 215. Fetching a single product
Created Sunday 7 May 2023 at 09:08 pm
Use the Mongoose provided `findById` method. Syntax:
```js
const product = await Product.findById(prodId);

// a major advantage here is that prodId can be a string, so we don't need to send a mongodb.ObjectId instance
```

Updating the controller:
```js
ShopController.getProducts = async (req, res, next) => {
  const prodId = req.params.productId;
  const product = await Product.findById(prodId);

  render('./product-detail-view', { product });
};
```