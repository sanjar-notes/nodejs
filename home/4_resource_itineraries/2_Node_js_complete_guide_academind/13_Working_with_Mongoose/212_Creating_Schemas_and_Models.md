## 212. Creating Schemas and Models
Created Sunday 7 May 2023 at 08:32 pm (binge)
Created Monday 29 May 2023 at 03:51 am (code)

In the product model file, comment out all the code, and rewrite. 
There are two steps in model creation:
1. Schema - talks only about attributes (data) of the model, does not have any methods
	```js
	const mongoose = require('mongoose');
	const Schema = mongoose.Schema;
	
	const productSchema = new Schema({
	  // id // 1. can be omitted, is auto assigned for all entities
	  
	  title: { type: String, required: true },
	  price: { type: Number, required: true },
	  description: String, // 2. shorthand, required is false by default
	  imageUrl: String,
	});
	```
2. Model - Schema + methods. Adding in the same file.
	```js
	const Product = mongoose.model('Product', productSchema);

	module.exports = Product;
	```

[Product model - code](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/ddbb7ec4b7c22f77af457b38e52218174853a547)