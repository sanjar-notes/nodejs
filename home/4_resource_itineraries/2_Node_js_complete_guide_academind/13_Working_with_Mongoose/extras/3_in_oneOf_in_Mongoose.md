# `in` (oneOf) operator
Created Monday 19 June 2023 at 02:52 am

- The MongoDB `$in` and `$nin` (inside the `.find()`) work just fine. Already noted [here](obsidian://open?vault=nodejs-notes&file=home%2F4_resource_itineraries%2F2_Node_js_complete_guide_academind%2F12_Working_with_NoSQL_and_MongoDB%2Fextras%2F3_in_oneOf)

But, just like with other query operators, Mongoose provides a more readable way to write queries with conditions - by chaining the operators.

## Syntax
- Use `.where` along with `.in` (or `.nin`), chained to `.find`.
- The value is an array, obviously.
```js
// Get all orders bound for India and USA
const orders = await Order
  .find()
  .where("shippingAddress")
  .in(["India", "USA"])

// Get all orders, except those bound for India and USA
const orders = await Order.find()
  .find()
  .where("shippingAddress")
  .nin(["India", "USA"])
```