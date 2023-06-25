# ObjectId in Mongoose
Created Sunday 25 June 2023 at 03:46 pm

The `ObjectId` class is available in the `mongoose` package, i.e. there's no need to install the "mongoose" package just to use `ObjectId`.

Location:
```js
const mongoose = require('mongoose');
const ObjectId = mongoose.Types.ObjectId;

new ObjectId(); // works
```