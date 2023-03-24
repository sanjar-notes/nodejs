# 153. Syncing Models to the Database
Created Friday 24 March 2023 at 10:41 pm

Sequelize can create tables from scratch, of course.
```js
await sequelize.sync(); // instance of Sequelize class
```

This is run only once, when the server app starts.

Note
- Sequelize instance has knowledge of all models, so all tables can be created.
- Tables are not created if they already exist. This is the default.

[Code](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/27bbb267d225ed0b35d867d462567bd3107cbde1)