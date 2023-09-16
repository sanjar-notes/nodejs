# 181. Creating and managing the connection
Created Friday 19 May 2023 at 01:28 am


## Creating the database connection
- Creating a connection. Copy the SRV address (from the website) and add the password (use an [env variable](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/226967b78f8741422a48e901144ea69cc60470cf))
	```js
	// file /util/database.js
	const mongodb = require('mongodb');
	const MongoClient = mongodb.MongoClient;

	const mongoConnect = callback => {
	  MongoClient.connect(
	    'mongodb+srv://maximilian:9u4biljMQc4jjqbe@cluster0-ntrwp.mongodb.net/test?retryWrites=true'
	  )// Copied from the site (SRV address)
	    .then(client => {
	      console.log('Connected!');
	      callback(client);
	    })
	    .catch(err => {
	      console.log(err);
	    });
	};
	
	module.exports = mongoConnect; // is a function
	```
- Use the connection code in main app file (`app.js`)
	```js
	const mongoConnect = require('./util/database.js')

	// express code

	// start express from inside the mongoConnect callback
	mongoConnect((client) => {
		console.log(client);
		app.listen(3000);
	});
	```

[Code till here](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/a3b84f8383ce314699f83539f86e89dde6dfa767)


## Better connection management
Currently, we need to use util/database.js for every DB operation. This is not ideal, since this means creating a new connection for each op. Also, we won't be able to close the connection.

Let's change the database util to prevent this.
```js
const mongodb = require('mongodb');
const MongoClient = mongodb.MongoClient;

let _db;

const mongoConnect = callback => {
  MongoClient.connect(
    'mongodb+srv://maximilian:9u4biljMQc4jjqbe@cluster0-ntrwp.mongodb.net/shop?retryWrites=true'
  )
    .then(client => {
      console.log('Connected!');
      _db = client.db();
      callback();
    })
    .catch(err => {
      console.log(err);
      throw err;
    });
};

const getDb = () => {
  if (_db) {
    return _db;
  }
  throw 'No database found!';
};

exports.mongoConnect = mongoConnect;
exports.getDb = getDb;
```
This way we'll import and try to *reuse* the connection (`getDb`). If this throws an error, we'll create a fresh connection (`mongoConnect`) and then use `getDb`.

This is a good pattern. [Code/Commit](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/a0e061c4294ee11922e7d8336372214e16c42c65)


## Create on first interaction - philosophy of MongoDB
Sequelize, or SQL requires the database or table to be present before a create op can be done. This is not the case with MongoDB. A create call in MongoDB will create all preceding "layers" automatically, if they don't exist.