# 201. Deleting Cart items
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

Code changes completed in a previous page, see - [main code](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/3fb41c3240039365854d4cf00b1e406ef1a3948d),  [minor fix commit](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/2656c19b369d9d55c4038f4601af90744e3ee484)

I refactored the logic into the model. [Code](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/8dcfbe1718662994dde321e7b5afa92a8d3c6dcd)