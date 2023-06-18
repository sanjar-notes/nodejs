# `in` (oneOf) operator
Created Monday 19 June 2023 at 02:38 am

## 1. `$in`
`$in` is a query operator. A better name for it would have been "oneOf".
It takes an array as value, and the filter matches when the DB attribute (document's) has a value that's one of the payload.

Better to show (example):
```js
// get all orders bound for India India and the US
// i.e. shippingAdress is one of ["India", "USA"]
const orders = await db
  .collection("orders")
  .find({
	shippingAddress: { $in: ["India", "USA"] },
	
	// `oneOf` would have been a better name (instead of `in`)
  })
```


#ignorable Technically, `$in` is equivalent to an OR with equals.
```js
const orders = await db
  .collection("orders")
  .find({
	$or: [
	  {  shippingAddress: "India" },
	  {  shippingAddress:   "USA" }
	]
	
	// `oneOf` would have been a better name (instead of `in`)
  })
```


## 2. `$nin`
`$in` has an opposite, named `$nin`. A better name for this would have been "notOneOf".
```js
// get all orders that are not bound for India or USA

const orders = await db
  .collection("orders")
  .find({
	shippingAddress: { $nin: ["India", "USA"] },

	// `notOneOf` would have been a better name (instead of `nin`)
  })
```

#ignorable Technically, `$nin` is equivalent to an NOR with equals.