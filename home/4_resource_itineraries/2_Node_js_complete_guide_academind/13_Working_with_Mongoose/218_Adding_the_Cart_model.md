# 218. Adding the Cart model
Created Thursday 11 May 2023 at 06:45 am

We'll can the cart here itself, as we did earlier with [vanilla](obsidian://open?vault=nodejs-notes&file=home%2F4_resource_itineraries%2F2_Node_js_complete_guide_academind%2F12_Working_with_NoSQL_and_MongoDB%2F196) MongoDB.

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
Basically, we learnt about model syntax for nested fields, in Mongoose.


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
No types needed, just use the Schema directly.


- [Model code](https://github.com/exemplar-codes/online-shop-with-nosql-mongoose/commit/3e58f32012c98a14a4bb2a542b32245108cc7674)
- [Cart features code](https://github.com/exemplar-codes/online-shop-with-nosql-mongoose/commit/5094391a7e41ec0dcb5b6c30736f1da8ee59829b)