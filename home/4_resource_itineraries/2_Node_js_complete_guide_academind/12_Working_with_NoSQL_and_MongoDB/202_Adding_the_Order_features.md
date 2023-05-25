## Adding the Order features
Created Sunday 7 May 2023 at 12:41 pm

Let's add the order features. Since an order is a "frozen" copy of a cart, this will be a little different - it doesn't make much sense to have an `orders` attribute in the User model, since there may be a lot of orders, which will make User objects very big.

Instead, we can create a new collection called 'orders', that stores all orders, irrespective of users. [Code - commit](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/3c5e62b988aee31e1fc8c51241aa744922ca6326)
```js
Orders = [{ userId, items: [{ product, quantity }] }]
```
Note: we need to store the whole product, instead of just the id, since Order is a history/frozen entity, and so, it should remain safe from product updates.

code:
```js
const { getDb, mongoConnect } = require('./util/database.js');
const mongodb = require("mongodb");

class User {
  // existing code

  async addOrder() {
    const db = getDb();

	// store the cart, but with all things frozen
	// cart stores productId not whole products, this is not good
	// we need whole products
	const cartWithProducts = await this.getCart(); // use existing method

	// store the cart, and user (since cart doesn't have `user`)
	await db
			.collection('orders')
			.insertOne(
			  {
			    ...this.cart,
			    user: {
				  _id: mongodb.ObjectId(this.id)
				  username: this.username,
				  email: this.email,
				}
				// user duplication is OK here
				// even if it may become inconsistent
			  }
			)

	// empty cart - effective completing the "freezing" requirement
	await db
			.collection('users')
			.updateOne(
			  { _id: mongodb.ObjectId(this.id) },
			  { $set: { cart: { items: [] } } }
			);

	return this;
  }
}
```
Note: since the *create* payload was `this.cart`, it included cart's `_id`. But this will not be saved in the new order, because this is a create call. In other words, we don't need to remove `_id` from the payload, since it's irrelevant in a create call.
