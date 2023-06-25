# 196. The Cart model
Created Sunday 7 May 2023 at 10:16 am

Since MongoDB allows nested docs by default, we don't need something like `CartItem` here - we can store an array (CartItems) in the same (User) document.

Also, since the User and Cart are 1-1 related and never transferred to other entities, we don't need a `Cart` model, we could just add a `cart` attribute to the User model itself.

Deleting Cart, CartItem, and updating User:
```js
const { getDb, mongoConnect } = require('./util/database.js');
const mongodb = require("mongodb");

class User {
  constructor(/* existing params, */, cart) {
    // existing code

    this.cart = cart ?? { items: [] };
    // typeof cart = { items: [{ ...product, quantity }] }
  }

  async addToCart(product, quantity = 1) {
	const existingIndex = cart.items.findIndex(item => item.product._id === product._id);

	if(existingIndex === -1 )
      this.cart.items.push({...product, quantity });
    else
	  this.card.items[existingIndex].quantity += quantity;

	const db = getDb();

	return db
			.collection('users')
			.updateOne(
				{ _id: new mongodb.ObjectId(this.id) },
				{ $set: { cart: this.cart } }
			)
			.then(result => { console.log(result); return result; });
			.catch(console.log);
  }
}
```


## Duplication in User.cart (197)
Right now, we actually save whole `Product`s in `User.cart`. This is not very good, since Product details may change frequently (e.g. the price), and our cart will then have stale product objects.

To fix this, let's just store the `productId` instead of the whole object. We will need an extra call for each item in the cart page to get product details, of course, but it's fine.

Update User (since cart is just a part of User now)
```js
const { getDb, mongoConnect } = require('./util/database.js');
const mongodb = require("mongodb");

class User {
  constructor(/* existing params, */, cart) {
    // existing code

    this.cart = cart ?? { items: [] };
    // typeof cart = { items: [{ ...product, quantity }] }
  }

  async addToCart(productId, quantity = 1) {
	const existingIndex = cart.items.findIndex(item => item.product._id.toString() === productId);

	if(existingIndex === -1 )
      this.cart.items.push(
	      { productId: new mongodb.ObjectId(productId), quantity }
	  );
    else
	  this.card.items[existingIndex].quantity += quantity;

	const db = getDb();

	return db
			.collection('users')
			.updateOne(
				{ _id: new mongodb.ObjectId(this.id) },
				{ $set: { cart: this.cart } }
			)
			.then(result => { console.log(result); return result; });
			.catch(console.log);
  }
}
```


Stuff done here:
1. Add cart model, as a nested field in User model. Reason: cart is guaranteed to be present and also be relevant only to one (something even tighter than 1-1, where swaps and null are possible) User at all times.
2. Add cart features.
3. Solved the cart action button bugs. This was happening because we used `productId` as the id of the cartItem. Should probably avoid this in the future - let every entity have it's own `id` (and also that `id` attribute name is the same for all). This way `_id` is the expected key instead of `productId` or whatever context dependent key.

[Code](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/3fb41c3240039365854d4cf00b1e406ef1a3948d)

[Code - fix for a bug - price, description and other keys were missing](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/2656c19b369d9d55c4038f4601af90744e3ee484)