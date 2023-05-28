# Using MongoDB and Mongoose together
Created Monday 29 May 2023 at 02:34 am

aka "Using raw MongoDB in Mongoose"

Mongoose and MongoDB can be used together. A DX disadvantage of doing this is that it makes using the database usage in the app a little confusing. 

But this (mixing) may be done deliberately, in some cases - if we need to use raw MongoDB (say a feature is absent from Mongoose and we wish to write a utility for it).

This is easily possible since, Mongoose is an abstraction over MongoDB.

To do this, simply connect using Mongoose, and store the corresponding "MongoDB" connection and database in a variable we can export anywhere in the app (the `_db` and `getDb` we have now). Under the hood, Mongoose does create a MongoDB connection. 

Also, there's no need to import the 'mongodb' package.

Updating the code:
```js
// database.js
const mongoose = require("mongoose");
const database_password = 'get it from env file';

let _db;

const mongooseConnect = async (cb) =>
  mongoose
    .connect(
      `mongodb+srv://sanjarcode-nodejscompleteguide:${database_password}@cluster-nodejscompleteg.nuohpop.mongodb.net/?retryWrites=true&w=majority`
    )
    .then(mongooseObject => {
      const mongoDbClient = mongooseObject.connection.getClient();
      _db = mongoDbClient.db();
    })
    .then(cb)
    .catch(console.log);


const getDb = () => {
  if (_db) {
    return _db;
  }
  throw "No database found!";
};


module.exports = {
  mongooseConnect,
  getDb
};
```

We have effectively made it possible to write simple MongoDB without any Mongoose constraints. 

Funnily enough, the app will work now without changes - it has no Mongoose models, but MongoDB code is there.