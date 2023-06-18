# 229. timestamps
Created Sunday 18 June 2023 at 08:46 pm

Mongoose, by default, doesn't store instance timestamps `createdAt` and `updatedAt`.

To enable them, set `timestamps` to `true` in the model's Schema config. Example:
```js
const mongoose = require("mongoose");

const OrderSchema = new mongoose.Schema(
  { userId: 'some code', shippingAddress: 'some code' },
  {
    timestamps: true, // here
  }
);

const Order = mongoose.model("Order", OrderSchema);
module.exports = { Order };
```
`createdAt` and `updatedAt` fields are now available on all model instances.

## Extracting time from `ObjectId`
MongoDB provides a utility `OjectId.getTimestamp`. It's an instance method on `ObjectId`.
```js
const documentCreatedAt = new ObjectId(user._id).getTimestamp();
```


## Extracting time from `ObjectId` (without utility)
`ObjectId` encode useful information within them. The document creation time is one of it, and can be extracted like so.
```js
// using plain JS - if mongodb or mongoose is not available
function dateFromObjectId(_id) {
	// time is stored in hexadecimal, in microseconds
	// getting the decimal equivalent, in milliseconds - for `Date`
    return new Date(parseInt(_id.toString().slice(0,8), 16) * 1000);
}
dateFromObjectId(user._id);

```