# 212. Creating Schemas and Models
Created Sunday 7 May 2023 at 08:32 pm (binge)
Created Monday 29 May 2023 at 03:51 am (code)

In the product model file, comment out all the code, and rewrite.
There are two steps in model creation:
1. Schema - this is a abstract blueprint of a "model", it may or may not have a corresponding collection.
	```js
	const mongoose = require('mongoose');
	const Schema = mongoose.Schema;
	
	const productSchema = new Schema({
	  // id // 1. can be omitted, is auto assigned for all entities
	  
	  title: { type: String, required: true },
	  price: { type: Number, required: true },
	  description: String, // 2. shorthand, required is false by default
	  imageUrl: String, // `required` is false by default
	});
	```
2. Model - created from Schemas, represents a collection. Adding in the same file.
	```js
	const Product = mongoose.model('Product', productSchema);

	module.exports = Product;
	```

Note: Mongoose adds `_id` field to every model by default. So it can be omitted from the Schema.

[Product model - code](https://github.com/exemplar-codes/online-shop-with-nosql-mongoose/commit/ddbb7ec4b7c22f77af457b38e52218174853a547)