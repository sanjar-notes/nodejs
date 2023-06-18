# limit, sort and count

## 1. limit
Created Monday 19 June 2023 at 12:50 am

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

Argument is an object.
- Default value is `{}` (no-effect). Empty value is OK too.
- Argument can have multiple parameters. Their job is "tie-breaking" - the successive criteria are apply only if documents match with all seen (on the left criteria).

Directions:
- `1` means normal sort (i.e. alphabetical, low to high)
- `-1` means non-normal sort.
- `0` is an invalid direction, will raise an error.

Default MongoDB sort is with respect to `_id`, and in normal (`1`) direction.

Example:
```js
const orders = await db
  .collection("orders")
  .find(/* some code */)
  .sort({ shippingAddress: 1 })
  .toArray();


// multi 
const orders = await db
  .collection("orders")
  .find(/* some code */)
  .sort({ shippingAddress: 1, phoneCode: -1 })
  // phone code will apply among documents with matching addresses
  .toArray();
```


## 3. count
Chain `.count` to `.find`. Argument is a "filter". Returns a number
```js
const numberOfOrders = await db
  .collection("orders")
  .find(/* some code */)
  .count();
```
