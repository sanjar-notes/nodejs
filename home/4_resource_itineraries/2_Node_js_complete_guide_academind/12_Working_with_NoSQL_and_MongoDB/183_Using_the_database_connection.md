# 183. Using the database connection
Created Friday 19 May 2023 at 01:30 am

## Using the database connection
```js
const { mongoConnect, getDb } = require("./util/database.js");

mongoConnect((client) => {
  const db = getDb();

  // database setup code, if needed
  await db
	  .collection('trial-collection')
	  .insertOne({name: 'Woods', friendName: 'Mason'});
	  
  app.listen(3000);
});

```
```js
// at any other place (the code will run after server starts anyway)
const { getDb } = require("./util/database.js");

let db = getDb();
if(!db) mongoConnect();
while(!db) db = getDb();

db.collection('trial-collection')
  .insertOne({name: 'Woods', friendName: 'Mason'})
  .then (console.log)
  .catch(console.log);
```
[Code/commit](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/f9e55013b1b4b11597552fff9e5848b17a958702)


## Creating the models
Since we don't have a SQL database now, the Sequelize models will not work. Let's create the Product model again (we'll use a class again, just like we did earlier when using files for storage):
```js
class Product {
	constructor(price, title, description, ...)
	{
		this.price = price;
		this.title = title;
		...
	}

	save() {
		// interact with MongoDB
	}
}
```


## Using the database connection/creating products
```js
const getDb = require('./util/database.js').getDb;

class Product {
	// some code here

	async create() {
	// assume no stupid errors occur

	  const db = getDb();
	  const result =
	  await db.collection('products').insertOne(this);

	// result has an `_id` that was autoassigned by MongoDB
	// Not stored at the top level though, so result._id won't have it
	}
}
```
[Code/commit](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/0adc534cb2c0e40538fdb51b5c3dd7b01fbcf605) - uses `findOne`

We used `insertOne`, `findOne` here. 
Learn more about CRUD ops - https://www.mongodb.com/docs/manual/crud/

Note: We need to comment out code that won't work, of course - in controllers and routes.