# limit, sort and count
Created Monday 19 June 2023 at 01:14 am

## 1. limit
Number of items returned can be limited by chaining the `.limit` method to `.find`.
```js
const orders = await db
  .collection("orders")
  .find(/* some code */)
  .limit(2)
  .toArray();
```

Note: 0 has no effect. Negative values behave the same as positive values.


## 2. sort
Items returned can be sorted by chaining `.sort` to `.find` (or similar)

It's the same as MongoDB's `.sort`, except that `0` is a valid direction (behaves the same as `1`, i.e. normal sort direction). FIXME: check once.

Example:
```js
const orders = await Order
  .find(/* some code */)
  .sort({ shippingAddress: 1 });


// multi 
const orders = await Order
  .find(/* some code */)
  .sort({ shippingAddress: 1, phoneCode: -1 })
  // phone code will apply among documents with matching addresses
```


## 3. count
Chain `.count` to `.find`. Argument is a "filter". Returns a number
```js
const numberOfOrders = await Order
  .find(/* some code */)
  .count();
```
