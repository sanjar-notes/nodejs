# query operators
Created Monday 19 June 2023 at 01:34 am

For the whole list - see [official MongoDB docs](https://www.mongodb.com/docs/v6.0/reference/operator/query-element/).

Currently, all our queries (filters) are "exact matches". How do we make filters with more complex conditions.

The primary where way to this is through "query operators".

## 1. Comparison
Here is the list:
1. `$eq` - "is equal to". This is the default. Example: `{ price: { $eq: 23 }}`. This is the same as `{ price: 23 }`.
2. `$ne` - "not equal to".
3. `$gt` - "greater than"
4. `$gte` - "greater than or equal to"
5. `$lt` - "less than"
6. `$lte` - "less than or equal"

Example:
```js
// get orders with total >= 1000
 const orders = await db
      .collection("orders")
      .find({ totalAmount: { $lte: 1000 } })
```


## 2. Logical operator (AND and OR).
The value of the operator here is an array. Obviously.

The operator list:
1. `$not` - logical NOT
2. `$and` - logical AND
3. `$or` - logical OR
4. `$nor` - true if all conditions are false.

Note: these operators apply as 'root'. They can't apply with other abstract operators. mAid - The other way doesn't make sense anyway, it conflicts with `$eq`.

- Syntax (AND and OR, combo) - both operators enclose the attribute. See mAid above. Makes sense from a math notation perspective too.
	```js
	// basic - single operator
	// get orders with total between 1000 (inclusive) and 5000
	const orders = await db
	  .collection("orders")
	  .find({
	
		$and: 
		  [
		    { totalAmount: { $gte: 1e3 } }, 
		    { totalAmount: { $lt: 5e3 } }
		  ],
		
	    })
	
	
	// #2. combine
	// each array element must be a valid filter
	
	// get all normal priced orders, but include all high price Cayman Islands orders too.
	const orders = await db
	  .collection("orders")
	  .find({
	  
	    $and: [
	    
	      { totalAmount: { $gte: 1e3 } },
	      {
	        $or: [
	          { totalAmount: { $lte: 5e3 } },
	          { shippingAddress: "Cayman Islands" },
	        ],
	      },
	      
	    ],
	  })
	
	```
- Syntax (`$not`) - it's a little different, `$not` is nested as a value of attribute.
	```js
	// get all orders bound to planets other than Earth
	const orders = await db
	  .collection("orders")
	  .find({
	    shippingPlanet: { $not: { $eq: "Earth" } }
	  })	
	```

Example (combine all 3)
```js
// get all medium-expensive orders (not expensive) not bound for mars
// include all high-expensive orders bound for Cayman Islands in this
orders = await db
  .collection("orders")
  .find({
	$and: [
	  { totalAmount: { $gte: 1e3 } },
	  {
		$or: [
		  { totalAmount: { $lte: 5e3 } },
		  { shippingAddress: "Cayman Islands" },
		],
	  },
	  {
		shippingPlanet: { $not: { $eq: "Mars" } },
	  },
	],
  })
```