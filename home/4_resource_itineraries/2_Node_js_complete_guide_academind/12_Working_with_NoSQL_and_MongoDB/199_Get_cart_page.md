## Adding User.getCart method (199)
Created Sunday 7 May 2023 at 12:08 pm

Let's add a new method, that will be used by the cart page controller action.
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

	  const cartWithProducts = productIds.map(async (productId) => {
	     const product = await db
				.collection('products')
				.findOne({ _id: new mongodb.ObjectId(productId) });

		return { ...item, product };
	   });

	  return cartWithProducts;
	}
}
```


'n' network calls are made here. this could be rewritten using `.find()`, so only one call is needed:
```js
let cartWithProducts2 =
	await db.collection('products')
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
Note:
1. Use `toString()` on the `fetchedInstance._id` because even though `._id` feels like a string, it's not strictly of type `string`.
2. MongoDB has the `$in` query operator is quite helpful, especially in `find` (i.e. find many), syntax:
	```js
	const mongodb = require("mongodb");
	const idArr = [42, 6023].map(id => new ObjectId(id));

	const items = await db.collection('something')
	  .find({ _id: { $in: idArr } })
	  .toArray();
	```

Code changes completed in a previous page - https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/3fb41c3240039365854d4cf00b1e406ef1a3948d