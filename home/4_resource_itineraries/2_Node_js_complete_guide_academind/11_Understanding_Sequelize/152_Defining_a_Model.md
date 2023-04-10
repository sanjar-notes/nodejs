# 152. Defining the a Model
Created Friday 24 March 2023 at 10:37 pm

## Creating models (and therefore tables)
Let's delete the products table from the database (using MySQL Workbench). 

We'll create tables using Sequelize.

Syntax for creating a model, in detail:
```js
const Sequelize = require('sequelize');
const sequelize = require('../path-to-sequelize-instance');

const MyModel = sequelize.define('modelName', {
	columnOneName: {
	    type: Sequelize.INTEGER,
	    allowNull: false,
	    autoIncrement: false,
	}
});

module.exports = MyModel;
```


```js
const Sequelize = require("sequelize");

const sequelize = require(path.join(rootDir, "util", "database.js"));

// 1. instance of sequelize, not the class
const Product = sequelize.define("product", {
  // 2. model name is typically in lowercase

  id: {
    type: Sequelize.INTEGER, // 3. JavaScriptish types
    autoIncrement: true,
    allowNull: false,
    primaryKey: true,
  },

  title: Sequelize.STRING, // 3. shorthand for title: { type: Sequelize.STRING }.
  // We should have added allowNull: false, but this is a demo for the shorthand

  price: {
    type: Sequelize.DOUBLE,
    allowNull: false,
  },

  description: {
    type: Sequelize.STRING,
    allowNull: false,
  },
});

module.exports = Product; // export for use elsewhere
```

[Code](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/89785f7d2302d9183f4747388badfc8cfa099e80)