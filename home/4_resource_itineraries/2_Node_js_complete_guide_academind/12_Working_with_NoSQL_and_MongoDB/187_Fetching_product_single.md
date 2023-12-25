# 187. Fetching product (single)
Created Tuesday 30 May 2023 at 02:07 am


## `findOne`
Use `.findOne(criteriaOr_id)`

```js
class Product {
// some code here
  static async findById(prodId) {
	const db = getDb();
	
	const product = 
	await db.collection('products')
		.findOne({ _id: prodId }); // _id is inside an Object

	// .findOne(prodId); // also works, matched against `_id`
	
	return product;
  }
}
```

Syntax for find one:
```js
const product = await db.collection('products').findOne({ _id: prodId });
```

**This doesn't work, though. Let's explore why.**


## `_id`argument should be an object
This code doesn't work because `_id` stored inside a MongoDB document is not of type string, and therefore comparison (equal) won't work. 

`_id` is actually a special object called `ObjectId`, specified by MongoDB. It's not a native JS feature. 
![](../../../../assets/187_Fetching_product_single-image-1-6f05df1a.png)

Why is the `_id` like this? Reasons:
1. It is easy to work with in BSON
2. Has the property of uniqueness
3. `_id` generated after (in time) has higher alphabetical rank than ones created before.
4. And more..

*In short, you need to pass `_id` of type `ObjectId` for `findOne` to work.*

## Fixing the code - `mongodb.ObjectId`
- MongoDB provides a utility method to create `_id` (i.e. `ObjectId`) objects.
```js
...find({ _id: prodId }) // doesn't work
// example prodId: "646a3b5193d6e61bddc26c17"


// fix: new mongodb.ObjectId()
const mongodb = require("mongodb");
...find({ _id: new mongodb.ObjectId(prodId)}); // works now
```

- Read is easy, `product._id` will work fine, where `product` is the fetched Product.
- The `ObjectId` constructor is polymorphic and idempotent - it accepts both `ObjectId` or string equivalent.

[Product details page](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/800c8de7b75f875d77e382d80eddf7cb4696a148)


## Pass `_id` directly
If the criteria is only `_id`, passing it directly (instead of in an object) is also OK. `find` and `findOne` both support this.

Avoid this if possible, since explicit is better. Otherwise the code will be hard to work with for new comers like my experience with Rails.

Example:
```js
// .find
// _id in object
const allProducts = await db
        .collection("products")
        .find({_id: new mongodb.ObjectId("6474f8ae83090103435e19d2") }) // as object
        .toArray();

// is the same as - _id passed directly
const allProducts = await db
        .collection("products")
        .find(new mongodb.ObjectId("6474f8ae83090103435e19d2")) // direct
        .toArray();

```

```js
// .fineOne
// _id in object
const product = await db
      .collection("products")
      .findOne({ _id: new mongodb.ObjectId(prodId) }); // object

// is the same as - _id passed directly
 const product = await db
      .collection("products")
      .findOne(new mongodb.ObjectId(prodId)); // direct
```