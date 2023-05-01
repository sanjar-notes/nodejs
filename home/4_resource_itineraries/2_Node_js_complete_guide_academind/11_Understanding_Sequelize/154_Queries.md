# 154. Queries
Created Tuesday 28 March 2023 at 12:05 am
Created 

Models created using Sequelize expose a lot of functionality (the core ORM) part. This functionality may be static or non-static methods, or even properties.

## Raw queries with Sequelize
```js
const sequelize = require('./sequelize');

// 1. simplest
const [rows, metadata] = await sequelize.query("SELECT * FROM products");


// 2. escape parts of the query
// placeholder is ?, values in the `replacements` array in the second argument
// behaves the same as mysql2
const [rows, metadata] = await sequelize.query("SELECT * FROM ?", 
	{ replacements: ["products"] }
);


// 3. Get the tablename from Model - .getTableName()
// Why am I not using escape-placeholders ? Because this is not allowed on MySQL's level. Have to do good old format string
const Product = require('./model/Product')
const tableName = Product.getTableName();
const [rows, metadata] = await sequelize.query(`SELECT * FROM ${tableName}`);


// 4. Note - pass the query `type` option to avoid double network consumption
const [rows, metadata] = await sequelize.query(`SELECT * FROM characters`);
// 'metadata' is the same as 'rows' here, waste of network

// this is better
const Sequelize = require('sequelize');
const rows = await sequelize.query(`SELECT * FROM characters`, 
	{ type: Sequelize.QueryTypes.SELECT }
);
```

Note:
- MySQL doesn't allow escaped values for table names, and column names. This becomes important when using raw queries using `mysql2` or "sequelize.`query()`". Workaround - use usual JS format string.
- To avoid wasteful metadata (second element in the response "sequelize.`query()`"), provide  the query "type" in the second argument of `.query()`.


## ORM queries (CRUD)
### Read
1. `MyModel.findAll([, options = {}])`
	```js
	const Product = require("../models/Product.js"); 
	// created using `sequelize.define(...)`, where `sequelize = new Sequelize(...)`
	
	// 1. get all, i.e. SELECT *
	const productsArray = Product.findAll();

	// 2. get all, but chosen attributes only. SELECT x, y, z
	const productsArray = Product.findAll({
		attributes: ['title', 'imageUrl']
	});

	// 3. get all, but change column name. 
	// Element is array ([original, alias]) instead of string
	// mixing is possible
	const productsArray = Product.findAll({
		attributes: [
		    ['title', 'myTitle'],
		    'price',
		    ['description', 'whatIsIt']
	});
	```
2. `MyModel.findById(id, [, optionsObject={}])`
	```js
	const Product = require("../models/Product.js");

	// get the product with matching id (assuming id is the primary key)
	await Product.findById(1);

	// get product, but only chisen attributes
	await Product.findById(1, {
		attributes: ['title', 'imageUrl']
	})

	// get product, but change some column names
	await Product.findBy(1, {
		attributes: [
		    ['title', 'myTitle'],
		    'price',
		    ['description', 'whatIsIt']
	})
	```

FIXME:  Sequelize does not respect the attributes array in that it forcibly returns the associated columns even if they are not in the attributes array. There's no easy way around this. e.g.
```js
const products = await cart.getProducts({
  attributes: ["id", "title", "price", "imageUrl", "description"],
  raw: true,
});

// returns the following. Problem: 'cart*' should have been excluded
/*
[
  {
    id: 1,
    title: 'A book',
    price: 12.99,
    imageUrl: 'https://cdn.pixabay.com/photo/2016/03/31/20/51/book-1296045_960_720.png',
    description: 'This is an awesome book',
    'cartItem.id': 1,
    'cartItem.quantity': null,
    'cartItem.createdAt': 2023-05-01T00:51:04.000Z,
    'cartItem.updatedAt': 2023-05-01T00:51:04.000Z,
    'cartItem.cartId': 1,
    'cartItem.productId': 1
  }
]
*/
```