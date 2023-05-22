# Creating the user model
Created Sunday 7 May 2023 at 10:01 am

We need to rewrite the User model, since we're not using Sequelize anymore.

Nothing special, same as adding the Product model. [Code](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/77beb7cd3f9edf18fc82f4cbdd81cdc15b24da3e). Example:
```js
const { getDb, mongoConnect } = require('./util/database.js');
const { ObjectId } = require("mongodb");

class User() {
  constructor(username, email) {
    this.username = username;
    this.email = email;
  }

  async create() {
    const db = getDb(); // for demo, assume this always works

	return db
			.collection('users')
			.insertOne(this)
			.then(console.log)
			.catch(console.log);
  }

  static async findById(userId) {
    const db = getDb();

    return db
		    .collection('users')
		    .findOne({ _id: new ObjectId(userId) });

		    // OR, equivalently
		    // .find({ _id: new ObjectId(userId) }).next();
  }
};
```
