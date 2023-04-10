# 154. Queries
Created Tuesday 28 March 2023 at 12:05 am
Created 

Models created using Sequelize expose a lot of functionality (the core ORM) part. This functionality may be static or non-static methods, or even properties.

## CRUD ops
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
	await Product.findBy(1, {
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
