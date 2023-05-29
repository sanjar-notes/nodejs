# 202. Adding the Order features
Created Sunday 7 May 2023 at 12:41 pm

Let's add the order features. Since an order is a "frozen" copy of a cart, this will be a little different - it doesn't make much sense to have an `orders` attribute in the User model, since there may be a lot of orders, which will make User objects very big.

Instead, we can create a new collection called 'orders', that stores all orders, irrespective of users. [Code - commit](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/3c5e62b988aee31e1fc8c51241aa744922ca6326)
```js
Orders = [{ userId, items: [{ product, quantity }] }]
```
Note: we need to store the whole product, instead of just the id, since Order is a history/frozen entity, and so, it should remain safe from product updates.

[Code - commit](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/b1c4b0ca1d5af634c21a7f6cf975aec6c3ee547e):
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
Note: 
1. `_id` in create call: since the *create* payload was `this.cart`, it included cart's `_id`. But this will not be saved in the new order, because this is a create call. In other words, **we don't need to remove `_id` from the payload, since it's irrelevant in a create call in MongoDB.**
2. Traceability - "orders" is a different collection from "users", which is fine. What is not good is that the User model has no indication of order in it's constructor. [See detail](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/a50463c4debcedc88698783e0852712469d8b7cb)

---

Adding shipping address and stuff - [code - commit](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/42bbac277747938a1599f17b07b929047191d5bf)