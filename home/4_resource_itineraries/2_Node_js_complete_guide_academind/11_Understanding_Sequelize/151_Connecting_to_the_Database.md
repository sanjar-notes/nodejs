# 151. Connecting to the Database
Created Friday 24 March 2023 at 10:03 pm

## Installing Sequelize
- Package name is "sequelize".
- Run `npm install sequelize` to install

Note: Sequelize needs a driver package to work. `mysql2` is fine.


## Connecting to the database
Sequelize uses `mysql2` behind the scenes. Therefore, we don't need to write `mysql2` code (i.e. creating a pool) ourselves. Of course, we still need to give the credentials. [API reference](https://sequelize.org/api/v6/class/src/sequelize.js~sequelize#instance-constructor-constructor)

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


## Creating DB from node, too
Sequelize, by default, expects the DB to be present (this means we need to create it from the terminal/DB tool). This can be bypassed (because Sequelize exposes part of `mysql2`, which doesn't have a "DB should exist" requirement). Updated [code](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/422983ac6dee09fc7c46f1518912a4ec20d07679):
```js
const Sequelize = require("sequelize");

// work even if DB does not exist
const sequelize = new Sequelize({
  username: "root",
  password: database_password,
  host: "localhost",
  dialect: "mysql",

  hooks: {
    afterConnect: async (connection, options) => {
      // connection is a mysql2 connection, since Sequelize used mysq2 under the hood/
      // also, Sequelize assumes a DB is present. We are bypassing this by using the mysql2 part Sequelize exposes, since
      // mysql2 has no "DB should exist" requirement. All it needs are creds and the DB to be running
      await connection
        .promise()
        .query("CREATE DATABASE IF NOT EXISTS " + database_name);
      options.database = database_name; // connect to the newly created DB
    },
  },
});
```
Note: all hooks, like `afterBulkSync` can be added here itself.