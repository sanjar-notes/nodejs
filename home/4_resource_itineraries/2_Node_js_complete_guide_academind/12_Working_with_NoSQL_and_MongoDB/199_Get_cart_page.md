# 199. Adding User.getCart method
Created Sunday 7 May 2023 at 12:08 pm

Let's add a new method, that will be used by the cart page controller action. [Code - commit](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/2656c19b369d9d55c4038f4601af90744e3ee484)
```js
const { getDb, mongoConnect } = require('./util/database.js');
const mongodb = require("mongodb");

class User {
	// existing code

	getCart() {
	  const user = req.user;
	  const cart = user.cart;

	  const db = getDb();

	  const productIds = cart.items.map(item => item.productId);

	// have to use Promise.all, 
	// since using map directly doesn't work with async functions
	// which evaluate to promises, not the resolved value
	const cartWithProducts = await Promise.all(
		productIds.map(async (productId) => {
			const product = await Product.findById(productId);
			return { ...item, product }; // spread item for 'quantity'
		});

	return cartWithProducts;
	}
}
```

'n' network calls are made here. this could be rewritten using `.find()` with `$in`, so that only one call is needed, like so:
```js
let cartWithProducts2 =
	await db.collection('products')
			// get all products whose `_id` is "oneOf" (in) the given array
			.find({ _id: { $in: productIds }})
			.toArray();

cartWithProducts2 = cartWithProducts2.map((product) =>
	({
	    ...product,
	    quantity:
		  cart.find(item => item.productId === product._id.toString())
			  .quantity
	})
);

return cartWithProducts2;
```

[Code - $in operator instead of n calls](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/e8f4f4a26633a2671f2ffb0843c04e812a6a0318)

Note:
1. Use `toString()` on the `fetchedInstance._id` because even though `._id` feels like a string, it's not strictly of type `string`. This will cause `Array.find` to fail, here.
2. MongoDB has the `$in` query operator that is quite helpful, especially in `find` (i.e. find many), syntax:
	```js
	const mongodb = require("mongodb");
	const idArr = [42, 6023].map(id => new ObjectId(id));

	const items = await db.collection('something')
	  .find({ _id: { $in: idArr } })
	  .toArray();
	```
3. The order of elements in array passed to `.find` with `$in` is does not affect the response order. FIXME: is there another operator to specify to follow order from passed array.