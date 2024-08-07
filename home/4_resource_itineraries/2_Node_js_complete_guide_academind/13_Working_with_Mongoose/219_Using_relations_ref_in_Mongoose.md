# 219. Using Relations (`ref`) in Mongoose
Created Sunday 14 May 2023 at 05:03 pm

We added the Product model, but one thing is missing from it. Every product is created by a User (seller). This is a 1-N relation.


## `ref` in Mongoose
Mongoose has a concept of 'references', which are implemented using the `ref` attribute. `ref` is the "lazy loading" construct of Mongoose.

Code:
```js
const ObjectId = Schema.Types.ObjectId;

// Example: the Wearer model. Assume Cloth model exists.
cloth: { ref: 'Cloth' } // myWearer.cloth will of type object

cloth: { ref: 'Cloth', type: String } // myWearer.cloth's type is String
cloth: { ref: 'Cloth', type: ObjectId } // myWearer.cloth's type is ObjectId

// Note: prefer type as ObjectId, it has the most intuitive behavior and is good performance wise too.
```
- The syntax is simple, add the attribute and use the keyword with the name of the model (to be associated).
- By default, a `ref` attribute is "lazy loaded", i.e. accessing the attribute will simply return the `_id` of the associated model, and not the whole document.
- By default, `_id` will be of type `ObjectId`.  This can be changed by specifying the `type:String` along with the ref. Now the `_id` will be a string when accessed.
- The value for the `ref` attribute is a string (the model's name), which may feel naive, but it has a very important reason - it helps avoid cyclic dependencies.


## Experiments - `type` with `ref`.
FIXME_done: check these 3 (no type, type String and type ObjectId) - which is which. The docs are outrageously useless
```js
const anyProductSimple = await Product.findOne();
const anyProductLean = await Product.findOne().lean();
const anyProductPopulate = await Product.findOne().populate("userId");
const anyProductLeanAndPopulate = await Product.findOne()
  .populate("userId")
  .lean();

[
  { prod: anyProductSimple, label: "ProductSimple" },
  { prod: anyProductLean, label: "ProductLean" },
  { prod: anyProductPopulate, label: "ProductPopulate" },
  { prod: anyProductLeanAndPopulate, label: "ProductLeanAndPopulate" },
].forEach(({prod, label}) => {
  console.log(`\n\n${label}`)
  console.log({
    prod,
    keys: Object.keys(prod),
    userStringAsso: prod["userId"],
    userDotAsso: prod.userId,
  });
});
```
Possibilities:
1. Skipping type - error.
2. With String, setting user to the whole object.
	1. Simple - direct key absent, value absent
	2. Lean - direct key present, value is ObjectId
	3. Populate - direct key absent, value is absent
	4. LeanAndPopulate - direct key present, value is whole object
3. With ObjectId - Setting attribute to whole object or just Id has the same behavior.
	1. Simple - direct key absent, value is ObjectId
	2. Lean - direct key present, value is ObjectId
	3. Populate -  direct key absent, value is whole object
	4. LeanAndPopulate - direct key present, value is whole object
4. With type as a schema (i.e. importing userSchema and using here) - doesn't differ much from ObjectId, except stuff is all there.

**Conclusion** - Prefer ref type as ObjectId. The simplest, intuitive and has good performance.

Note: I added a simple way to reset database without having to use Compass - [code](https://github.com/exemplar-codes/online-shop-with-nosql-mongoose/commit/4a1edcd3992cea1fef12cd4f00990940a41a2e06). Toggle this line to reset. It's OFF by default.

## Continuing with the Product model
Let's update the Product model:
```js
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

const productSchema = new Schema({
  title: String,
  price: { type: Number, required: true },
  description: String,
  imageUrl: String,

  userId: { ref: 'User', type: Schema.Types.ObjectId, required: true };
});
```

[Code](https://github.com/exemplar-codes/online-shop-with-nosql-mongoose/commit/aa7c2d8181660e25762c651832023511b4bac245)