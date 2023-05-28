## Getting orders
This is very simple, from a *joins* perspective, since an order has a high degree of duplicates, i.e. no joins/extra calls are needed.

There's a different problem here, though. We don't store anything related to order in the User model, and therefore we don't know the orderIds. Consequently, we need to query the "orders" collection with a condition of `user._id` since we every order does have the `user` object. MongoDB syntax for nested matching:
```js
const { getDb, mongoConnect } = require('./util/database.js');
const mongodb = require("mongodb");

class User {
  // existing code

  async getOrders () {
    // .find({_id: { $in: [??]}}) // can't use, since we don't know orderIds

	const db = getDb();

	return db
			.collection('orders')
			.find({ "user._id": new mongodb.ObjectId(this.id) });
  }
}
```

This syntax is not something new/different, as compared to using `_id` - we just changed the key to be `user._id`. The **important thing** is to know that MongoDB supports queries with nested keys.

Note: I wrote the code later, and the id key was changed to `userId`.
[Code - Order listing and detail page](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/a07f8f5d9c93a08b90d07c958515f074f4515f82)


## Cleaning up isolated products
Situation: A user (seller) creates a product, which is then "added to cart" by multiple other users (buyers). The seller than deletes the product. Now, we have the product references in carts that doesn't actually exist, in other words, the carts are now inconsistent.

This is bad because the user expects that the "ordering" will succeed, which is not possible now and will fail technically. We should actually show a warning here, or atleast make the cart consistent - in other words, this case should be handled specially, as opposed to a just a 500.

There are many ways to solve this problem:
1. During the `getCart` operation, we query the 'products' collections too, to get product details. We can simply add a check here, to see if the query returns the same number of products as items in the cart. If not, there is a product that has been deleted. Since we know which one has been deleted - we can either show a "unavailable" message or simply delete the item from the cart.
2. The above method works at request time (when "Order now" is pressed), and may be slow. We can solve this problem, by actually running a planned *job* every 24 hours (or some other period), where we go through all carts and remove the items whose product has been deleted.
   
Of course, the "periodic sweep" approach could mean that our server spends time on Carts (users) who have not used our app in a long time - which can be significantly expensive. A hybrid approach would be better - we could use some criteria (or ML) based filter so only users who shop regularly are part of this periodic sweep and their carts are marked 'sweeped'. This way, we can have both "periodic sweep" as well as request time cleanup, but the request time one is skipped for regular users, since their carts have the "sweeped" label. Also, if a user tries to order but he is not a regular one, the request time cleanup should run of course.

This is briefly discussed in the course, but not demonstrated or anything. I think this will be easy enough to do (from an backend perspective, not the criteria or ML part). So skipping the code part.