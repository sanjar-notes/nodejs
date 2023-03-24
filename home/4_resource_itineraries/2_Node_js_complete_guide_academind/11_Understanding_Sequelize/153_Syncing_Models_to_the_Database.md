# 153. Syncing Models to the Database
Created Friday 24 March 2023 at 10:41 pm

Sequelize can create tables from scratch, of course.
```js
await sequelize.sync(); // instance of Sequelize class
```

This is run only once, when the server app starts. Example:
```js
const app = Express.app();
const sequelize = require('./util/database.js');

// ... code here

sequelize.sync()
	.then(() => { app.listen(3000); })
	.catch((err) => console.log(err));
```

Note
- Sequelize instance has knowledge of all models, so all tables can be created.
- Tables are not created if they already exist. This is the default.

---

This is it, the DB is ready for use. Code: [start](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/ea51668c60fcfdec84f710da9fc785a177b27c60) to [finish](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/27bbb267d225ed0b35d867d462567bd3107cbde1)