# 224. Adding the Order model and features
Created Friday 19 May 2023 at 12:10 am

Let's add the product model - [code - commit](https://github.com/exemplar-codes/online-shop-with-nosql-mongoose/commit/616d6cf3923735f756f08cadd92d586f4ea6fcc8). Example:
```js
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

const orderSchema = new Schema({
	// cart: CartModel, // invalid, since cart is not a separate model
	products: [
		{
			product:  { type: Object, required: true }, // general storage
			quantity: { type: Number, required: true },
		}
	],
	total: { type: Number, required: true },
	user: {
		// enumerating all, since we don't want the cart here
		name: { type: String, required: true },
		userId: { 
			ref: 'User', 
			type: Schema.Types.ObjectId, 
			required: true 
		},
	},
});


module.exports = mongoose.model('Order', orderSchema);
```

Then, the controller action can be changed. I'm assuming this is easy to do, so skipping. [Code](https://github.com/exemplar-codes/online-shop-with-nosql-mongoose/commit/384321f5790c43a56a7bb31a8ddc9dd2ce5e282a)

One potential caveat `myBook.authorId` (even if `authorId` was populated) may not work, replace the code by this `{...myBook.authorId._doc}`. FIXME: I think this is not an issue, remove it if it's not.