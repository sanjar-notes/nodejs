## Deleting Cart items (201)
Created Sunday 7 May 2023 at 12:26 pm

Basically, just update the cart. Updating the code (User model, since cart is a part of it):
```js
const { getDb, mongoConnect } = require('./util/database.js');
const mongodb = require("mongodb");

class User {
  // existing code

  async deleteItemFromCart(productId) {
	// make sure we don't mutate the existin cart, since the operation may fail

	// .filter is safe
	const updatedCart = this.cart.filter(item => item.productId.toString() !== productId.toString());

	const db = getDb();
	return db
			.collections('users')
			.updateOne(
			  { _id, new mongodb.ObjectId(this.id)},
		      { $set: { cart: updatedCart }}
			);
  }
}
```

Code changes completed in a previous page - https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/3fb41c3240039365854d4cf00b1e406ef1a3948d