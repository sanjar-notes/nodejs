# query operators in Mongoose
Created Monday 19 June 2023 at 02:17 am

- The MongoDB query operators work just fine. Already noted [here](obsidian://open?vault=nodejs-notes&file=home%2F4_resource_itineraries%2F2_Node_js_complete_guide_academind%2F12_Working_with_NoSQL_and_MongoDB%2Fextras%2Fquery_operators)

But Mongoose provides a more readable way to write queries with conditions - by chaining the operators.

FIXME: see later. 
- The thing is to use `.where("attributeName")` whose chained functions (name same as MongoDB operators) take their value as argument. 
- The default (implicit) relation between chained operators is 'AND'.
- For complex stuff like AND and OR, the argument becomes an array, just like with MongoDB.
- The structure is similar to Cypress, RSpec's "code as you would say".
- *It may be useful for simple conditionals where the condition for an attribute is made against constants. *Example:
```js
// get all orders with totalAmount between 1000 (inclusive) and 5000

const orders = await Order
  .find(/* some code */)
  .where("totalAmount")
  .gte(1e3)
  .lt(5e3) // implicit AND
  .where("shippingAddress")
  .equals("Cayman Islands");

// some more variations

// #1. shorthand for equals
.where("shippingAddress")
.equals("Cayman Islands");

.where("shippingAddress", "Cayman Islands")


// #2. not equals
.where("shippingAddress")
.ne("Cayman Islands")
```