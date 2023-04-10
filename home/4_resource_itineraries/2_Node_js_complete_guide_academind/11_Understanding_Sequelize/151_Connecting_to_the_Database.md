# 151. Connecting to the Database
Created Friday 24 March 2023 at 10:03 pm

## Installing Sequelize
- Package name is "sequelize".
- Run `npm install sequelize` to install

Note: Sequelize needs a driver package to work. `mysql2` is fine.


## Connecting to the database
Sequelize uses `mysql2` behind the scenes. Therefore, we don't need to write `mysql2` code (i.e. creating a pool) ourselves. Of course, we still need to give the credentials.
```js
const Sequelize = require("sequelize");

// (database, username, password, options)
const sequelize = new Sequelize("node-complete", "root", "my-password", {
  host: "localhost",
  dialect: "mysql",
});

module.exports = sequelize;
```

The entity we exported here is not just a connection pool:
1. It has many utilities
2. It's much more general than a pool
3. It's aware of all models in the app

This 'sequelize' variable will be used for all DB operations.

[Code](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/ea51668c60fcfdec84f710da9fc785a177b27c60)


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