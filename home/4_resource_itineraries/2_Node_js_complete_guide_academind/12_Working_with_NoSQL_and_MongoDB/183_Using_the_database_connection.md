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