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

[Code](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/ea51668c60fcfdec84f710da9fc785a177b27c60)