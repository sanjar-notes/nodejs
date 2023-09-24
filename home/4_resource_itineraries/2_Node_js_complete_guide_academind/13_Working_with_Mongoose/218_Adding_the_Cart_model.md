---
tags:
  - nested-schemas
  - mongoose
---
# 218. Adding the Cart model
Created Thursday 11 May 2023 at 06:45 am

We'll the cart here itself, as we did earlier with [vanilla](obsidian://open?vault=nodejs-notes&file=home%2F4_resource_itineraries%2F2_Node_js_complete_guide_academind%2F12_Working_with_NoSQL_and_MongoDB%2F196) MongoDB.

```js
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

const userSchema = new Schema({
  name : { type: String, required: true },
  email: { type: String, required: true },

  cart: {
    // doesn't need a `type` since it's an object we are going to define
    
    // `required` can be specified since it's about the existence of the key `cart` itself. BUT THIS GIVES AN ERROR, FIXME: why?

    items: [
		    // array is also self-descriptive, no `type` needed
	  {
        productId: {
          // types needed here because we are at the last level
          type: Schema.Types.ObjectId,
          required: true,
        },
        quantity: { type: Number, required: true },
      },
    ]
  }
});

module.export = mongoose.model('User', userSchema);
```
Basically, we learnt about model syntax for nested fields and arrays, in Mongoose.

Note:
- **Arrays are a first class construct** in MongoDB, and they don't have a id, therefore, they don't need a type schema etc. Also, empty arrays will be initialized automatically if a schema has an array. Nice. *In other words, from a Schema POV, arrays are treated as simple containers.*
	- Array _elements_ will be assigned an `_id`, even if they are not a Schema/model/ref.
	```js
	const productSchema = new mongoose.Schema({
	  price: { type: Number, required: true },
	  title: { type: String, required: true },
	
	  versionArray: [{
	    // each element, like this, will be given an _id
	    
	    name: { type: String, default: "def version" },
	    description: { type: String, default: "def desc" },
	  }],
	});
	```
- **Plain objects are also a first class construct** in MongoDB, so there's no need for a type. *In other words, from a Schema POV, plain objects are treated as simple containers.*  Consequently, they won't get an `_id`. This holds recursively too. Example:
	```js
	const productSchema = new mongoose.Schema({
	  price: { type: Number, required: true },
	  title: { type: String, required: true },
	
	  version: {
	    // the db instance of this won't have an `_id`, it will just have name and description fields
	    
	    name: { type: String, default: "def version" },
	    description: { type: String, default: "def desc" },
	  },
	});
	```
- By default, `_id` is assigned automatically to
	1. Model instances. Expected behavior.
	2. Elements of an array, unless they are scalar values. Not expected but a good default. <details><summary>See thought</summary>This is interesting - plain elements are not part of any model, and don't reside in their dedicated collection, just saying. This is very helpful anyway, since using index as primary key is bad, and an extra argument just for doing it would have been extra work.</details>


## Reusing existing Schemas
Just showing that this is possible. The existing userSchema:
```js
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

const userSchema = new Schema({
  name : { type: String, required: true },
  email: { type: String, required: true },

  cart: {
    // items: [String] // syntax example
    // items: [{ type: String, required: false }] // syntax example
    items: [
      { 
        productId: { type: Schema.Types.ObjectId, required: true }, 
        quantity: { type: Number, required: true } 
      }
    ]
  }
});
```
could be rewritten as:
```js
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

const CartItem = new Schema({
	productId: { type: Schema.Types.ObjectId, required: true }, 
	quantity: { type: Number, required: true } 
});

const userSchema = new Schema({
  name : { type: String, required: true },
  email: { type: String, required: true },

  cart: {
    items: [CartItem] // this is fine
    
    // or equivalently (FIXME: got no errors, but check again)
    items: [{ type: CartItem }]
  }
});
```
No explicit types needed, just reuse the Schema directly.

Note: `CartItem` is a Schema, but has no 'model' (i.e. no dedicated collection). This is fine, and is the reason why `Schema` and `Model` exist as two different concepts in Mongoose. We could attach utility methods on such interstitial `Schema`s, making out business logic code leaner.

- [Model code](https://github.com/exemplar-codes/online-shop-with-nosql-mongoose/commit/3e58f32012c98a14a4bb2a542b32245108cc7674)
- [Cart features code](https://github.com/exemplar-codes/online-shop-with-nosql-mongoose/commit/5094391a7e41ec0dcb5b6c30736f1da8ee59829b)