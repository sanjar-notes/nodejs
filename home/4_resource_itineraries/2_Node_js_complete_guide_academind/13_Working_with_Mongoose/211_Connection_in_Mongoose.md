## 211. Connecting to the MongoDB Server with Mongoose
Created Sunday 7 May 2023 at 08:25 pm

Mongoose docs  - https://mongoosejs.com/docs/

Install Mongoose by running `npm install mongoose`. It's a core dependency of course.

Mongoose manages one connection for us. Our code will change like this:
```js
const mongoose = require('mongoose');

// express code

mongoose
	.connect('SRV_link_with_username_and_password')
	.then(() => app.listen(3000))
	.catch(console.log);
```
At all places of use, we can use `mongoose` directly (by importing the package), there's no need for a util/database.js file. We can delete that file.


## We can still have a database.js util
Created Monday 29 May 2023 at 01:50 am

Mongoose has very little connection code, but we can still have a util for database connection. The goal here is to keep the structure same for mongoose and mongodb, and not clutter the main app file.

```js
// database.js
const mongoose = require("mongoose");

// Note: 'mongooseConnect' is a name I made up
const mongooseConnect = async (cb) =>
  mongoose
    .connect(
      `mongodb+srv://sanjarcode-nodejscompleteguide:${database_password}@cluster-nodejscompleteg.nuohpop.mongodb.net/?retryWrites=true&w=majority`
    )
    .then(cb)
    .catch(console.log);

module.exports = {
  mongooseConnect,
  
  // remove these
  // mongoConnect,
  // getDb,
};
```

```js
// app.js
const {
  // mongoConnect, // not needed
  mongooseConnect
} = require("./util/database.js");
// express code

// mongoConnect(async (client) => {
//  app.listen(3000);
// });
// changes to somehing similar

mongooseConnect(async (mongooseObject) => {
  app.listen(3000);
});
```