# 214. Fetching products
Created Monday 29 May 2023 at 04:32 am

[Code](https://github.com/exemplar-codes/online-shop-with-nosql-mongoose/commit/8be419a93fb9639e5999dc9b5573253092930e64)

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

Note: Just like MongoDB - no arguments for `.find` means 'get everything'.


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

Note: Just like MongoDB - no arguments for `.findOne` means 'get any'.


## Mongoose allows for string `_id`, mostly
MongoDB is strict about values given to it for `_id` - they should be of type ObjectId.

Mongoose is more flexible with this, as it works fine even if the string equivalent is used. This behavior is consistent across all query methods.

There is a caveat though - `_id` argument passed as direct string (as opposed to in an object) doesn't work. Details:
- Passing direct `_id` works only if it's passed as an ObjectId - string won't work.
- When `_id` is passed in an object, both string or ObjectId work.
```js
const Product = require('./path-to-models/Product');
const mongoose = require("mongoose");
const ObjectId = mongoose.mongo.ObjectId;


Product.find(new ObjectId("6474f8ae83090103435e19d1"));         // ok
Product.find({ _id: "6474f8ae83090103435e19d1"});               // ok
Product.find({ _id: new ObjectId("6474f8ae83090103435e19d1")}); // ok

Product.find("6474f8ae83090103435e19d1"); // fails - direct string
```


```js
Product.findOne(new ObjectId("6474f8ae83090103435e19d1"));         // ok
Product.findOne({ _id: "6474f8ae83090103435e19d1"});               // ok
Product.findOne({ _id: new ObjectId("6474f8ae83090103435e19d1")}); // ok

Product.findOne("6474f8ae83090103435e19d1"); // fails - direct string
```
For the `.findOne` case (above), Mongoose does provide a function that allows `_id` as direct string argument. It's called `.findById`. Example:
```js
Product.findById("6474f8ae83090103435e19d1"); // works !

// findById accepts ObjectId too
Product.findById(new ObjectId("6474f8ae83090103435e19d1")); // works
```

[Code](https://github.com/exemplar-codes/online-shop-with-nosql-mongoose/commit/8791ad4e6be63cff915ed2f8e8163ad8f98c6e66)

Note: this behavior of `*ById` accepting both (string or ObjectId) directly and other ones needing it in an object (string and ObjectId both accepted), is consistent for all query methods.