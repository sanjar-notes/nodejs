# 188. Edit and delete product
Created Sunday 7 May 2023 at 10:01 am

## Adding `_id` to model (tip)
Add a `_id` attribute to the Product model. This is a nice thing to do since it limits the need create `ObjectId`, to just inside model, and away from the app code.

Also, since `ObjectId` has the `.toString` method, template engines will (atuomatically) work just fine with `_id` being an object.

Note: make sure the `_id` is null if absent from the constructor, since `new ObjectId(null)` is still a valid `ObjectId`. A weird quirk from MongoDB, but fine.

[Code](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/60df5e3f7377c3dc883553ea93bc08f78f4001d9)


## Delete product
`deleteOne`

Add **delete** method to the Product model.
Example:
```js
const mongodb = require("mongodb");

class Product {
  constructror(id) {
    this.id = id;
    // ... some code
  }

  delete() {
    const idObject = new mongodb.ObjectId(this.id);
    const db = getDb();

    return db
      .collection("products")
      .deleteOne({ _id: idObject })

      .then((result) => {
        console.log(result);
      })
      .catch((err) => {
        console.log(err);
      });
  }
  // ... some code
}
```

Note:
- Delete one - `deleteOne()`
- Delete many - `deleteMany()`
- The argument is the criteria or `_id`, just like with `.find` and `.findOne`.

[Delete Product - code](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/b4f51b381f6abb037125121b543579a8707c5436)


## Edit product
`updateOne` - this one is special since it takes a payload argument.

Let's add **edit** methods to the Product model.
Example:
```js
const mongodb = require("mongodb");

class Product {
  constructror(id) {
    this.id = id;
    // ... some code
  }
  // ... some code

  update() {
    const idObject = new mongodb.ObjectId(this.id);
    const db = getDb();

    const updatePayload = { ...this };
    delete updatePayload._id; // since this is a string now

    return db
      .collection("products")
      .updateOne({ _id: idObject }, { $set: updatePayload })

      .then((result) => {
        console.log(result);
      })
      .catch((err) => {
        console.log(err);
      });
  }
}
```

- **Update** (`updateOne()`) takes two arguments
  1.  A query filter. Example - `_id` or criteria.
  2.  Second is an object, which should at-least have `$set` key with the update payload. MongoDB does "merged updation" by default. 

Note:
- It's ok to send `_id` in payload, but it must be an object not a string and must be the same as the existing one (FIXME check that it must be same or not).
- `_id` in payload (if sent) should be of type `ObjectId`, otherwise mongodb will throw an error. Obvious.

[Edit Product - code](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/bc69c7c8498808f173ba6216ebc437af247e330e)