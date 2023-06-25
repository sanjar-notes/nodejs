# 213. Saving data through Mongoose
Created Sunday 7 May 2023 at 08:47 pm (binge)
Created Monday 29 May 2023 at 04:08 am (code)

The model code in our controllers will most remain the same. There are a few changes we'll need though:
```js
const Product = require('../models/Product');


const newProduct = new Product(title, price, description, imageUrl);
// will change to
const newProduct = new Product({ title, price, description, imageUrl});


// save remains unchanged, since Mongoose adds a .save for instances
newProduct
	.save()
	.then()
	.catch();

// OR, if you prefer async-await
try { await newProduct.save(); }
catch(e) { }
```
The `.save()` instance method will create a new collection (if it doesn't exist) and add a product in it.

**Collection name** - The collection is named 'products', even though we never specified it. This is because Mongoose, by default, names the collection as a pluralized lowercase of the model name (which we did specify). `Product` --> `products`

**Returns created instance** - Mongoose's `.save()` will return the complete created object, unlike MongoDB (which only returns the `_id`). Convenient!

https://github.com/exemplar-codes/online-shop-with-nosql-mongoose/commit/ddbb7ec4b7c22f77af457b38e52218174853a547 - ignore the `userId` attribute for now, assume it's absent. We'll look at associations later.

## Shorthand - `.create`
```js
// construct + .save()
const newProduct = new Product({/* stuff */});
const newSavedProduct = await newProduct.save();


// can be shortened to .create
const newSavedProduct = Product.create({/* stuff */});
```
Returns created document. The return value is the same as `new MyModel()` with `.save`